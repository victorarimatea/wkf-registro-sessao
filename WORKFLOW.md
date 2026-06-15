# WORKFLOW.md — Registro de Sessão de Trabalho

**Versão:** v1.4 — 2026-06-15
**Status:** ativo
**Responsável:** Victor Leonardo Arimatea Queiroz — Diretor de Transformação Digital
**Repositório:** workflow-registro-sessao (W03)

---

## Seção 1 — Identificação

| Campo | Valor |
|---|---|
| Nome do processo | Registro de Sessão de Trabalho |
| ID | W03 |
| Versão | v1.4 |
| Status | ativo |
| Data de criação | 2026-06-02 |
| Responsável | DTD/SETIS/SES-DF |
| Skill associada | Sem skill dedicada — gerado pelo próprio Claude ao final da sessão |
| Repositório de destino | P02 `hub-memoria` (documentos/) |

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

Um relatório de sessão bem-sucedido satisfaz todos os critérios abaixo
(estrutura de três blocos da Seção 6, vigente a partir da v1.3):

**Bloco I — Narrativa:**
- [ ] Frontmatter YAML com campos obrigatórios preenchidos, incluindo
  `convergencia` e `residuo_tolerado`
- [ ] Seção de missão e contexto explicando o estado anterior à sessão
- [ ] Seção narrativa cobrindo as principais decisões e descobertas
- [ ] Tabela de decisões tomadas com contexto e impacto
- [ ] Tabela comparativa do estado antes/depois da sessão
- [ ] Seção de aprendizados com reflexões sobre o processo

**Bloco II — Ciclo de qualidade:**
- [ ] Tabela de operações S04 executadas, apontando para backlogs (sem duplicar)
- [ ] Narrativa do ciclo auditoria → correção (abertura, correções, fechamento)
- [ ] Declaração de convergência explícita (estado + resíduo SEV)

**Bloco III — Handoff:**
- [ ] Bloco de Handoff autocontido como seção final (estado herdado, pendências
  SEV abertas, decisões adiadas, próximo tijolo)

**Transversais:**
- [ ] Linguagem narrativa — não apenas lista de ações
- [ ] Arquivo salvo em `hub-memoria/documentos/` com nomenclatura padrão
- [ ] Referência adicionada no `EXECUCOES.md` do P02

---

## Seção 4 — Etapas do processo

| # | Etapa | Executor | Tipo | Entrada | Saída |
|---|---|---|---|---|---|
| 0 | Identificação da sessão como relevante | Humano ou Claude | Manual | Estado da sessão ao final | Decisão de registrar |
| 1 | Leitura do contexto da sessão | Claude | Manual | Histórico da conversa | Compreensão do que foi feito |
| 2 | Redação do relatório narrativo | Claude | Manual | Contexto da sessão | Documento .md com estrutura obrigatória |
| 2-A | Reconciliação com o ROADMAP | Claude | Manual | Entregáveis da sessão + ROADMAP.md do hub-entrada | Lista de itens a marcar ✅ ou incluir retroativamente |
| 3 | Revisão pelo responsável | Humano | Manual | Rascunho do relatório + lista de itens ROADMAP | Relatório aprovado + itens ROADMAP validados |
| 4 | Depósito no P02 e atualização do ROADMAP | S04 (IA) | Automatizada em sessão autenticada | Relatório aprovado + itens ROADMAP validados | Arquivo em `hub-memoria/documentos/` + ROADMAP.md atualizado |
| 5 | Referência no EXECUCOES.md | S04 (IA) | Automatizada em sessão autenticada | Arquivo depositado | Linha em `hub-memoria/EXECUCOES.md` |


### Etapa 2-B — Identificação de aprendizado consolidado (hub-aprendizagem)

| Campo | Valor |
|---|---|
| Executor | Claude |
| Tipo | Semi-automático |
| Entrada | Histórico completo da sessão |
| Saída | Rascunho de aprendizado na Seção E da staging.md (se aprovado) |
| Critério de conclusão | Varredura realizada; resultado declarado no relatório |

**Quando executar:** após a Etapa 2-A, antes do relatório final.
Obrigatória em sessões com diagnóstico, decisão arquitetural ou mudança
estrutural. Pode ser omitida em sessões operacionais rotineiras sem
conteúdo substantivo além das alterações em si.

**Como executar:** aplicar os critérios de elegibilidade da Etapa 6-A
da S04 (sub-seção "Segundo tipo de candidato — Conhecimento consolidado").
Se elegível, apresentar ao mantenedor, aguardar aprovação, redigir
imediatamente com contexto fresco e depositar na Seção E da staging.md.

**Resultado no relatório:**
- `"Aprendizado consolidado: nenhum identificado"` — ou —
- `"Aprendizado consolidado: [título] → depositado na Seção E da staging.md"`

### Detalhamento da Etapa 2-A — Reconciliação com o ROADMAP

Antes de redigir o relatório final, o Claude deve:

1. Ler o `ROADMAP.md` do `hub-entrada` (via web_fetch ou com token ativo)
2. Para cada entregável produzido na sessão (repositório criado, skill atualizada,
   workflow alterado, documento gerado), verificar se ele aparece no ROADMAP:
   - **Estava previsto:** preparar marcação ✅ com data de conclusão
   - **Não estava previsto:** preparar inclusão na seção ✅ Concluído, já marcado
     como concluído com data — nunca omitir
3. Consolidar a lista de alterações necessárias no ROADMAP e incluir na seção
   "Estado antes/depois" do relatório narrativo
4. Submeter ao mantenedor junto com o rascunho do relatório (Etapa 3)

**Regra:** toda implementação real deve aparecer no ROADMAP. O planejamento prévio
não é condição para o registro — o registro é o que torna o histórico confiável.

---

## Seção 5 — Skills e subprocessos consumidos

| Recurso | Tipo | Papel | Link |
|---|---|---|---|
| skill-github-orquestracao | S04 | Depósito no P02 e atualização do EXECUCOES.md | [→](https://github.com/victorarimatea/skill-github-orquestracao) |
| hub-memoria | P02 | Repositório de destino | privado |

---

## Seção 6 — Estrutura obrigatória do relatório de sessão

A partir da v1.3, o relatório de sessão é organizado em **três blocos** com
funções distintas. O relatório não foi reinventado — foi formalizado: o melhor
relatório existente (SESSAO-2026-06-07) já fazia intuitivamente quase tudo isto;
esta estrutura torna obrigatório o que antes era improvisado.

**Princípio organizador:** o registro olha para **duas direções** ao mesmo tempo
— para trás (o que esta sessão resolveu) e para frente (o bastão entregue). São
o mesmo estado do ecossistema visto de dois lados, e por isso vivem no mesmo
documento.

---

### BLOCO I — Narrativa (a história da sessão)

**1. Frontmatter YAML**
```yaml
id_registro: SESSAO-AAAA-MM-DD-[descricao-slug]
tipo: Relatório de Sessão de Trabalho
projeto: P02 — hub-memoria
data_sessao: AAAA-MM-DD
data_registro: AAAA-MM-DD
ferramenta: Claude (Anthropic) — claude.ai
participantes: [nome, cargo]
duracao_estimada: [estimativa]
status: Completo / Parcial
convergencia: atingida | nao-atingida
residuo_tolerado: [lista de SEV3/SEV4 carregados via Handoff, ou "nenhum"]
```

Os dois campos finais — `convergencia` e `residuo_tolerado` — são obrigatórios
a partir da v1.3. Eles ancoram a declaração de convergência na escala SEV já
existente (zero SEV1/SEV2 = convergência atingida), sem criar uma segunda
taxonomia. Resíduo vazio equivale ao que se chamaria "convergência plena";
resíduo com SEV3/SEV4 equivale a "convergência operacional" — mas o leitor vê
o resíduo concreto em vez de decodificar um adjetivo. O `residuo_tolerado` é,
ainda, exatamente a matéria-prima do Bloco de Handoff (item 10): um alimenta
o outro sem retrabalho.

**2. Missão e contexto da sessão** — estado anterior, o que motivou a sessão

**3. Narrativa principal** — o que foi feito, como, por que

**4. Decisões tomadas** — tabela com decisão, contexto e impacto

**5. Estado antes/depois** — tabela comparativa de dimensões relevantes

**6. Aprendizados** — reflexões sobre o processo, erros, descobertas

---

### BLOCO II — Ciclo de qualidade (o que olha para trás)

Este bloco formaliza o que o relatório de 2026-06-07 improvisou. Responde à
pergunta "por que esta sessão existiu e como ela fechou".

**7. Operações executadas (S04)** — tabela das escritas realizadas, *apontando*
para os backlogs e changelogs onde o detalhe vive, **sem duplicar** o conteúdo
deles. Colunas mínimas: repositório, arquivo, operação.

**8. Ciclo de auditoria → correção** — registro narrativo do ciclo: auditoria de
abertura (handoff herdado), correções aplicadas, auditoria de fechamento,
iterações até convergir. É a narrativa de conformidade — distinta da narrativa
de missão do Bloco I.

**9. Declaração de convergência** — explícita: estado (`atingida` /
`nao-atingida`) + resíduo SEV tolerado. É o carimbo que autoriza o encerramento.
Uma sessão que encerra sem convergir (restou um SEV1/SEV2) recebe
`nao-atingida`, com a pendência aberta no Handoff como **dívida prioritária** —
tornando inescapável a primeira ação da sessão seguinte. Um sistema que só
registra sucesso mente por omissão.

---

### BLOCO III — Handoff (o que olha para frente)

**10. Bloco de Handoff para a próxima sessão** — autocontido, é a seção **final**
do relatório. Lido diretamente do hub-memoria via API pela abertura da sessão
seguinte (protocolo W06, Etapa 2). Conteúdo obrigatório:
- **Estado herdado** — convergência da sessão que encerra
- **Pendências SEV abertas** (resíduo tolerado SEV3/SEV4, ou SEV1/SEV2 como
  dívida prioritária se a sessão não convergiu)
- **Decisões adiadas** — questões de design deixadas para sessão futura
- **Próximo tijolo concreto** — a próxima ação prevista, do ROADMAP

**Diagnóstico causal das pendências (C8):**
Para cada item no Handoff listado como pendente ou como dívida prioritária,
incluir não apenas *o que* ficou aberto, mas *por que* ficou — qual foi a causa
que impediu a conclusão nesta sessão (falta de token, tempo, dependência externa,
decisão adiada). O diagnóstico causal permite que a sessão seguinte chegue já
orientada, não apenas informada. Sem o "por quê", o Handoff informa; com o "por quê",
o Handoff orienta.



---

### Distinção entre Bloco II e Bloco III

O Bloco II **olha para trás** (o que se resolveu nesta sessão); o Bloco III
**olha para frente** (o bastão entregue à próxima). Mesmo estado, duas direções,
mesmo documento.

### Momento de registro

O relatório é explicitamente o **último ato da sessão**, depositado *após* a
auditoria de fechamento (W05) confirmar a convergência. Ordem canônica:

> trabalho → auditoria de fechamento (chat separado, sem token) → correções se
> necessário → reauditoria até convergir → redação e depósito do relatório
> (já com handoff) → revogação do token

O relatório não pode ser escrito antes da convergência, porque uma de suas
seções (item 9) *é* a declaração de convergência.

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

## Seção 9 — Histórico de versões

| Versão | Data | Tipo | Descrição |
|---|---|---|---|
| v1.4 | 2026-06-15 | Melhoria | Bloco III do relatório recebe instrução de diagnóstico causal (C8): handoff declara não apenas o que ficou pendente, mas por que ficou — orientando a sessão seguinte |
| v1.3 | 2026-06-12 | Melhoria | Estrutura de três blocos formalizada (Bloco I Narrativa, Bloco II Ciclo de qualidade, Bloco III Handoff); campos `convergencia` e `residuo_tolerado` adicionados ao frontmatter |
| v1.2 | 2026-06-07 | Melhoria | Etapa 2-A (reconciliação com ROADMAP) e Etapa 2-B (conhecimento consolidado) adicionadas |
| v1.1 | 2026-06-04 | Melhoria | Ajustes menores de estrutura e critério de acionamento |
| v1.0 | 2026-06-02 | Criação | Processo inaugural de registro narrativo de sessões de trabalho |

## Seção 8 — Referências e dependências

- M01 `hub-fonte` — convenções de nomenclatura
- S04 `skill-github-orquestracao` — depósito no ecossistema
- P02 `hub-memoria` — repositório de destino
- W02 `workflow-registro-reuniao` — workflow irmão (reuniões vs sessões)
