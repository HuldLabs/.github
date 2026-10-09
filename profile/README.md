# HuldLabs

Ferramentas para construir software em times pequenos: um método de trabalho, um design system e
frameworks por stack. Cada peça é um catálogo — o projeto instala só o que usa.

O conceito é **framework modular self-service multi-stack**: um projeto Python + React ou Python +
Jinja pode consumir o design system e a camada de método sem adotar um framework inteiro.

## As peças

| Peça | Papel | O que é |
|---|---|---|
| [**Tars**](https://github.com/HuldLabs/tars) | como a gente trabalha | catálogo de método: camada `.ai`, gates, hooks, workers e memória. Transversal. |
| [**Tomo**](https://github.com/HuldLabs/tomo) | como o app aparece | design system: tokens (sem framework) e UI React; macros Jinja depois. Transversal e multi-stack. |
| [**Sofon**](https://github.com/HuldLabs/sofon) | o que o app é | framework da stack Next: kernel, serviços de núcleo (jobs, mensageria, IAM, IA, segredos, egress), módulos e banco. |
| [**Pion**](https://github.com/HuldLabs/pion) | o que o app é | framework da stack Python. |
| [**Kipp**](https://github.com/HuldLabs/kipp) | como o trabalho anda | projetos, itens, board e canal dos agentes (MCP). Instância global ou módulo do Sofon. |
| [**Bulq**](https://github.com/HuldLabs/bulq) | onde o segredo mora | motor de segredos portátil e agnóstico de provedor; referência neutra `sec://`. Transversal. |
| [**Murph**](https://github.com/HuldLabs/murph) | o que sobrevive | backup com deduplicação e cifra age, restauração testada. Transversal. |

E o ambiente onde elas rodam: [**Endurance**](https://github.com/HuldLabs/endurance), o
devcontainer do ecossistema — não é peça, é a nave.

## Regras transversais

- **Catálogo, não pacote fechado.** Cada peça publica itens; o projeto declara o que importa e o
  sync puxa só o declarado, com versão e hash travados num lock.
- **Nada exige um runtime de quem não o usa.** Um repo só Python é caso de primeira classe; um repo
  só Node também. Cada item declara a stack que pede.
- **Ferramenta transversal sai como binário único** — `tars` já é, com `tars secrets` dentro; `kipp`
  virá. Quem consome não instala o runtime de outra stack.
- **Segredos:** 1Password é a fonte; no dia a dia, cache sops + age com chave por projeto;
  1Password só no refresh. Cada comando declara se roda como automação (service account) ou como
  dono, sem fallback entre os dois. O catálogo nunca guarda referência `op://`.
- **Distribuição de pacotes no GitHub Packages privado**, escopo `@huldlabs`.

## Origem dos nomes

Nomes de ficção científica, escolhidos pelo que descrevem. **Sofon** e **Tomo** vêm de *O Problema
dos Três Corpos*: o sófon é um próton desdobrado em supercomputador, e Tomoko é o avatar dele — a
face do sófon, que é o papel do design system. **Pion** é o méson pi, uma partícula subatômica:
cada stack nova é uma partícula (PHP será *Phonon*). **Tars** e **Kipp** são os robôs de
*Interstellar*: o TARS tem módulos que se rearranjam conforme a tarefa, com parâmetros ajustáveis; o KIPP é o irmão dele, e o nome soa como *keep* (guardar tarefas e lembretes). **Murph** é a filha do Cooper, quem guarda
a mensagem e salva todo mundo com ela; **Endurance** é a nave que leva os robôs. **Bulq** vem de
*bulk*: segredos em lote, entregues no tamanho pedido.

## Estado hoje

- **Tars** — publicado (`0.0.1-dev.9`), com binário, README e `tars secrets` (refresh, exec,
  check, rotate).
- **Kipp** — nasceu: README, ADR-0001, consome o Tars; ainda sem código.
- **Sofon** e **Tomo** — em extração a partir do segtools.
- **Pion** — nasce no seo-brain.
- **Bulq** — desenho decidido, sem código; vem antes do `tars identity`.
- **Murph** — desenho decidido; extração a partir do backup do Fabber.
- **Endurance** — devcontainer na `main`; a tag `v0.1.0` espera o Tars dev.10.
