---
icon: lucide/house
hide:
  - navigation
  - toc
---

# Robótica Unisinos

**Documentação, guias e relatórios do grupo de robótica da Unisinos.**

Aqui reunimos o material técnico produzido no laboratório: manuais de operação
dos robôs, tutoriais de programação, procedimentos de segurança e estudos de caso
para quem está começando ou quer se aprofundar.

[Ler o ebook do Dobot Magician](dobot-magician/index.md){ .md-button .md-button--primary }
[GitHub](https://github.com/Unisinos-Robotics){ .md-button }

## Sobre o grupo

A Robótica Unisinos é um grupo de estudantes e pesquisadores da Universidade do
Vale do Rio dos Sinos (Unisinos) dedicado ao estudo, à programação e à aplicação
de robôs. Este site é a base de conhecimento do grupo: tudo o que aprendemos
operando os equipamentos do laboratório fica documentado aqui para as próximas
turmas.

## Documentação

<div class="grid cards" markdown>

-   :lucide-bot: __Dobot Magician__

    ---

    Ebook técnico sobre robótica colaborativa usando o Dobot Magician:
    fundamentos, segurança, operação com DobotLab, programação em Python
    (`pydobot`) e estudos de caso.

    [:lucide-arrow-right: Abrir o ebook](dobot-magician/index.md)

-   :lucide-construction: __Em breve__

    ---

    Novos robôs, projetos e relatórios do laboratório serão publicados aqui.
    Quer documentar algo? Veja [como participar](#contato-e-como-participar).

</div>

## Contato e como participar

- **GitHub:** [github.com/Unisinos-Robotics](https://github.com/Unisinos-Robotics)
- **Encontrou um erro ou quer sugerir um conteúdo?** Abra uma
  [issue](https://github.com/Unisinos-Robotics/RoboticaUnisinosPage/issues).
- **Quer contribuir com a documentação?** Crie uma branch a partir da `main`,
  escreva suas páginas em Markdown dentro de `docs/` e abra um pull request.
  Todo conteúdo é revisado antes de ser publicado.

!!! tip "Rodando o site localmente"

    ``` sh
    uv sync
    uv run zensical serve
    ```

    O site fica disponível em <http://localhost:8000>.
