---
icon: lucide/library
---

# Glossário e referências

## Glossário

| Termo | Significado |
|---|---|
| **ADC** | Conversor analógico-digital. No Magician, lê de 0 a 4095 com entrada máxima de 5 V. |
| **Aplicação colaborativa** | Combinação de robô, ferramenta, tarefa e ambiente em que pessoa e robô compartilham o espaço de trabalho. É o que se avalia quanto ao risco. |
| **ARC** | Movimento em arco definido por três pontos. |
| **Cobot** | Robô projetado para trabalhar próximo de pessoas. Termo de Colgate e Peshkin (1996). |
| **Cinemática direta / inversa** | Cálculo da pose a partir dos ângulos das juntas, e o inverso. |
| **DobotLab** | Plataforma web de programação e operação da Dobot. |
| **DobotLink** | Driver local que conecta o DobotLab ao hardware. |
| **Efetuador** (*end-effector*) | Ferramenta na ponta do braço: ventosa, garra, caneta, laser, extrusora. |
| **EIO** | *Extended I/O*: pinos de I/O endereçados de 1 a 20. |
| **Fila de comandos** | Buffer do controlador que executa comandos em ordem. |
| **Guiamento manual** (*hand guiding*) | Conduzir o robô com as mãos. No Magician, com o botão Unlock. |
| **Homing** | Procedimento em que o robô busca o limite e volta à origem para referenciar as juntas. |
| **Jog** | Movimento manual eixo a eixo pelos botões. |
| **JUMP** | Movimento em "porta": sobe, desloca e desce. |
| **MOVJ / MOVL** | Movimento de juntas (trajetória livre) / linear (linha reta). |
| **Multiplexação** | Escolha da função de um pino de I/O (DO, DI, PWM, ADC). |
| **Perda de passo** (*lost step*) | Quando o motor de passo não executa todos os passos comandados e a posição real difere da calculada. |
| **PFL** | *Power and force limiting*: limitação de potência e força. |
| **PTP** | Movimento ponto a ponto. |
| **PWM** | Modulação por largura de pulso. |
| **Repetibilidade** | Capacidade de voltar ao mesmo ponto (0,2 mm no Magician). |
| **SSM** | *Speed and separation monitoring*: monitoramento de velocidade e separação. |
| **Teaching & playback** | Programar mostrando os pontos e reproduzindo a sequência. |
| **Workspace** | Volume alcançável pela ponta do robô. |

## Documentação oficial da Dobot

- *Dobot Magician User Guide (DobotLab-based)*, V2.3.14, 18/04/2024. Shenzhen
  Yuejiang Technology Co., Ltd. Fonte principal dos capítulos 2 a 15.
- *Dobot Magician Communication Protocol*, V1.1.5, 05/08/2019.
  [PDF](https://download.dobot.cc/product-manual/dobot-magician/pdf/en/Dobot-Communication-Protocol-V1.1.5.pdf).
- *Dobot Magician API Description*.
  [Download Center](https://en.dobot.cn/service/download-center?keyword=&products%5B%5D=316).
- DobotLab: <https://dobotlab.dobot.cc/>.

## Software

- `pydobot` 1.3.2: [PyPI](https://pypi.org/project/pydobot/) ·
  [GitHub](https://github.com/luismesas/pydobot).
- `pyserial`: <https://pyserial.readthedocs.io/>.
- Repetier Host (pacote da Dobot): <https://download.dobot.cc/3D/RepetierHost.zip>.

## Normas

- ISO 12100: *Safety of machinery — General principles for design — Risk
  assessment and risk reduction*.
- ISO 10218-1 e ISO 10218-2: *Robotics — Safety requirements* (edições de
  2011, revisadas em 2025).
- ISO/TS 15066:2016: *Robots and robotic devices — Collaborative robots*
  (conteúdo incorporado à ISO 10218:2025).
- ISO 13849-1: *Safety of machinery — Safety-related parts of control systems*.
- NR-12: *Segurança no Trabalho em Máquinas e Equipamentos*, Ministério do
  Trabalho e Emprego.

## Bibliografia

- J. E. Colgate, W. Wannasuphoprasit e M. A. Peshkin, "Cobots: Robots for
  collaboration with human operators", *Proceedings of the ASME Dynamic Systems
  and Control Division*, 1996.
- Control Design, ["ISO 10218 update makes functional-safety requirements more
  explicit"](https://www.controldesign.com/industry-news/news/55268769/iso-10218-update-makes-functional-safety-requirements-more-explicit).

## Créditos

As figuras indicadas como "Fonte: User Guide" foram reproduzidas do manual
oficial da Dobot, para fins educacionais. Todos os direitos sobre essas figuras
pertencem à Shenzhen Yuejiang Technology Co., Ltd.
