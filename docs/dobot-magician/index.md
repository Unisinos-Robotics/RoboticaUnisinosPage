---
icon: lucide/book-open
---

# Robótica Colaborativa com Dobot Magician

**Ebook técnico da Robótica Unisinos**: fundamentos teóricos, segurança,
operação, programação via API e estudos de caso.

<figure markdown="span">
  ![Dobot Magician](assets/aparencia.png){ width="640" }
  <figcaption>Dobot Magician: base, braço traseiro, antebraço e efetuador. Fonte: Dobot Magician User Guide V2.3.14.</figcaption>
</figure>

## Sobre este ebook

O Dobot Magician é um braço robótico de mesa usado no laboratório para ensino e
prototipagem. Este material reúne, em português, tudo o que você precisa para
operá-lo com segurança e programá-lo: dos conceitos de robótica colaborativa ao
código Python que move o robô.

O conteúdo de operação foi adaptado do capítulo 5 (*Operation*) do manual
oficial **Dobot Magician User Guide (DobotLab-based) V2.3.14**, complementado com
material de referência sobre normas de segurança e com a biblioteca
[`pydobot`](https://pypi.org/project/pydobot/).

!!! warning "O Magician não é um cobot certificado"

    O Magician é um braço **educacional**. Ele não é certificado como robô
    industrial pela ISO 10218 e não deve ser tratado como um equipamento seguro
    para contato com pessoas. Usamos o Magician para **aprender** os conceitos e
    as práticas de robótica colaborativa num equipamento de baixo risco. Veja o
    [capítulo 5](seguranca/normas.md).

## Como ler

<div class="grid cards" markdown>

-   :lucide-graduation-cap: __Parte I · Fundamentos__

    ---

    O que é robótica colaborativa, o hardware do Magician, cinemática,
    workspace, sistemas de coordenadas e interfaces elétricas.

    [:lucide-arrow-right: Capítulo 1](fundamentos/robotica-colaborativa.md)

-   :lucide-shield-check: __Parte II · Segurança__

    ---

    Normas (ISO 10218, ISO/TS 15066, NR-12), avaliação de risco e os
    procedimentos seguros adotados no laboratório.

    [:lucide-arrow-right: Capítulo 5](seguranca/normas.md)

-   :lucide-wrench: __Parte III · Operação__

    ---

    DobotLab, Blockly, desenho, laser, teaching & playback, impressão 3D,
    calibração, modo offline, joystick e I/O.

    [:lucide-arrow-right: Capítulo 7](operacao/dobotlab.md)

-   :lucide-code: __Parte IV · Programação via API__

    ---

    Python no DobotLab, a biblioteca `pydobot` e padrões de código seguro.

    [:lucide-arrow-right: Capítulo 16](programacao/python-dobotlab.md)

-   :lucide-flask-conical: __Parte V · Estudos de caso__

    ---

    Pick-and-place com ventosa, desenho por trajetória e integração com
    sensores via I/O.

    [:lucide-arrow-right: Capítulo 19](casos/pick-and-place.md)

-   :lucide-library: __Glossário e referências__

    ---

    Termos técnicos, manuais oficiais, normas e bibliografia.

    [:lucide-arrow-right: Referências](referencias.md)

</div>

## Roteiros sugeridos

| Perfil | Caminho |
|---|---|
| Primeiro contato com o robô | Cap. [2](fundamentos/magician.md) → [6](seguranca/procedimentos.md) → [7](operacao/dobotlab.md) → [11](operacao/teaching-playback.md) |
| Quero programar em Python | Cap. [3](fundamentos/cinematica.md) → [6](seguranca/procedimentos.md) → [17](programacao/pydobot.md) → [18](programacao/boas-praticas.md) → [19](casos/pick-and-place.md) |
| Projeto com sensores e atuadores | Cap. [4](fundamentos/conexao-interfaces.md) → [15](operacao/io.md) → [21](casos/sensor-io.md) |
| Disciplina de robótica colaborativa | Partes I e II completas, depois os estudos de caso |

## Convenções

!!! danger "Perigo"
    Risco alto, que pode causar ferimento grave.

!!! warning "Atenção"
    Risco médio ou baixo, que pode causar ferimento leve ou danificar o robô.

!!! note "Nota"
    Informação complementar.

Cada capítulo começa com os **objetivos** e termina com a **fonte** no manual
oficial, para você consultar o original quando precisar.

??? info "Créditos das figuras"

    As figuras marcadas com "Fonte: Dobot Magician User Guide" foram reproduzidas
    do manual oficial da Shenzhen Yuejiang Technology Co., Ltd. (Dobot), para fins
    educacionais. Os direitos pertencem ao fabricante.
