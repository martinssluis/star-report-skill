[English](README.md) · **Português**

# star-report

Uma skill de agente que transforma o seu trabalho de software em relatórios reutilizáveis — numa reunião, numa entrevista, num pull request ou no histórico técnico do projeto.

A novidade: ela pode **documentar enquanto você resolve o problema**. Comece uma sessão de debug ou uma feature com a skill ativa e ela mantém um registro da sessão conforme o trabalho anda — o bug reproduzido, as hipóteses descartadas, a decisão tomada, o teste que provou a correção. Quando você termina, o registro vira o relatório. Nada de reconstruir de memória o que você fez duas semanas atrás.

Ela é escrita em Markdown puro, no formato `SKILL.md`, e funciona em **qualquer agente que leia skills** — Claude Code, Claude.ai, GitHub Copilot, Codex, Cursor e outros.

---

## Dois modos

| Modo | Quando | O que acontece |
|---|---|---|
| **Ao vivo** | O problema está sendo resolvido agora | A skill mantém um registro da sessão, atualizado a cada marco, e escreve o relatório no fim |
| **Retrospectivo** | O trabalho já foi feito | Você descreve informalmente; a skill pergunta o que falta e escreve o relatório |

### Como funciona o modo ao vivo

```
problema reproduzido ─► hipótese testada ─► causa raiz ─► decisão ─► correção aplicada ─► verificado
         │                     │                 │            │               │                │
         └─────────────────────┴─────────────────┴── registro da sessão ──────┴────────────────┘
                                                           │
                                                           ▼
                                      STAR · Resumo Técnico · Decisão Técnica
```

As atualizações são discretas: uma linha no fim da resposta (`📝 Registro atualizado: causa raiz`). As perguntas para o relatório ficam para o final — resolver o problema vem primeiro. Em agentes com acesso a arquivos, o registro é um Markdown no seu projeto (por padrão `docs/deliveries/AAAA-MM-DD-<slug>.md`); em interfaces de chat, ele fica na própria conversa.

> Uma skill é acionada pela descrição ou quando você a invoca. Para ter o modo ao vivo, chame a skill (ou peça para "documentar enquanto resolvemos") **no começo** do trabalho — ela não reconstrói marcos que aconteceram antes de estar ativa, embora use o que já estiver na conversa.

---

## Formatos

| Formato | Para | Seções |
|---|---|---|
| **STAR** | Entrevistas, avaliações de desempenho, apresentações | Situação, Tarefa, Ação, Resultado |
| **Resumo Técnico** | PRs, commits, changelogs | Problema, Solução, Impacto |
| **Decisão Técnica** (ADR simplificado) | Escolha entre abordagens | Contexto, Decisão, Alternativas, Consequências |

A skill escolhe o formato pelo contexto, ou pergunta. Uma sessão pode render mais de um — uma caça a bug dá um bom STAR e uma boa descrição de PR.

---

## Instalação

### Com o apm (recomendado)

O [apm](https://github.com/microsoft/apm), o Agent Package Manager, instala e atualiza a skill sem você copiar pasta nenhuma. Este repositório é um pacote apm: `apm.yml` na raiz e a skill em `.apm/skills/`.

```bash
# instale o apm, se ainda não tiver
brew install apm                        # macOS
curl -sSL https://aka.ms/apm-unix | sh  # Linux, ou macOS sem Homebrew
irm https://aka.ms/apm-windows | iex    # Windows, no PowerShell

# depois, na pasta do projeto
apm install martinssluis/star-report-skill
```

Para escolher a pasta do agente:

```bash
apm install martinssluis/star-report-skill --target claude
apm install martinssluis/star-report-skill --target copilot
apm install martinssluis/star-report-skill --target all
```

**Atualizar:** `apm install --update`. **Remover:** `apm uninstall star-report-skill`. Para fixar uma versão: `martinssluis/star-report-skill#v2.0.0`.

### Copiando a pasta

| Agente | Pasta do projeto | Pasta pessoal |
|---|---|---|
| Claude Code | `.claude/skills/` | `~/.claude/skills/` |
| Copilot | `.github/skills/` | conforme a documentação |
| Demais agentes (Codex, Cursor…) | `.agents/skills/` | conforme a documentação |

```bash
git clone https://github.com/martinssluis/star-report-skill.git
mkdir -p .claude/skills
cp -R star-report-skill/.apm/skills/delivery-report .claude/skills/
```

### Claude.ai

Compacte a pasta `delivery-report` em `.zip` (ou baixe o `delivery-report.skill` das releases) e envie em **Configurações → Capacidades → Skills**.

---

## Uso

**Ao vivo**, no começo do trabalho:

```
/delivery-report
```

ou em linguagem natural: *"vamos resolver esse timeout e documentar enquanto isso"*, *"registra essa investigação para virar um STAR"*.

**Retrospectivo:** *"semana passada adicionei seleção múltipla no campo de etiquetas, escreve isso para minha avaliação"*, *"transforma essa correção numa descrição de PR"*.

A skill responde no idioma em que você escreve (português ou inglês).

---

## Princípios

1. **Não inventa.** Número ou causa sem fonte vira `[a confirmar]`.
2. **Hipótese é marcada.** O que é leitura do agente aparece identificado.
3. **Previsão não é resultado.** "Deve economizar 20 h/mês" entra como impacto esperado, com um **Para fortalecer** dizendo o que medir.
4. **Evidência, não relato.** No modo ao vivo, cada entrada do registro tem a fonte: saída observada, o que você disse ou hipótese.
5. **Hipóteses descartadas ficam.** "O que não funcionou" costuma ser a parte mais convincente de uma resposta de entrevista.
6. **Informação interna pode ficar fora.** Para entrevistas ou uso público, a skill oferece uma versão sem nomes de sistemas internos, clientes ou números confidenciais.

---

## Estrutura do repositório

```
star-report-skill/
├── apm.yml
├── README.md / README.pt-BR.md
└── .apm/skills/delivery-report/
    ├── SKILL.md                 # fluxo e regras (lido pelo agente)
    ├── README.md / README.pt-BR.md
    ├── references/
    │   ├── formats.md           # os três formatos, com exemplos
    │   ├── live-mode.md         # como acompanhar a sessão em tempo real
    │   └── interview.md         # perguntas para lacunas, métricas, sinais de alerta
    └── templates/
        └── session-log.md       # o arquivo de trabalho do modo ao vivo
```

Os arquivos lidos pelo agente (`SKILL.md`, `references/`, `templates/`) ficam em inglês, que é o que os modelos seguem com mais consistência. O relatório sai no idioma do usuário.

## Contribuindo

Issues e PRs são bem-vindos. Ao mudar a skill, mantenha o `name` do `SKILL.md` igual ao nome da pasta, suba a `version` do `apm.yml` e atualize os dois READMEs.

Estrutura inspirada no [skills-protagonista](https://github.com/dudscode/skills-protagonista).

por [@martinssluis](https://github.com/martinssluis)
