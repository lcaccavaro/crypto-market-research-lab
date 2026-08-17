# Protocolo de Experimento — Market Research Lab

> **Todo experimento deve seguir este protocolo. Sem exceções.**
>
> Preencha cada seção antes de iniciar qualquer análise.
> Seções marcadas com ⚠️ são críticas para validade científica.

---

## Template de Protocolo

Copie este template para cada nova hipótese em `05_hypotheses/HXXX_nome/PROTOCOL.md`.

---

```markdown
# [HXXX] — Nome da Hipótese

## Metadados

| Campo | Valor |
|---|---|
| ID | HXXX |
| Data de criação | YYYY-MM-DD |
| Autor | - |
| Status | [ ] Rascunho / [ ] Em andamento / [ ] Concluído / [ ] Arquivado |
| Resultado | [ ] Confirmado / [ ] Refutado / [ ] Inconclusivo |

---

## ⚠️ 1. Hipótese

Enuncie a hipótese de forma clara, falsificável e em uma ou duas frases.

**H₀ (nula):** [O que a hipótese nula afirma — geralmente ausência de efeito]

**H₁ (alternativa):** [O que a hipótese alternativa afirma]

Exemplo:
> H₀: O funding rate de contratos perpétuos de BTC não possui poder preditivo sobre o retorno de BTC nas próximas 24h.
> H₁: Funding rate acima do percentil 95 histórico é seguido por retorno negativo médio estatisticamente significativo nas próximas 24h.

---

## 2. Rationale

Por que faz sentido testar esta hipótese? Qual é o mecanismo econômico ou comportamental que poderia explicá-la?

- Explicação intuitiva:
- Mecanismo proposto:
- Literatura ou referências relevantes:
- Por que pode ser um sinal real (e não ruído)?

---

## ⚠️ 3. Dados Necessários

Liste todos os dados necessários para testar a hipótese.

| Dado | Fonte | Granularidade | Disponibilidade | Custo |
|---|---|---|---|---|
| - | - | - | - | - |

---

## ⚠️ 4. Período de Análise

| Campo | Valor |
|---|---|
| **Período total disponível** | YYYY-MM-DD a YYYY-MM-DD |
| **Training period** | YYYY-MM-DD a YYYY-MM-DD |
| **Validation period** | YYYY-MM-DD a YYYY-MM-DD |
| **Test period (out-of-sample)** | YYYY-MM-DD a YYYY-MM-DD |
| **Justificativa da divisão** | - |

> ⚠️ O test period deve ser congelado ANTES de qualquer análise e só deve ser usado UMA VEZ.

---

## ⚠️ 5. Frequência

| Campo | Valor |
|---|---|
| **Frequência do sinal** | ex.: 8h (alinhado ao funding), diária, semanal |
| **Frequência de execução simulada** | ex.: entrada no próximo open após sinal |
| **Latência assumida** | ex.: sinal calculado em T, execução em T+1h |

---

## ⚠️ 6. Definição Matemática

Defina matematicamente o sinal, os critérios de entrada/saída e qualquer variável utilizada.

**Sinal (S_t):**
```
S_t = f(x₁_t, x₂_t, ...) 

Onde:
- x₁_t = [descrição precisa]
- x₂_t = [descrição precisa]
```

**Critério de entrada:**
```
Entrar long quando: [condição matemática]
Entrar short quando: [condição matemática]
```

**Critério de saída:**
```
Encerrar posição quando: [condição matemática]
Stop loss: [nível ou critério]
Take profit: [nível ou critério, se aplicável]
```

**Definições auxiliares (se "whale", "smart money", etc.):**
```
Whale = endereço com saldo > P99(distribuição de saldos) calculado sobre [período]
```

---

## 7. Baseline

O que seria o resultado esperado sem nenhum sinal (estratégia nula)?

| Baseline | Descrição | Expectativa |
|---|---|---|
| Buy & hold | Retorno de simplesmente manter o ativo | [calcular ex-ante] |
| Random entry | Entradas aleatórias com mesmo sizing | [estimar por simulação] |
| Benchmark de mercado | Índice de referência | [definir] |

A hipótese só tem valor se superar o baseline de forma estatisticamente significativa.

---

## ⚠️ 8. Possíveis Vieses

Liste explicitamente todos os potenciais vieses antes de olhar os resultados.

| Viés | Risco | Mitigação |
|---|---|---|
| Look-ahead bias | [descrever risco específico] | [como foi mitigado] |
| Data leakage | [descrever risco específico] | [como foi mitigado] |
| Survivorship bias | [descrever risco específico] | [como foi mitigado] |
| Selection bias | [descrever risco específico] | [como foi mitigado] |
| Overfitting / curve-fitting | [descrever risco específico] | [como foi mitigado] |
| Múltiplos testes | [quantos testes foram feitos?] | [correção aplicada?] |

---

## ⚠️ 9. Métricas de Avaliação

Defina as métricas ANTES de calcular os resultados. Não adicione métricas após ver os resultados.

| Métrica | Threshold mínimo para "edge" | Justificativa |
|---|---|---|
| Sharpe Ratio (OOS) | > 0.5 | - |
| Maximum Drawdown | < [X]% | - |
| Taxa de acerto | > [X]% | - |
| p-value (AR vs zero) | < 0.05 (com correção múltiplos testes) | - |
| Effect size (Cohen's d) | > [X] | - |
| Expectancy por trade | > [X] bps após custos | - |

---

## 10. Custos e Slippage

| Custo | Estimativa | Fonte da estimativa |
|---|---|---|
| Spread bid-ask | [X] bps | - |
| Taxa de exchange | [X] bps por lado | - |
| Slippage estimado | [X] bps | - |
| **Total por trade (ida+volta)** | [X] bps | - |

> Um edge de [X] bps por trade exige custo total < [X] bps para ser viável.

---

## 11. Análise de Robustez (plano)

Antes de executar, defina como será testada a robustez:

- [ ] Sensitivity analysis: variar parâmetros em ±[X]%
- [ ] Subperíodos: testar separadamente em [período A] e [período B]
- [ ] Walk-forward: janela de treino = [X] meses, passo = [Y] meses
- [ ] Permutation test: [N] permutações aleatórias do sinal
- [ ] Outros ativos: testar em [ETH, outros]

---

## RESULTADOS (preencher após análise)

> ⚠️ Preencha esta seção somente após concluir a análise. Não altere as seções acima após ver os resultados.

---

## 12. Resultados In-sample

| Métrica | Training | Validation |
|---|---|---|
| Sharpe Ratio | - | - |
| Retorno total | - | - |
| Max Drawdown | - | - |
| N operações | - | - |
| Taxa de acerto | - | - |
| Expectancy | - | - |
| p-value | - | - |

---

## 13. Resultados Out-of-sample

| Métrica | Resultado | Threshold definido a priori | Pass/Fail |
|---|---|---|---|
| Sharpe Ratio | - | > 0.5 | - |
| Max Drawdown | - | < [X]% | - |
| p-value | - | < 0.05 | - |
| Effect size | - | > [X] | - |
| Expectancy | - | > [X] bps | - |

---

## 14. Interpretação

O que os resultados dizem? Ser honesto — especialmente sobre limitações.

- O edge é estatisticamente significativo? Em qual conjunto?
- O edge é economicamente relevante (após custos)?
- O resultado foi estável em subperíodos?
- A análise de robustez confirma ou fragiliza o resultado?

---

## 15. Conclusão

**Resultado final:**
- [ ] Edge identificado e robusto → documentar e avançar para walk-forward mais rigoroso
- [ ] Edge identificado mas frágil → documentar como inconclusivo, listar condições específicas
- [ ] Hipótese refutada → documentar resultado negativo, arquivar

**Uma frase resumindo:**
> [Ex.: "Funding rate acima do P95 não demonstrou poder preditivo significativo sobre retorno das próximas 24h no período testado (2020-2022), com Sharpe OOS de -0.12 e p-value de 0.34."]

---

## 16. Limitações

Liste as limitações honestas desta análise:

1. Tamanho da amostra: [N] eventos — pode ser insuficiente para conclusões robustas
2. Período único: resultados podem não generalizar para outros regimes de mercado
3. Dados: [qualidade, gaps, possíveis erros de atribuição]
4. Custos: estimativa de slippage pode estar subestimada para trades maiores
5. [Outras limitações específicas]

---

## Arquivos Relacionados

| Arquivo | Descrição |
|---|---|
| `notebook_exploracao.ipynb` | Análise exploratória inicial |
| `notebook_backtest.ipynb` | Backtest completo |
| `notebook_robustez.ipynb` | Testes de robustez |
| `results/summary.csv` | Resultados numéricos |
| `results/equity_curve.png` | Equity curve |
```

---

## Checklist Final antes de Publicar Resultado

- [ ] Todas as seções acima estão preenchidas
- [ ] A hipótese foi definida ANTES de ver os dados
- [ ] O período out-of-sample foi tocado somente UMA vez
- [ ] Look-ahead bias foi explicitamente verificado
- [ ] Custos de transação estão incluídos nos resultados
- [ ] Todos os resultados negativos estão documentados
- [ ] O código que gera os resultados está commitado e reproduzível

---

*Experiment Protocol v1.0 — Market Research Lab*
