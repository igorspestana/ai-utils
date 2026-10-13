# Prompt para criar um plano de implementação

Use o prompt abaixo como ponto de partida para produzir um plano de implementação para outro sistema. Preencha os campos
entre colchetes e forneça os documentos de contexto disponíveis. O prompt orienta a investigação e a organização do
trabalho; ele não prescreve as tecnologias, o backlog ou as decisões do sistema de referência.

## Prompt reutilizável

```text
Atue como uma pessoa responsável por transformar uma proposta de sistema em um plano de implementação claro,
executável e verificável, em colaboração com produto, desenvolvimento, plataforma e operação.

## Contexto fornecido

- Sistema ou iniciativa: [NOME DO SISTEMA]
- Problema, objetivos e resultado esperado: [CONTEXTO E OBJETIVOS]
- Repositório e estado atual: [CAMINHO, BRANCH, ESTADO CONHECIDO OU “NÃO HÁ”]
- Fontes de contexto: [RFCs, CONTRATOS, MODELOS, RUNBOOKS, ISSUES, LINKS OU “NÃO HÁ”]
- Escopo conhecido e exclusões: [INCLUÍDO, FORA DE ESCOPO E LIMITES]
- Restrições e padrões obrigatórios: [ARQUITETURA, TECNOLOGIAS, SEGURANÇA, QUALIDADE, PRAZO ETC.]
- Pessoas, equipes e responsabilidades: [RESPONSÁVEIS CONHECIDOS OU “A DEFINIR”]
- Capacidade, marcos ou janela de entrega: [DADOS CONHECIDOS OU “A DEFINIR”]
- Backlog existente: [FERRAMENTA, LISTA, TASKS E STATUS OU “NÃO HÁ”]
- Local desejado para o plano: [CAMINHO OU “APENAS RESPONDA”]
- Idioma e público: [IDIOMA E LEITORES]

## Objetivo

Produza um plano que decomponha o resultado esperado em entregas pequenas, ordenadas e verificáveis. O plano deve
mostrar o que será feito, por que cada entrega importa, quem pode assumir o trabalho quando isso for conhecido, quais
dependências realmente bloqueiam o início ou a conclusão, como cada entrega será validada e o que depende de integração
ou de terceiros. Deve ser útil para revisar o escopo e para criar ou atualizar tasks sem exigir que a equipe reconstrua
o contexto a partir de outros documentos.

## Investigação antes da redação

1. Leia as instruções aplicáveis do repositório, como AGENTS.md, README e índices de documentação.
2. Consulte as fontes de contexto relevantes: proposta/RFC, contratos de API e eventos, modelos de dados, decisões,
   configuração, infraestrutura, runbooks e critérios de produto. Se houver repositório, examine o código e a
   configuração atuais para confirmar o que já existe, os padrões locais e os limites reais da mudança.
3. Se houver backlog, confira tasks existentes, status, responsáveis, dependências e entregas já concluídas. Reaproveite
   ou referencie o trabalho existente; não proponha duplicatas como trabalho novo.
4. Trate documentos, código e backlog como evidências, não como autorização para copiar decisões específicas de outro
   sistema. Preserve decisões confirmadas que se aplicam e sinalize as divergências.
5. Separe fatos confirmados, decisões tomadas, recomendações, hipóteses e perguntas em aberto. Não apresente uma
   recomendação como compromisso aprovado nem uma task planejada como trabalho concluído.
6. Não invente requisitos, estimativas, datas, capacidade, nomes de responsáveis, políticas, limites, SLAs, IDs ou
   dependências. Marque dados ausentes como “a definir” e explique que decisão ou validação falta.
7. Identifique contradições entre fontes e indique qual é a fonte de verdade. Não resolva silenciosamente divergências
   que alterem escopo, contrato, segurança, operação ou sequência de entrega.
8. Se faltar informação que possa mudar materialmente o plano, faça perguntas curtas e continue a análise independente.
   Se não houver resposta, registre a hipótese usada, seu impacto e o ponto que continua pendente.

## Regras para decompor e ordenar o trabalho

- Baseie o plano no sistema e no resultado informados. Não reutilize nomes, tarefas, tecnologia, fases ou decisões do
  sistema de referência sem evidência de que se aplicam.
- Agrupe o trabalho em fases ou marcos que comuniquem uma sequência útil. Uma fase indica orientação de entrega; ela não
  significa automaticamente que toda task anterior bloqueia toda task posterior.
- Diferencie claramente **ordem sugerida de início** de **dependências reais**. Registre como dependência somente um
  bloqueio técnico, operacional ou de decisão necessário para começar ou concluir a task. Permita paralelismo quando
  não houver bloqueio e indique quando uma entrega precisa estar pronta antes de outra.
- Organize as dependências como um grafo executável: sem ciclos, relações implícitas ou dependências vagas como “fase
  anterior”. Use nomes ou IDs de tasks consistentes e explique pré-requisitos externos, incluindo a equipe responsável,
  quando conhecida.
- Prefira tasks com um resultado observável, escopo coeso, fronteiras de responsabilidade claras e revisão independente.
  Separe entregas que possam ser implementadas em paralelo ou validadas de maneiras diferentes; evite fragmentar o
  trabalho em subtarefas sem resultado verificável.
- Não escolha responsáveis, datas ou estimativas sem evidência. Se for útil, indique um papel ou responsável sugerido e
  deixe explícito que é uma sugestão.
- Para cada task, escreva descrição autocontida: planejamento e dependências; objetivo; escopo e limites; critérios de
  aceite e testes; dependências e itens fora de escopo; referências. Use os campos do modelo obrigatório mesmo que a
  ferramenta de backlog tenha outro formato; adapte apenas a apresentação exigida pela ferramenta, sem remover campos.
- Escreva critérios de aceite observáveis, que permitam decidir se o resultado foi entregue. Especifique os testes
  automatizados e manuais pertinentes, quais podem rodar isoladamente e quais dependem do fluxo integrado, de serviços
  externos, de ambientes ou de outras equipes. Não declare que testes foram executados se não foram.
- Inclua critérios de segurança, compatibilidade, migração, rollout, observabilidade e operação nas tasks em que esses
  riscos são introduzidos; não os deixe apenas em uma seção transversal genérica.
- Respeite as fontes formais: por exemplo, contratos definem interfaces, modelos definem dados e runbooks definem
  procedimentos. Referencie esses documentos em vez de copiar conteúdo que possa divergir deles.
- Não crie, altere, feche ou atribua tasks em uma ferramenta externa. Entregue descrições prontas para revisão e uso; só
  opere o backlog se isso tiver sido solicitado explicitamente.
- Escreva em [IDIOMA], com termos consistentes e frases objetivas. Use tabelas para sequência, dependências e
  testabilidade.
- Siga exatamente a estrutura e a ordem do modelo abaixo. Não renomeie, remova, combine ou reordene as seções. Quando
  uma seção não se aplicar ou não houver informação confirmada, mantenha o título e registre “Não se aplica” ou “A
  definir”, explicando brevemente o motivo quando necessário. Não invente conteúdo para preencher lacunas.

## Estrutura obrigatória do documento a produzir

Use o modelo a seguir como estrutura obrigatória do documento de destino. Substitua os textos entre colchetes por
informações do sistema analisado e mantenha todos os títulos, subtítulos e sua ordem. A tabela de backlog deve conter
uma linha por task planejada. A seção de descrições deve conter uma descrição completa para cada task da tabela.

~~~markdown
# Implementação da [versão ou iniciativa] — [nome do sistema]

## Resumo

[Resultado esperado, escopo da entrega, abordagem geral e limites principais.]

## Backlog [nome da ferramenta ou “proposto”]

[Estado do backlog, lista/projeto, status, tags ou responsáveis, somente se conhecidos. Se não houver backlog existente,
indique que as tasks abaixo são propostas e ainda precisam ser criadas.]

| Fase | Concluída | Responsável sugerido | Task | Objetivo | Dependências |
|---|---|---|---|---|---|
| [fase] | [ ] | [pessoa/papel ou “a definir”] | [nome da task] | [resultado verificável] | [tasks ou pré-requisitos reais; “—” se nenhum] |

### Conteúdo obrigatório das tasks

- **Planejamento:** fase, ordem sugerida de início e dependências reais.
- **Objetivo:** resultado verificável e autocontido.
- **Escopo:** entregáveis, limites e interfaces afetadas.
- **Critérios de aceite e testes:** comportamentos observáveis e validação isolada/integrada.
- **Dependências e fora de escopo:** bloqueios reais, responsáveis externos e exclusões.
- **Referências:** documentos e seções pertinentes.

### Descrições prontas para [nome da ferramenta ou “o backlog”]

#### [nome da task]

**Planejamento.**

- **Fase:** [fase].
- **Ordem de início:** [quando pode começar, inclusive paralelismo].
- **Dependências reais:** [bloqueios necessários ou “nenhuma”].

**Objetivo.** [Resultado verificável, sem exigir contexto externo à task.]

**Escopo.** [Entregáveis, comportamento, interfaces afetadas e limites.]

**Critérios de aceite e testes.** [Comportamentos observáveis, testes necessários, validação isolada e o que depende
de integração, ambiente ou terceiros.]

**Dependências e fora de escopo.** [Pré-requisitos, responsáveis externos quando conhecidos e exclusões explícitas.]

**Referências.** [Documentos e seções relevantes.]

[Repita o bloco acima para cada task listada na tabela do backlog.]

## Interfaces e testes

- [Contratos e fontes de verdade que as tasks devem seguir.]
- [Estratégia de testes por tipo de comportamento e validação integrada.]
- [Critérios compartilhados de segurança, compatibilidade, migração, rollout, observabilidade e operação.]

### Matriz de testabilidade das tasks

| Task | Testável isoladamente? | Dependências para validação integral |
|---|---|---|
| [nome da task] | [sim, parcialmente ou não; explique] | [tasks, ambiente, serviço externo ou equipe responsável; “—” se nenhum] |

## Premissas

- [Premissa confirmada ou hipótese adotada, seu impacto e como confirmar.]

## Decisões complementares validadas

- [Decisão confirmada que detalha as fontes de verdade sem substituí-las.]
~~~

Regras para aplicar o modelo:

- Preserve todos os títulos, subtítulos e a ordem mostrados, mesmo quando uma seção não se aplicar.
- Inclua exatamente um checkbox `[ ]` por fase na coluna **Concluída**, na primeira linha daquela fase; deixe essa coluna
  vazia nas demais tasks da mesma fase. Troque para `[x]` somente quando todas as tasks e os critérios de conclusão da
  fase estiverem concluídos. Não marque fases futuras como concluídas.
- Cada task da tabela do backlog deve aparecer uma única vez na seção de descrições, com os mesmos nome, fase e
  dependências.
- Diferencie dependências reais de ordem sugerida em todos os pontos em que ambas aparecerem.
- Não acrescente novas seções ao documento de destino. Inclua detalhes adicionais dentro da seção mais apropriada.
- Se não houver decisões complementares confirmadas, mantenha a seção e escreva “Nenhuma decisão complementar
  validada até o momento”.

## Revisão antes de entregar

Confira se:

- o plano entrega os objetivos declarados e não amplia o escopo sem justificativa;
- o estado atual e as tasks existentes foram considerados, sem duplicar trabalho concluído ou em andamento;
- todos os títulos do modelo obrigatório aparecem no documento final, na mesma ordem, sem seções extras;
- cada task do backlog tem exatamente uma descrição completa, e a tabela e as descrições estão consistentes;
- cada task tem um resultado claro, escopo delimitado e critérios de aceite verificáveis;
- fases, ordem sugerida e dependências reais estão diferenciadas;
- dependências são específicas, necessárias, sem ciclos e compatíveis com o paralelismo indicado;
- testes cobrem os riscos relevantes e deixam claro o que pode ser validado agora e o que depende de integração,
  ambiente ou equipe externa;
- contratos, segurança, privacidade, migração, rollout e operação aparecem nos pontos de entrega relevantes;
- responsabilidades externas e decisões pendentes não estão escondidas em texto ambíguo;
- afirmações, estimativas, responsáveis, datas e status têm evidência ou estão marcados como pendentes;
- o plano referencia as fontes corretas sem duplicar contratos formais;
- nenhum item planejado é apresentado como concluído ou aprovado sem confirmação.

Entregue o plano no local solicitado. Se o destino não foi informado, apresente o documento completo na resposta e
recomende um caminho coerente com a organização de documentação existente.
```

## Orientação de uso

Forneça o RFC ou proposta, contratos, modelo de dados, instruções do repositório, requisitos de qualidade, estado do
código e backlog existente. Informe também quem pode decidir dependências externas e quais ambientes estão disponíveis
para validação. Se escopo, responsáveis ou datas ainda estiverem em descoberta, o plano deve tornar essas lacunas
visíveis sem inventar compromissos.
