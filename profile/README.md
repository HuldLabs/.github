# HuldLabs

Ferramentas para construir software em times pequenos: um método de trabalho, um design system e
frameworks por stack. Cada peça é um catálogo — o projeto instala só o que usa.

O conceito é **framework modular self-service multi-stack**: um projeto Python + React ou Python +
Jinja pode consumir o design system e a camada de método sem adotar um framework inteiro.

## As cinco peças

| Peça | Papel | O que é |
|---|---|---|
| [**Tars**](https://github.com/HuldLabs/tars) | como a gente trabalha | catálogo de método: camada `.ai`, gates, hooks, workers e memória. Transversal. |
| [**Tomo**](https://github.com/HuldLabs/tomo) | como o app aparece | design system: tokens (sem framework) e UI React; macros Jinja depois. Transversal e multi-stack. |
| [**Sofon**](https://github.com/HuldLabs/sofon) | o que o app é | framework da stack Next: kernel, serviços de núcleo (jobs, mensageria, IAM, IA, segredos, egress), módulos e banco. |
| [**Pion**](https://github.com/HuldLabs/pion) | o que o app é | framework da stack Python. |
| [**Kipp**](https://github.com/HuldLabs/kipp) | como o trabalho anda | projetos, itens, board e canal dos agentes (MCP). Instância global ou módulo do Sofon. |

## Regras transversais

- **Catálogo, não pacote fechado.** Cada peça publica itens; o projeto declara o que importa e o
  sync puxa só o declarado, com versão e hash travados num lock.
- **Nada exige um runtime de quem não o usa.** Um repo só Python é caso de primeira classe; um repo
  só Node também. Cada item declara a stack que pede.
- **Ferramenta transversal sai como binário único** — `tars` já é; `kipp` e `tars secrets` virão.
  Quem consome não instala o runtime de outra stack.
- **Segredos:** 1Password é a fonte; no dia a dia, cache sops + age; 1Password só no refresh.
- **Distribuição de pacotes no GitHub Packages privado**, escopo `@huldlabs`.

## Origem dos nomes

Nomes de ficção científica, escolhidos pelo que descrevem. **Sofon** e **Tomo** vêm de *O Problema
dos Três Corpos*: o sófon é um próton desdobrado em supercomputador, e Tomoko é o avatar dele — a
face do sófon, que é o papel do design system. **Pion** é o méson pi, uma partícula subatômica:
cada stack nova é uma partícula (PHP será *Phonon*). **Tars** e **Kipp** são os robôs de
*Interstellar*: o TARS tem módulos que se rearranjam conforme a tarefa, com parâmetros ajustáveis; o KIPP é o irmão dele, e o nome soa como *keep* (guardar tarefas e lembretes).

## Estado hoje

- **Tars** — publicado, com binário e README.
- **Kipp** — nasceu: README, ADR-0001, consome o Tars; ainda sem código.
- **Sofon** e **Tomo** — em extração a partir do segtools.
- **Pion** — nasce no seo-brain.
