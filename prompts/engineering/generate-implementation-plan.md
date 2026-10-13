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
  aceite e testes; dependências e itens fora de escopo; referências. Adapte os títulos se a ferramenta de backlog usar
  outro formato.
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
  testabilidade quando facilitarem a consulta. Omita seções não aplicáveis e explique brevemente a omissão quando ela
  puder gerar dúvida.

## Estrutura do plano

Adapte a estrutura às necessidades do sistema. Não preencha seções com conteúdo genérico.

1. **Título e resumo** — sistema, objetivo da entrega, escopo da versão e resultado esperado.
2. **Fontes de verdade e estado atual** — documentos e código consultados, trabalho existente e decisões relevantes.
3. **Escopo e limites** — entregas incluídas, exclusões explícitas, consumidores, sistemas externos e responsabilidades
   de outras equipes.
4. **Backlog por fase ou marco** — tabela com fase, ordem sugerida de início, responsável/papel se conhecido, task,
   resultado e dependências reais. Marque paralelismo e pré-requisitos externos.
5. **Descrições prontas das tasks** — uma seção por task, contendo:
   - **Planejamento:** fase, ordem sugerida de início e dependências reais;
   - **Objetivo:** resultado de negócio ou técnico que possa ser verificado sem contexto externo à task;
   - **Escopo:** entregáveis, comportamento, interfaces afetadas e limites;
   - **Critérios de aceite e testes:** comportamento observável, cobertura necessária, validação isolada e validação
     integrada ou externa;
   - **Dependências e fora de escopo:** pré-requisitos, responsáveis externos quando conhecidos e itens excluídos;
   - **Referências:** documentos, seções, contratos ou configurações relevantes.
6. **Interfaces e integração** — contratos que várias tasks precisam respeitar, sequência entre componentes, compatibilidade,
   e como validar a integração. Não redefina contratos mantidos por outra fonte.
7. **Estratégia transversal de qualidade e entrega** — critérios compartilhados de teste, segurança, migração,
   observabilidade, deploy, rollout, rollback e prontidão operacional que não sejam específicos de uma única task.
8. **Matriz de testabilidade** — para cada task, indique se pode ser validada isoladamente, quais dependências são
   necessárias para a validação integral e quem fornece essas dependências.
9. **Premissas, decisões pendentes e riscos** — registre somente pontos que afetam escopo, sequência, capacidade,
   segurança, operação ou aceitação; inclua impacto e próximo passo/responsável se conhecido.
10. **Referências e fontes de verdade** — caminhos ou links para documentos usados e a responsabilidade de cada um.

## Revisão antes de entregar

Confira se:

- o plano entrega os objetivos declarados e não amplia o escopo sem justificativa;
- o estado atual e as tasks existentes foram considerados, sem duplicar trabalho concluído ou em andamento;
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
