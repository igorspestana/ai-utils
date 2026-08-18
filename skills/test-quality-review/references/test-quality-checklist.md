# Checklist de Qualidade de Testes

## Princípio central
Um bom teste não é aquele que passa quando a implementação está correta. É aquele que falha quando a implementação está errada.

## Critérios obrigatórios

### O teste precisa conseguir falhar
- Perguntar qual implementação claramente errada continuaria passando.
- Marcar como achado quando o teste só executa o código, mas não valida resultado ou efeito observável.
- Considerar alto risco quando uma implementação que retorna constante, ignora entrada, remove condição ou troca operador continuaria verde.

### Testar comportamento, não implementação
- Preferir validação de resultado, estado persistido, efeito público, evento emitido, erro contratado ou saída observável.
- Evitar achado quando uma chamada interna faz parte do contrato explícito, como integração com gateway, métrica obrigatória ou auditoria.
- Marcar como fraco quando o teste depende de nome de variável, estrutura interna, quantidade de chamadas internas ou detalhes que poderiam mudar sem quebrar o requisito.

### Cada assertion precisa validar algo relevante
Marcar assertions inúteis ou insuficientes, incluindo:
- `expect(true).toBe(true)`.
- Comparar uma variável com ela mesma.
- Verificar apenas que não lançou erro, quando o requisito exige saída, estado ou erro específico.
- Verificar apenas `toBeDefined`, `not.toBeNull` ou existência genérica quando o requisito exige valor específico.
- Snapshot amplo sem invariantes importantes, quando o snapshot aprova ruído e não evidencia o comportamento.

### Verificar o resultado correto, não apenas algum resultado
- Se a especificação exige valor exato, validar valor exato.
- Se exige estrutura, validar campos semanticamente relevantes.
- Se exige transformação, validar entrada e saída com exemplos capazes de revelar erro de lógica.

### Cobrir caminho feliz
- Exigir pelo menos um teste do comportamento principal com dados representativos.
- Verificar se o teste demonstra o requisito central do PR, não apenas inicialização, renderização superficial ou chamada sem exception.

### Cobrir casos de borda relevantes
Selecionar conforme o domínio da mudança:
- vazio;
- zero;
- negativos;
- máximos e mínimos;
- um único elemento;
- duplicados;
- strings vazias;
- `null` ou `undefined`;
- limites de intervalo;
- datas em fronteiras;
- timezone;
- ordenação;
- concorrência ou idempotência;
- permissões ou papéis diferentes.

### Cobrir entradas inválidas quando fizer parte do contrato
- Verificar rejeição, erro, fallback ou validação prometida.
- Confirmar mensagem, tipo de erro ou status quando isso fizer parte do contrato.
- Não exigir teste de entrada inválida se o contrato explicitamente delega essa garantia a outra camada já testada.

## Heurísticas de mutação
Imaginar mutações pequenas e perguntar se os testes falhariam:
- trocar `>` por `>=`, `<` por `<=` ou `==` por `!=`;
- trocar `+` por `-`, multiplicar por fator errado ou arredondar incorretamente;
- remover uma condição;
- retornar sempre o mesmo valor;
- ignorar primeiro ou último elemento;
- inverter `true` e `false`;
- trocar `and` por `or`;
- remover tratamento de erro;
- ignorar campo relevante;
- aceitar entrada inválida;
- mockar retorno feliz independente da entrada.

Se uma mutação plausível não seria detectada por nenhum teste, reportar a lacuna ligada ao requisito afetado.

## Antipadrões

### Testes excessivamente permissivos
- Aceitar vários resultados quando só um é correto.
- Usar regex ampla demais.
- Comparar apenas parte do objeto e ignorar campos relevantes.
- Usar `arrayContaining` ou `objectContaining` quando a completude importa.
- Normalizar ou filtrar o resultado no próprio teste de modo que esconda o bug.

### Mocks que removem o que deveria ser testado
- Mockar a própria lógica sob validação.
- Mockar camada demais e só testar que mocks foram chamados.
- Fazer o mock retornar exatamente o que a implementação deveria calcular.
- Não exercitar integração relevante quando o contrato do PR é justamente integrar componentes.

### Setup desconectado da assertion
- Montar cenário complexo e depois validar algo que independe desse cenário.
- Criar fixtures com campos importantes, mas não verificar nenhum efeito desses campos.
- Reutilizar fixture genérica que torna impossível saber qual requisito está sendo provado.

### Testes não determinísticos ou dependentes
- Depender de tempo real sem congelar relógio.
- Depender de aleatoriedade sem seed/controlador.
- Depender de rede, ordem instável, timezone local ou estado compartilhado.
- Passar ou falhar dependendo da ordem de execução de outros testes.

## Mapeamento requisito -> teste
Para cada comportamento relevante do PR, tentar preencher:
- Requisito ou comportamento esperado.
- Arquivo e teste que valida esse comportamento.
- Entrada ou cenário preparado.
- Assertion que observa o resultado.
- Mutação errada que o teste detectaria.

Se algum item essencial não puder ser preenchido, considerar achado ou limitação explícita.

## Severidade sugerida
- Alta: teste verde permitiria bug crítico, regressão de regra de negócio, falha de segurança, perda de dados, permissão indevida ou erro financeiro.
- Média: teste não cobre comportamento principal, edge case provável, entrada inválida contratada ou mutação simples do código alterado.
- Baixa: assertion fraca, excesso de acoplamento à implementação, legibilidade que dificulta manutenção ou lacuna em cenário menos provável.
