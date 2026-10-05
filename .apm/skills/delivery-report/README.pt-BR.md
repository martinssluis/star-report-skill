[English](README.md) · **Português**

# Skill `delivery-report`

Uma skill de agente que transforma entregas de software em relatórios estruturados, em prosa — **ao vivo**, enquanto o problema é resolvido, ou **em retrospecto**, a partir de uma descrição informal.

- **STAR** para entrevistas, avaliações e apresentações.
- **Resumo Técnico** para PRs e commits.
- **Decisão Técnica** (ADR simplificado) quando uma abordagem foi escolhida entre outras.

## Instalação

```bash
apm install martinssluis/star-report-skill
```

Ou copie esta pasta para onde o seu agente lê skills (`.claude/skills/` no Claude Code, `.agents/skills/` na maioria dos outros). O [README do repositório](../../../README.pt-BR.md) tem todas as opções.

## Uso

No começo do trabalho, para o modo ao vivo:

```
/delivery-report
```

Ou: *"vamos resolver isso e documentar enquanto isso"*. Para algo já feito: *"escreve como STAR a correção do cache que fiz ontem"*.

No modo ao vivo, a skill pergunta o que está sendo resolvido e onde guardar o registro, e volta para o problema. A cada marco — reproduzido, hipótese testada, causa raiz, decisão, correção, verificado — ela atualiza o registro e acrescenta uma linha à resposta. No fim, faz até 3 perguntas, escreve o relatório e lista o que está **[a confirmar]** e o que medir (**Para fortalecer**).

## O que ela promete não fazer

- **Não inventa números, causas nem datas.** O que não tem fonte vira `[a confirmar]`.
- **Não apresenta previsão como resultado.**
- **Não interrompe o debug** com perguntas do relatório; elas esperam o fechamento.
- **Não mantém nomes internos** num relatório que você vai compartilhar fora da empresa, se você pedir a versão anonimizada.

## Estrutura

```
delivery-report/
├── SKILL.md                 # fluxo e regras
├── references/
│   ├── formats.md           # formatos, voz e exemplos completos
│   ├── live-mode.md         # marcos, atualizações discretas, fechamento
│   └── interview.md         # perguntas para lacunas, métricas candidatas, sinais de alerta
└── templates/
    └── session-log.md       # arquivo de trabalho do modo ao vivo
```
