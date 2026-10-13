# Prompt para criar um RFC de arquitetura

Use o prompt abaixo como ponto de partida para produzir um RFC de arquitetura para outro sistema. Preencha os campos
entre colchetes e forneça os documentos de contexto disponíveis. O prompt orienta a investigação e a redação; ele não
prescreve as tecnologias nem as decisões do sistema de referência.

## Prompt reutilizável

```text
Atue como arquiteto(a) de software e engenheiro(a) responsável por produzir um RFC de arquitetura claro, verificável e
útil para implementação e operação.

## Contexto fornecido

- Sistema ou iniciativa: [NOME DO SISTEMA]
- Problema ou oportunidade: [DESCRIÇÃO DO PROBLEMA]
- Objetivos de negócio e técnicos: [OBJETIVOS]
- Usuários, consumidores e sistemas envolvidos: [ATORES E INTEGRAÇÕES]
- Escopo conhecido: [INCLUÍDO E EXCLUÍDO, SE CONHECIDO]
- Restrições e padrões obrigatórios: [TECNOLOGIAS, PLATAFORMA, SEGURANÇA, PRAZO, CUSTO ETC.]
- Decisões já tomadas: [DECISÕES CONFIRMADAS]
- Repositório e documentação disponíveis: [CAMINHOS, LINKS OU “NÃO HÁ”]
- Local desejado para o RFC: [CAMINHO OU “APENAS RESPONDA”]
- Idioma e público: [IDIOMA E LEITORES]

## Objetivo

Produza um RFC de proposta de arquitetura que explique por que o sistema é necessário, quais responsabilidades terá,
como as partes se integram, quais decisões precisam ser tomadas e como a solução pode ser implementada, protegida,
operada e entregue em etapas. O documento deve permitir que equipes de produto, desenvolvimento, plataforma e operação
entendam a proposta e identifiquem decisões pendentes antes da implementação.

## Investigação antes da redação

1. Leia as instruções aplicáveis do repositório, como AGENTS.md, README e índices de documentação.
2. Consulte os documentos de arquitetura, contratos, modelos de dados, planos, configuração e infraestrutura relevantes.
   Se houver repositório, examine também o código existente que ajude a confirmar padrões e limites reais.
3. Trate a documentação e o código como fontes de evidência, não como autorização para copiar decisões que pertencem a
   outro sistema. Reutilize padrões existentes quando forem aplicáveis e explique qualquer desvio relevante.
4. Separe fatos confirmados, decisões existentes, hipóteses, recomendações e perguntas em aberto. Não apresente uma
   hipótese como fato.
5. Não invente requisitos, números, políticas, garantias de fornecedores, nomes de serviços, URLs, preços, limites,
   SLAs ou práticas operacionais. Se um dado depender de confirmação, marque-o como pendente e indique como verificá-lo.
   Se houver acesso à web e a decisão depender de informação atual de fornecedor, padrão ou preço, verifique em fonte
   primária e registre a fonte e a data de consulta.
6. Identifique contradições entre fontes e indique qual fonte de verdade deve prevalecer. Não resolva silenciosamente
   uma divergência que possa mudar a arquitetura.
7. Se faltar informação que possa alterar materialmente a proposta, faça perguntas curtas antes de fechar a decisão.
   Continue a análise independente. Se não for possível obter resposta, registre a hipótese adotada, o impacto e a
   alternativa que fica em aberto.

## Regras para a proposta

- Baseie o documento no sistema informado. Não copie nomes, domínios, fluxos ou decisões específicas de outro RFC.
- Comece com uma decisão central resumida em linguagem direta e explique o estado da proposta, data, escopo, envolvidos
  e identificadores relevantes do sistema quando esses dados forem conhecidos.
- Explique o problema e os resultados esperados antes de descrever componentes e tecnologias.
- Defina o que pertence ao sistema, o que pertence aos consumidores e o que fica fora do escopo. Explicite limites de
  domínio, propriedade dos dados e responsabilidades de autorização.
- Para cada decisão arquitetural importante, registre a escolha, os motivos, os custos ou limitações e as condições que
  justificariam reavaliá-la. Inclua alternativas reais, não opções caricaturais.
- Mostre os fluxos principais em diagramas Mermaid ou blocos de sequência/texto legíveis. Inclua caminhos de sucesso,
  falha, retry e recuperação quando forem relevantes.
- Use exemplos concretos para contratos e mensagens, mas identifique-os como ilustrativos se ainda não forem um
  contrato formal. Inclua validação, erros, compatibilidade, idempotência, ordenação e versionamento quando aplicáveis.
- Descreva persistência, estados e transições se o sistema mantiver dados ou trabalho de longa duração. Inclua
  consistência, concorrência, retenção, exclusão, migrações e recuperação de falha conforme o contexto.
- Explique autenticação, autorização, gestão de segredos, privacidade, limites de uso e riscos de abuso. Não inclua
  segredos nem dados pessoais reais.
- Cubra logs, métricas, traces, dashboards e alertas de forma que a operação consiga detectar falhas e responder a elas.
- Descreva configuração, dependências e responsabilidades de deploy por ambiente. Não fixe valores de produção sem
  evidência; prefira indicar configuração e critérios para escolher valores.
- Defina testes e critérios de pronto observáveis, ligados aos riscos e fluxos descritos no RFC.
- Planeje rollout, compatibilidade entre versões, migração de dados e reversão ou mitigação quando aplicável.
- Use a documentação existente como mapa de fontes de verdade. Indique quais documentos complementares devem definir
  detalhes que não pertencem ao RFC, como OpenAPI, esquema de eventos, modelo de dados ou runbooks.
- Escreva em [IDIOMA], com termos consistentes, frases objetivas e tabelas apenas quando facilitarem comparação ou
  consulta. Evite texto promocional e recomendações sem justificativa.
- Não declare que implementação, validação ou teste ocorreu se isso não foi realizado.

## Estrutura do RFC

Adapte os títulos ao sistema e remova ou combine seções que não se aplicarem. Quando uma seção importante não for
aplicável, explique brevemente o motivo em vez de preencher com conteúdo genérico.

1. **Título e metadados** — nome, status, data, escopo, consumidores ou usuários, repositório/artefato/ambiente quando
   conhecidos.
2. **Decisão central** — recomendação em poucas linhas, principais componentes e fluxo de alto nível; marque decisões
   pendentes.
3. **Conteúdo** — índice numerado das seções.
4. **Contexto e problema** — situação atual, motivação, impacto, objetivos, não objetivos e critérios de sucesso.
5. **Responsabilidades e fronteiras** — responsabilidades do sistema, consumidores, dependências e itens fora do
   escopo.
6. **Arquitetura proposta** — diagrama, componentes, fluxos principais, fronteiras de confiança e modos de falha.
7. **Contratos e integração** — APIs, eventos, mensagens, SDKs ou interfaces relevantes; exemplos, validação, erros,
   autenticação, idempotência, versionamento e compatibilidade conforme aplicável.
8. **Integração dos consumidores ou usuários** — sequência de uso, responsabilidades de cada lado, experiência esperada
   e comportamento em falhas.
9. **Processamento assíncrono e filas** — inclua somente se necessário; aborde entrega, duplicidade, ordenação,
   retries, backoff, DLQ, outbox, concorrência e reprocessamento conforme o desenho escolhido.
10. **Persistência, dados e estados** — propriedade, modelo conceitual, ciclo de vida, transições, consistência,
    idempotência, retenção, migração e recuperação.
11. **Integrações externas** — responsabilidades dos adapters, timeouts, limites, custos, disponibilidade, retries,
    tratamento de falhas e dependência de fornecedor.
12. **Autenticação e autorização** — identidades, credenciais, escopos, rotação, isolamento entre consumidores e
    evolução prevista.
13. **Segurança, privacidade e limites** — dados sensíveis, ameaça relevante, validação, abuso, quotas, proteção de
    segredos e controles necessários.
14. **Observabilidade e operação** — logs seguros, métricas, tracing, painéis, alertas, runbooks e sinais de saúde.
15. **Estrutura de projeto** — organização de módulos/pacotes compatível com a arquitetura e os padrões reais do
    repositório; omita se não houver decisão de código a registrar.
16. **Configuração e infraestrutura** — configuração não sensível, secrets, valores por ambiente, permissões e
    responsabilidades de deploy.
17. **Testes e definição de pronto** — testes necessários, cenários críticos e critérios de aceite verificáveis.
18. **Alternativas consideradas** — opções avaliadas, decisão e razões, incluindo quando a escolha poderá mudar.
19. **Riscos e trade-offs** — risco, impacto e mitigação; não repita decisões sem explicitar a consequência.
20. **Plano de rollout** — preparação, implementação, validação, integração inicial, produção e gatilhos para evoluções.
21. **Questões em aberto e hipóteses** — somente as que ainda exigem confirmação, com responsável ou próximo passo se
    conhecido.
22. **Referências e fontes de verdade** — documentos internos, padrões e fontes primárias usados; identifique a data
    de consulta para fatos sujeitos a mudança.

## Revisão antes de entregar

Antes de entregar, confira se:

- a decisão central responde ao problema e é consistente com o restante do documento;
- responsabilidades, fronteiras e dados de propriedade estão claros;
- cada fluxo importante cobre sucesso e falha sem depender de comportamento implícito;
- contratos e estados não se contradizem;
- requisitos de segurança e operação aparecem também nos fluxos, configurações e critérios de pronto relevantes;
- alternativas e trade-offs são específicos da proposta;
- números e afirmações externas têm evidência ou estão marcados como pendentes;
- documentos complementares estão apontados como fontes de verdade, sem duplicar contratos formais;
- o texto distingue fatos, decisões, hipóteses e recomendações;
- o RFC está pronto para revisão pelas equipes envolvidas, sem afirmar que já foi aprovado.

Entregue o RFC no local solicitado. Se o destino não foi informado, apresente o documento completo na resposta e
recomende um caminho de arquivo coerente com a organização de documentação existente.
```

## Orientação de uso

Para obter um resultado específico, forneça ao modelo os documentos do sistema, restrições conhecidas, responsáveis por
decisões e o público do RFC. Se a arquitetura ainda estiver em descoberta, use o RFC para explicitar hipóteses e
alternativas, não para simular decisões já aprovadas.
