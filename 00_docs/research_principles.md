# Princípios de Pesquisa — Market Research Lab

> Estas são as regras científicas invioláveis deste laboratório. Toda análise, experimento e conclusão deve obedecer a estes princípios.

---

## 1. Falsificabilidade em vez de Confirmação

Não desenvolvemos análises para confirmar o que já acreditamos.

Toda hipótese deve ser formulada de maneira **falsificável**: deve ser possível encontrar evidências que a refutem.

Se uma análise só pode confirmar — mas nunca refutar — a hipótese, ela não é científica.

---

## 2. Definição a Priori

Toda hipótese, todos os critérios e todas as métricas de avaliação devem ser **definidos antes** de ver os dados.

**Proibido:**
- Ajustar a hipótese após ver os resultados
- Escolher o período de análise após observar que esse período "funciona"
- Definir "whale" ou "smart money" usando critérios que dependem do resultado

**Obrigatório:**
- Registrar a hipótese e o protocolo antes de iniciar qualquer análise
- Congelar a definição matemática de todos os sinais antes de calcular qualquer resultado

---

## 3. Separação Rigorosa de Dados

Os dados têm três funções distintas e **não intercambiáveis**:

| Conjunto | Finalidade |
|---|---|
| **In-sample / Treino** | Desenvolvimento do modelo, calibração de parâmetros |
| **Validação** | Seleção entre modelos alternativos |
| **Out-of-sample / Teste** | Avaliação final — toque somente uma vez |

O conjunto out-of-sample deve ser reservado até o final. Se for "olhado" antes, torna-se in-sample efetivamente.

---

## 4. Prevenção de Look-ahead Bias

Toda análise deve simular exatamente o que estaria disponível em cada momento do tempo.

**Checklist obrigatório:**
- [ ] O sinal usa somente dados disponíveis em `t-1` para a decisão em `t`?
- [ ] Features calculadas com janelas móveis usam somente o passado?
- [ ] Dados macroeconômicos são o "first release", não os revisados?
- [ ] A normalização foi calculada somente com dados do treino?

---

## 5. Correção para Múltiplos Testes

Testar múltiplas hipóteses, múltiplos ativos, múltiplos períodos e múltiplos parâmetros inflaciona artificialmente a probabilidade de encontrar um resultado significativo por acaso.

**Regras:**
- Documentar **todos** os testes realizados, incluindo os que falharam
- Aplicar correção para múltiplos testes (Bonferroni, FDR/Benjamini-Hochberg) quando necessário
- Desconfiar de qualquer resultado com p-value baixo que surgiu de múltiplas tentativas

> **O p-value de um único teste após testar 100 hipóteses não é p-value — é ruído.**

---

## 6. Robustez é Mais Importante que Precisão

Uma estratégia que funciona somente em um ativo, em uma janela de tempo, com parâmetros precisos, não é robusta.

**Critérios de robustez:**
- O resultado se mantém ao variar os parâmetros em ±20-30% (sensitivity analysis)?
- Funciona em outros ativos similares?
- Funciona em subperíodos diferentes da amostra?
- Sobrevive a testes Monte Carlo com permutação aleatória dos dados?

---

## 7. Registrar Resultados Negativos

Um resultado negativo (hipótese refutada) tem **o mesmo valor científico** que um resultado positivo.

**Obrigatório:**
- Registrar toda hipótese testada em `00_docs/hypotheses.md`
- Registrar resultados negativos com o mesmo rigor que positivos
- Nunca "esconder" testes que falharam

O cemitério de hipóteses refutadas é evidência de pesquisa séria.

---

## 8. Proibição de Cherry-picking

Proibido:
- Selecionar o período que apresenta os melhores resultados
- Selecionar o ativo que apresenta os melhores resultados
- Selecionar os parâmetros que apresentam os melhores resultados
- Apresentar somente os resultados favoráveis

Se o resultado é bom somente em condições específicas, isso deve estar explicitamente documentado como uma limitação, não escondido.

---

## 9. Correlação ≠ Causalidade

Encontrar correlação entre dois fenômenos não implica que um causa o outro.

**Sempre perguntar:**
- Existe uma mecanismo causal plausível?
- Existe uma terceira variável que pode explicar a correlação (confounding)?
- A correlação sobrevive a controles estatísticos adequados?

Jamais usar linguagem causal sem evidência de causalidade.

---

## 10. Definições Quantitativas Obrigatórias

Os termos a seguir só podem ser usados se acompanhados de uma definição quantitativa explícita:

| Termo | O que deve ser definido |
|---|---|
| "Whale" | Limiar de saldo/volume, percentil, período de referência |
| "Smart Money" | Critério de performance, janela histórica, benchmark |
| "Significativo" | p-value, alfa, correção para múltiplos testes |
| "Funciona" | Métrica específica, período, custo de transação incluído |
| "Forte correlação" | Coeficiente, intervalo de confiança, tamanho da amostra |
| "Regime de mercado" | Critério de classificação, variáveis utilizadas |

---

## 11. Custos de Transação e Slippage

Nenhum resultado de backtest é válido sem a consideração de:

- **Spread bid-ask** estimado para o mercado e período
- **Slippage** para execução de ordens a mercado
- **Taxas** da exchange
- **Impacto de preço** para posições grandes

Um edge que desaparece após custos realistas não é um edge.

---

## 12. Significância Estatística é Necessária, mas Não Suficiente

Um resultado estatisticamente significativo (p < 0.05) pode ser:
- Fruto de múltiplos testes (falso positivo)
- Economicamente irrelevante (tamanho de efeito muito pequeno)
- Não-robusto fora do período testado

**Sempre reportar:**
- p-value **e** tamanho do efeito (effect size)
- Intervalo de confiança, não apenas estimativa pontual
- Performance out-of-sample, não apenas in-sample

---

## 13. Documentação Completa é Obrigatória

Todo experimento deve ser documentado no protocolo padrão (`experiment_protocol.md`).

Experimento não documentado = experimento não existente.

---

## Síntese

> Prefira resultados honestos a resultados bonitos.
>
> Um edge pequeno e robusto vale mais que uma estratégia "perfeita" que só funciona no backtest.
>
> Se os dados não suportam a hipótese, abandone a hipótese — não ajuste os dados.

---

*Research Principles v1.0 — Market Research Lab*
