# WORKFLOW.md — Registro de Sessão de Trabalho

**Versão:** v1.0 — 2026-06-02
**Status:** ativo
**Responsável:** Victor Leonardo Arimatea Queiroz — Diretor de Transformação Digital
**Repositório:** workflow-registro-sessao (W03)

---

## Seção 1 — Identificação

| Campo | Valor |
|---|---|
| Nome do processo | Registro de Sessão de Trabalho |
| ID | W03 |
| Versão | v1.0 |
| Status | ativo |
| Data de criação | 2026-06-02 |
| Responsável | DTD/SETIS/SES-DF |
| Skill associada | Sem skill dedicada — gerado pelo próprio Claude ao final da sessão |
| Repositório de destino | P02 `ecossistema-dtd-setis` (documentos/) |

---

## Seção 2 — Missão e contexto organizacional

### Missão

Transformar sessões de trabalho intensivo no Claude em registros narrativos
estruturados que preservem a história da construção do ecossistema — as decisões
de design, os percalços, as visões que emergiram, os erros cometidos e as
soluções encontradas.

### Por que este processo existe

O trabalho de construção do ecossistema acontece em sessões de trabalho no Claude.
Cada sessão pode durar horas, gerar dezenas de decisões e resultar em implementações
que transformam o estado do ecossistema. Sem registro estruturado, essa história
se perde — restam apenas commits no git e changelogs técnicos.

O relatório de sessão é o documento que dá voz humana à história técnica.
Ele não substitui os backlogs e changelogs — os complementa com narrativa,
contexto e reflexão.

### Quem pode acionar este workflow

- O Claude ao final de qualquer sessão que resulte em implementações relevantes
- O Diretor de Transformação Digital ao identificar que uma sessão merece registro
- Futuramente: qualquer colaborador da DTD com acesso ao ecossistema

### Critério de acionamento

Uma sessão merece registro quando:
- Resultou em criação de novo tipo de repositório ou instrumento
- Conteve decisões de design com impacto estrutural
- Resolveu um problema crônico ou identificou causa raiz de drift
- Produziu artefatos com valor histórico para o ecossistema

---

## Seção 3 — Estado final esperado

Um relatório de sessão bem-sucedido satisfaz todos os critérios abaixo:

- [ ] Front Matter YAML com campos obrigatórios preenchidos
- [ ] Seção de contexto explicando o estado anterior à sessão
- [ ] Seção narrativa cobrindo as principais decisões e descobertas
- [ ] Tabela de decisões tomadas com contexto e impacto
- [ ] Tabela comparativa do estado antes/depois da sessão
- [ ] Seção de aprendizados com reflexões sobre o processo
- [ ] Linguagem narrativa — não apenas lista de ações
- [ ] Arquivo salvo em `ecossistema-dtd-setis/documentos/` com nomenclatura padrão
- [ ] Referência adicionada no `EXECUCOES.md` do P02

---

## Seção 4 — Etapas do processo

| # | Etapa | Executor | Tipo | Entrada | Saída |
|---|---|---|---|---|---|
| 0 | Identificação da sessão como relevante | Humano ou Claude | Manual | Estado da sessão ao final | Decisão de registrar |
| 1 | Leitura do contexto da sessão | Claude | Manual | Histórico da conversa | Compreensão do que foi feito |
| 2 | Redação do relatório narrativo | Claude | Manual | Contexto da sessão | Documento .md com estrutura obrigatória |
| 3 | Revisão pelo responsável | Humano | Manual | Rascunho do relatório | Relatório aprovado |
| 4 | Depósito no P02 | S04 (IA) | Automatizada em sessão autenticada | Relatório aprovado | Arquivo em `ecossistema-dtd-setis/documentos/` |
| 5 | Referência no EXECUCOES.md | S04 (IA) | Automatizada em sessão autenticada | Arquivo depositado | Linha em `ecossistema-dtd-setis/EXECUCOES.md` |

---

## Seção 5 — Skills e subprocessos consumidos

| Recurso | Tipo | Papel | Link |
|---|---|---|---|
| skill-github-orquestracao | S04 | Depósito no P02 e atualização do EXECUCOES.md | [→](https://github.com/victorarimatea/skill-github-orquestracao) |
| ecossistema-dtd-setis | P02 | Repositório de destino | privado |

---

## Seção 6 — Estrutura obrigatória do relatório de sessão

Todo relatório de sessão deve conter as seguintes seções:

**1. Frontmatter YAML**
```yaml
id_registro: SESSAO-AAAA-MM-DD-[descricao-slug]
tipo: Relatório de Sessão de Trabalho
projeto: P02 — ecossistema-dtd-setis
data_sessao: AAAA-MM-DD
data_registro: AAAA-MM-DD
ferramenta: Claude (Anthropic) — claude.ai
participantes: [nome, cargo]
duracao_estimada: [estimativa]
status: Completo / Parcial
```

**2. Contexto da sessão** — estado anterior, o que motivou a sessão

**3. Narrativa principal** — o que foi feito, como, por que

**4. Decisões tomadas** — tabela com decisão, contexto e impacto

**5. Estado antes/depois** — tabela comparativa de dimensões relevantes

**6. Aprendizados** — reflexões sobre o processo, erros, descobertas

**Nomenclatura do arquivo:**
`SESSAO-AAAA-MM-DD.md` ou `SESSAO-AAAA-MM-DD-[descricao].md`

---

## Seção 7 — Roadmap de automação

| Etapa | Status atual | Próxima evolução |
|---|---|---|
| Redação do relatório | 🔄 Manual — Claude redige com base no contexto da sessão | Estrutura de prompt padronizada para orientar a redação |
| Depósito no P02 | 🔄 Automático em sessões autenticadas | Idem |
| Referência no EXECUCOES.md | 🔄 Automático em sessões autenticadas | Idem |
| Identificação automática de sessões relevantes | ❌ Manual | Critérios formais no CONTEXTO.md para o Claude identificar autonomamente |

---

## Seção 8 — Referências e dependências

- M01 `ecossistema-sumario` — convenções de nomenclatura
- S04 `skill-github-orquestracao` — depósito no ecossistema
- P02 `ecossistema-dtd-setis` — repositório de destino
- W02 `workflow-registro-reuniao` — workflow irmão (reuniões vs sessões)
