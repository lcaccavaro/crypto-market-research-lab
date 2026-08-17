# Repositórios Externos — Market Research Lab

> Catálogo consolidado de repositórios externos clonados e auditados.
> Para cada projeto, ver o `AUDIT.md` correspondente em `02_external/repositories/<nome>/`.

---

## Tabela Consolidada — Projetos Clonados e Auditados

| Projeto | URL | Licença | Python | Status | O que faz | Relevância | Observações |
|---|---|---|---|---|---|---|---|
| **crypto-market-data** | [ErcinDedeoglu](https://github.com/ErcinDedeoglu/crypto-market-data) | CC BY 4.0 | N/A (dados JSON) | ✅ WORKING | 29 datasets diários on-chain + derivatives BTC (exchange flows, OI, funding, liquidações, whale ratio, etc.) | 🔴 **ALTA** | Dados prontos para uso imediato; atualização automática diária; histórico desde dez/2022; requer atribuição |
| **CRYPTODATACOLLECTOR** | [nopervA](https://github.com/nopervA/CRYPTODATACOLLECTOR) | ⚠️ Nenhuma | 3.10+ | ⚠️ PARTIAL | Coletor em tempo real de Binance Futures via WebSocket (trades, order book, funding, OI, liquidações) em Parquet | 🟡 **MÉDIA** | Referência de arquitetura para coleta de microestrutura; sem licença; não é histórico |
| **Orderflow** | [AndreaFerrante](https://github.com/AndreaFerrante/Orderflow) | ⚠️ Nenhuma clara | 3.8–3.11 | ⚠️ PARTIAL | Framework de market microstructure: volume profile, footprint, VWAP, backtesting, Monte Carlo, HMM, estatísticas | 🟡 **MÉDIA** | Referência de código de alta qualidade; `numba~0.58` incompatível com Python 3.14; sem licença clara |
| **crypto-quant-lab** | [SinanGokmen](https://github.com/SinanGokmen/crypto-quant-lab) | MIT | 3.9+ | ⚠️ PARTIAL | Lab de research de ICT/SMC (FVG/IFVG) com backtesting rigoroso, purged K-fold, walk-forward, Monte Carlo | 🔴 **MUITO ALTA** | Melhor referência metodológica da lista; documenta resultados negativos honestamente; anti-look-ahead por construção |
| **EventStudy** | [zrxbeijing](https://github.com/zrxbeijing/EventStudy) | MIT | 3.6 (obsoleto) | ❌ BROKEN | Event study para ações via Yahoo Finance + market model OLS; calcula retornos anormais | 🟡 **MÉDIA** | Abandonado desde 2020; `pandas-datareader` + Yahoo Finance quebrado; lógica de AR válida para referência |
| **market-regime-detection** | [Sakeeb91](https://github.com/Sakeeb91/market-regime-detection) | ⚠️ Nenhuma | 3.8+ (plan.) | ❌ BROKEN | HMM + GMM + change point detection para regimes de mercado (SPY) | 🟢 **BAIXA** | Repositório é apenas plano (README + docs); nenhum código implementado |

---

## Legenda de Status

| Status | Significado |
|---|---|
| ✅ WORKING | Funciona conforme documentado, sem bloqueadores |
| ⚠️ PARTIAL | Funciona parcialmente; há limitações de deps, versão ou escopo |
| ❌ BROKEN | Não funciona — código ausente, deps quebradas ou projeto abandonado |
| 🚫 NOT_RELEVANT | Funcional mas fora do escopo do laboratório |

---

## Indicação de Aproveitamento

### 🔴 Usar imediatamente

| Projeto | O que usar |
|---|---|
| **crypto-market-data** | Todos os 29 datasets JSON como fonte de dados para H001, H002, H003, H005. Pronto para uso sem instalação adicional. |

### 🟡 Estudar o código — não executar ainda

| Projeto | O que estudar |
|---|---|
| **crypto-quant-lab** | `ifvg/analysis/` (walk-forward, monte_carlo, metrics), `atom_indicator/cv.py` (purged K-fold), `ifvg/tests/test_engine_no_lookahead.py` — referência metodológica para validação |
| **Orderflow** | `orderflow/stats/montecarlo.py`, `orderflow/stats/hypothesis.py`, `orderflow/stats/markov.py` — referência de implementação estatística |
| **EventStudy** | `EventStudy/return_calculator.py` — lógica de cálculo de Abnormal Returns (OLS market model) para H004 |
| **CRYPTODATACOLLECTOR** | `collector/taker_delta_builder.py`, `collector/funding_event_tracker.py` — referência de lógica de order flow |

### 🔴 Não usar

| Projeto | Motivo |
|---|---|
| **market-regime-detection** | Sem código implementado |
| **EventStudy** (como ferramenta) | Abandonado, deps quebradas |

---

## Conflitos de Dependências Identificados

| Conflito | Projetos afetados | Solução |
|---|---|---|
| `numba~0.58` incompatível com Python 3.14 | Orderflow | Criar venv isolado com Python 3.11 se necessário executar |
| `polars~0.19.13` (versão muito antiga) | Orderflow | Idem |
| `pandas-datareader` + Yahoo Finance quebrado (2026) | EventStudy | Não instalar; usar `yfinance` direto se necessário |
| `pyarrow`, `aiohttp`, `websockets` ausentes | CRYPTODATACOLLECTOR | Instalar em venv isolado somente se precisar executar |

**Regra:** Nenhuma dependência de projetos externos foi instalada no venv principal (`market-research-lab/.venv`). Venvs isolados a criar conforme necessidade.

---

## Referências para Estudo Futuro (não clonados)

| Repositório | Descrição | Relevância |
|---|---|---|
| [quantconnect/Lean](https://github.com/quantconnect/Lean) | Engine de backtesting institucional | Alta — referência de arquitetura |
| [mementum/backtrader](https://github.com/mementum/backtrader) | Framework de backtesting Python maduro | Alta — simples e didático |
| [polakowo/vectorbt](https://github.com/polakowo/vectorbt) | Backtesting vetorizado de alta performance | Alta — ideal para research |
| [robcarver17/pysystemtrade](https://github.com/robcarver17/pysystemtrade) | Sistema de trading sistemático (Robert Carver) | Alta — referência de quant sistemático |
| [hudson-and-thames/mlfinlab](https://github.com/hudson-and-thames/mlfinlab) | Implementações do livro "Advances in Financial ML" (Lopez de Prado) | Alta — referência em ML financeiro rigoroso |
| [stefan-jansen/machine-learning-for-trading](https://github.com/stefan-jansen/machine-learning-for-trading) | Código do livro "ML for Algorithmic Trading" | Alta — excelente referência |
| [coinmetrics/community-data](https://github.com/coinmetrics/community-data) | Dados históricos on-chain (CoinMetrics Community) | Alta — dados gratuitos de qualidade |

---

*Repositories v2.0 — Auditoria completa em 2026-08-17*
