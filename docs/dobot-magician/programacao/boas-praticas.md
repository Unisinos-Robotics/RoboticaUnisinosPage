---
icon: lucide/shield-alert
---

# 18. Padrões de código seguro

!!! abstract "Objetivos do capítulo"

    - Aplicar ao código os princípios de redução de risco do [cap. 5](../seguranca/normas.md).
    - Validar alvos antes de enviá-los ao robô.
    - Estruturar scripts que sempre terminam em estado seguro.

No laboratório, a maior parte dos acidentes com robôs pequenos vem do
**software**: uma coordenada digitada errada, um laço que não termina, uma
velocidade alta esquecida. Este capítulo reúne padrões simples que evitam esses
problemas.

## 18.1 Princípios

| Princípio | Na prática |
|---|---|
| **Falhar antes de mover** | Valide cada alvo contra uma "caixa segura" antes de enviá-lo. |
| **Começar devagar** | `speed(20, 20)` nos primeiros testes; aumente aos poucos. |
| **Testar no ar** | Rode a trajetória com Z deslocado para cima antes da versão real. |
| **Terminar em estado conhecido** | `try/finally`: desligar a ventosa ou o laser, subir e fechar a porta. |
| **Uma fonte da verdade** | Coordenadas em constantes nomeadas, não espalhadas pelo código. |
| **Humano no circuito** | Peça confirmação antes de movimentos grandes ou do primeiro ciclo. |

## 18.2 Um wrapper defensivo

```python title="seguro.py" linenums="1"
import math
from contextlib import contextmanager

from magician import Magician  # extensão do capítulo 17

# Caixa segura do laboratório: ajuste à sua bancada.
X_MIN, X_MAX = 150.0, 300.0
Y_MIN, Y_MAX = -150.0, 150.0
Z_MIN, Z_MAX = -55.0, 120.0     # Z_MIN: um pouco acima da mesa (meça!)
R_MIN, R_MAX = -90.0, 90.0
RAIO_MIN, RAIO_MAX = 160.0, 310.0  # anel alcançável, com margem
VEL_MAX = 50.0                  # % de velocidade permitida


class AlvoInseguro(ValueError):
    pass


def validar(x, y, z, r=0.0):
    raio = math.hypot(x, y)
    problemas = []
    if not X_MIN <= x <= X_MAX: problemas.append(f"x={x} fora de [{X_MIN}, {X_MAX}]")
    if not Y_MIN <= y <= Y_MAX: problemas.append(f"y={y} fora de [{Y_MIN}, {Y_MAX}]")
    if not Z_MIN <= z <= Z_MAX: problemas.append(f"z={z} fora de [{Z_MIN}, {Z_MAX}]")
    if not R_MIN <= r <= R_MAX: problemas.append(f"r={r} fora de [{R_MIN}, {R_MAX}]")
    if not RAIO_MIN <= raio <= RAIO_MAX: problemas.append(f"raio={raio:.0f} fora do anel")
    if problemas:
        raise AlvoInseguro("; ".join(problemas))


class MagicianSeguro(Magician):
    """Magician que recusa alvos fora da caixa segura e limita a velocidade."""

    def __init__(self, port, ensaio=False, **kw):
        super().__init__(port, **kw)
        self.ensaio = ensaio            # True = só imprime, não move
        self.speed(20, 20)              # o construtor do pydobot deixa em 100%

    def speed(self, velocity=20.0, acceleration=20.0):
        super().speed(min(velocity, VEL_MAX), min(acceleration, VEL_MAX))

    def _mover(self, metodo, x, y, z, r, wait):
        validar(x, y, z, r)
        if self.ensaio:
            print(f"[ensaio] {metodo.__name__}({x:.1f}, {y:.1f}, {z:.1f}, {r:.1f})")
            return
        metodo(x, y, z, r, wait=wait)

    def move_to(self, x, y, z, r=0.0, wait=True):
        self._mover(super().move_to, x, y, z, r, wait)

    def jump_to(self, x, y, z, r=0.0, wait=True):
        self._mover(super().jump_to, x, y, z, r, wait)


@contextmanager
def conectar(porta, ensaio=False):
    """Abre o robô e garante um final seguro, mesmo com erro ou Ctrl+C."""
    robo = MagicianSeguro(porta, ensaio=ensaio)
    try:
        yield robo
    finally:
        if not robo.ensaio:
            try:
                robo.pump_off()
                x, y, z, r, *_ = robo.pose()
                robo.move_to(x, y, min(z + 30, Z_MAX), r, wait=True)  # sobe
            except Exception as e:  # o fechamento não pode falhar
                print(f"Aviso ao finalizar: {e}")
        robo.close()
```

Uso:

```python
from seguro import conectar

with conectar("/dev/ttyUSB0", ensaio=True) as robo:   # 1º: ensaio, só imprime
    robo.move_to(220, 0, 50)
    robo.jump_to(220, 80, -20)
```

No modo ensaio, o script conecta ao robô (para ler a pose, por exemplo), mas
só **imprime** os movimentos. Quando a saída estiver correta, troque para
`ensaio=False`.

## 18.3 "Teste no ar"

Antes de executar uma trajetória rente à mesa, rode a mesma trajetória com um
**deslocamento em Z**:

```python
DZ_TESTE = 40  # mm acima da trajetória real; use 0 na execução final

for (x, y, z) in trajetoria:
    robo.move_to(x, y, z + DZ_TESTE)
```

## 18.4 Parando o robô

| Meio | Efeito |
|---|---|
| `Ctrl+C` no script | Interrompe o Python. Com `try/finally`, o robô termina o comando atual e o script finaliza em estado seguro. **Comandos já enfileirados continuam executando.** |
| Botão Stop do DobotLab | Parada de emergência por software (só com o DobotLab conectado). |
| Botão **Reset** da base | Reinicia o controlador: o robô para e desconecta. |
| Botão **Power** | Desliga. Último recurso: o braço recolhe ao desligar. |

!!! tip "Envie aos poucos"

    Para manter o `Ctrl+C` eficaz, use `wait=True`. Assim a fila do robô tem no
    máximo um movimento pendente e a parada é rápida.

!!! info "Entrada STOP KEY"

    A interface de comunicação da base tem uma entrada chamada **STOP KEY**
    (EIO20), com pull-up de 10 kΩ ([cap. 4](../fundamentos/conexao-interfaces.md#46-io-multiplexado-eio)).
    O manual não detalha o comportamento dela. Se for usá-la, teste com cuidado
    e não a trate como uma parada de emergência certificada.

## 18.5 Checklist de revisão de código

- [ ] Todas as coordenadas passam por `validar()` ou por uma função equivalente.
- [ ] `speed()` é chamado logo após conectar.
- [ ] Há `try/finally` ou gerenciador de contexto fechando a porta.
- [ ] Efetuadores (bomba, laser) são desligados no `finally`.
- [ ] O último movimento usa `wait=True`.
- [ ] A primeira execução foi feita em **ensaio** e depois com **teste no ar**.
- [ ] Constantes de posição estão nomeadas e documentadas (de onde vieram e como foram medidas).
