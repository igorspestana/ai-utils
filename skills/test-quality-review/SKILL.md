---
name: test-quality-review
description: Revisa a qualidade dos testes de um PR e produz achados técnicos sobre testes que passam sem validar comportamento real. Use quando o usuário pedir validação de testes, review focado em testes, análise de cobertura efetiva, detecção de assertions inúteis, mocks excessivos, testes permissivos ou garantia de que os testes falhariam com uma implementação errada, sempre a partir de um número ou URL de PR.
---

# Test Quality Review

## Objetivo
Executar um review técnico focado na qualidade real dos testes adicionados ou alterados em um PR, verificando se eles distinguem uma implementação correta de implementações erradas ou quase corretas.

Princípio central: um bom teste não é aquele que passa quando a implementação está correta; é aquele que falha quando a implementação está errada.

## Entrada
- `entenda_o_objetivo_do_pr` (obrigatório; deve ser número ou URL do PR)

## Workflow
1. Ler `entenda_o_objetivo_do_pr` e validar se é número ou URL de PR; se for branch ou outro formato, retornar erro pedindo número/URL.
2. Executar `gh pr view <identificador> --comments --json title,body,files,author,baseRefName,headRefName,labels,reviewRequests,reviews` para obter contexto do PR.
3. Executar `gh pr diff <identificador>` para analisar código e testes no diff real.
4. Se o `gh` falhar por acesso à API ou sandbox, repetir com permissão elevada quando disponível antes de abandonar a análise.
5. Se o `gh` retornar erro de autenticação, interromper imediatamente e informar apenas que o `gh` não está autenticado.
6. Se a consulta ao `gh` falhar por outro motivo, interromper a análise e informar o motivo; não inferir o objetivo do PR sem esse passo.
7. Salvar um resumo enxuto do PR em `agent-artifacts/test-quality-review/<identificador-sanitizado>/gh-pr-summary.md`.
8. Resumir em uma frase o comportamento esperado, usando PR body, título, comentários e diff. Quando a especificação estiver incompleta, declarar a inferência e limitar a confiança dos achados.
9. Ler `references/test-quality-checklist.md` e aplicar somente os critérios relevantes ao tipo de mudança.
10. Mapear requisitos ou comportamentos esperados para os testes existentes: requisito -> cenário testado -> assertion observável.
11. Identificar testes que passariam mesmo com implementação errada, assertion inútil, mock que elimina a lógica testada, setup desconectado da assertion, teste permissivo, teste frágil ou teste que valida implementação em vez de comportamento.
12. Fazer análise mental de mutações pequenas no código alterado e perguntar se os testes do PR detectariam cada mutação relevante.
13. Classificar achados por severidade e registrar evidência objetiva com arquivo, trecho do comportamento e motivo pelo qual o teste não detecta o bug.
14. Se não houver alteração de testes no PR, avaliar se a mudança exigia testes e reportar a lacuna como achado quando houver risco real.
15. Produzir review em PT-BR.

## Regras
- Use `references/test-quality-checklist.md` como checklist canônica.
- Use `gh pr view` e `gh pr diff` como fontes primárias.
- Não aceitar branch como identificador de PR.
- Não inventar requisitos não observáveis; diferenciar fato, inferência e limitação.
- Priorizar achados sobre testes que não conseguem falhar, assertions sem valor, permissividade excessiva, mocks indevidos e ausência de casos essenciais.
- Não usar cobertura de linhas como prova de qualidade dos testes.
- Evitar reclamar de detalhes internos quando o teste valida um contrato observável suficiente.
- Registrar caminhos relativos quando citar arquivos.
- Manter linguagem direta, objetiva e técnica.

## Template do Resumo do GH
Preencher `agent-artifacts/test-quality-review/<identificador-sanitizado>/gh-pr-summary.md` com:

```md
# PR Summary
- Identificador: <numero-ou-url>
- Título: <title>
- Autor: <author>
- Base: <baseRefName>
- Head: <headRefName>
- Labels: <labels>
- Objetivo resumido: <1 frase objetiva>
- Arquivos de teste alterados:
  - <path1>
- Arquivos de produção alterados:
  - <path1>
- Comentários e reviews relevantes:
  - <resumo curto>
```

## Saída esperada
- Resumo do objetivo do PR.
- Avaliação geral da capacidade dos testes de falhar com implementações erradas.
- Lista de achados ordenados por severidade, com evidência e sugestão objetiva.
- Critérios relevantes validados sem problemas.
- Limitações da análise, quando houver especificação insuficiente ou diff parcial.
