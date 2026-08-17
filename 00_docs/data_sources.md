# Fontes de Dados — Market Research Lab

> Catálogo de fontes de dados organizadas por categoria.
> Para cada fonte: tier de acesso, custo, qualidade e limitações conhecidas.

---

## Tier de Acesso

| Tier | Descrição |
|---|---|
| 🟢 Free | Gratuito, sem registro ou com registro gratuito |
| 🟡 Freemium | Plano gratuito com limitações; plano pago disponível |
| 🔴 Paid | Apenas plano pago |
| 🔵 Research | Acesso especial via programa de pesquisa |

---

## 1. Dados de Mercado (OHLCV)

| Fonte | Tier | Granularidade | Histórico | Notas |
|---|---|---|---|---|
| [Binance API](https://binance-docs.github.io/apidocs/) | 🟢 Free | 1s, 1m, 5m, ... 1M | ~2017 | Rate limits; dados de alta qualidade |
| [CoinGecko API](https://www.coingecko.com/en/api) | 🟡 Freemium | Diário (free), intraday (pago) | ~2013 | Boa cobertura de altcoins |
| [CryptoCompare](https://min-api.cryptocompare.com/) | 🟡 Freemium | Minuto | Variável | API bem documentada |
| [Kaiko](https://www.kaiko.com/) | 🔴 Paid | Tick | Longo | Alta qualidade; uso institucional |
| [yfinance](https://pypi.org/project/yfinance/) | 🟢 Free | Diário | ~2017 | Yahoo Finance; conveniente, mas não confiável para prod |

---

## 2. Dados de Derivativos

| Fonte | Tier | Dados disponíveis | Notas |
|---|---|---|---|
| [Binance Futures API](https://binance-docs.github.io/apidocs/futures/en/) | 🟢 Free | Funding rate, OI, liquidações | Dados em tempo real; histórico limitado na API pública |
| [Coinalyze](https://coinalyze.net/) | 🟡 Freemium | OI, funding, liquidações, multi-exchange | Agregado multi-exchange; gratuito com limitações |
| [Laevitas](https://laevitas.ch/) | 🟡 Freemium | OI, funding, liquidações, opções | Foco em opções também |
| [The Block Data](https://www.theblock.co/data) | 🟡 Freemium | OI agregado, volume futuros | Dados diários gratuitos |
| [CoinGlass](https://www.coinglass.com/) | 🟡 Freemium | Liquidações, OI, funding | API disponível; bom para liquidações |

---

## 3. Dados On-chain

| Fonte | Tier | Redes | Dados disponíveis | Notas |
|---|---|---|---|---|
| [Glassnode](https://glassnode.com/) | 🟡 Freemium | BTC, ETH e outros | Exchange flows, holder behavior, SOPR, MVRV, etc. | Referência em on-chain; plano free limitado |
| [CryptoQuant](https://cryptoquant.com/) | 🟡 Freemium | BTC, ETH e outros | Exchange flows, whale alerts, miner flows | Alternativa ao Glassnode |
| [Dune Analytics](https://dune.com/) | 🟡 Freemium | EVM (ETH, Polygon, etc.) | Queries SQL customizadas on-chain | Excelente para DeFi e EVM |
| [Nansen](https://nansen.ai/) | 🔴 Paid | Multi-chain | Wallet labeling, smart money tracking | Etiquetagem de carteiras de alta qualidade |
| [Arkham Intelligence](https://arkhamintelligence.com/) | 🟡 Freemium | Multi-chain | Entity identification, wallet tracking | Crescente; boa cobertura |
| [IntoTheBlock](https://www.intotheblock.com/) | 🟡 Freemium | BTC, ETH, altcoins | Large holders, concentration, flows | Bom para holder analysis |
| [Etherscan API](https://etherscan.io/apis) | 🟢 Free | ETH, ERC-20 | Transações, saldos, eventos de contratos | Direto da fonte; free com limites |
| [Blockchain.com API](https://www.blockchain.com/api) | 🟢 Free | BTC | Transações, blocos, endereços | Dados básicos de BTC |

---

## 4. Dados Macroeconômicos

| Fonte | Tier | Dados disponíveis | Notas |
|---|---|---|---|
| [FRED (Federal Reserve)](https://fred.stlouisfed.org/) | 🟢 Free | CPI, PCE, Fed Funds Rate, GDP, etc. | Via API FRED; referência padrão |
| [Bureau of Labor Statistics](https://www.bls.gov/data/) | 🟢 Free | NFP, CPI, PPI | Dados oficiais do governo; first release disponível |
| [Trading Economics](https://tradingeconomics.com/) | 🟡 Freemium | Calendário econômico global | Histórico de consenso e actual; útil para event study |
| [Investing.com](https://www.investing.com/economic-calendar/) | 🟡 Freemium | Calendário econômico | Alternativa ao Trading Economics |
| [OECD Data](https://data.oecd.org/) | 🟢 Free | Dados macro internacionais | Frequência baixa (mensal/trimestral) |

---

## 5. Dados de Eventos e Notícias

| Fonte | Tier | Dados disponíveis | Notas |
|---|---|---|---|
| [CryptoPanic](https://cryptopanic.com/developers/api/) | 🟡 Freemium | Notícias cripto categorizadas, sentiment | API disponível; útil para event tagging |
| [Santiment](https://santiment.net/) | 🔴 Paid | Social volume, sentiment, dev activity | Referência em social sentiment cripto |
| [LunarCrush](https://lunarcrush.com/) | 🟡 Freemium | Social engagement, influencer activity | Métricas de redes sociais |
| [Messari](https://messari.io/) | 🟡 Freemium | Research, on-chain, eventos | API bem documentada |

---

## 6. Order Flow e Microestrutura

| Fonte | Tier | Dados disponíveis | Notas |
|---|---|---|---|
| [Binance Trade Streams](https://binance-docs.github.io/apidocs/) | 🟢 Free | Trade-level data (taker side) | Coleta em tempo real via WebSocket |
| [Tardis.dev](https://tardis.dev/) | 🔴 Paid | Order book snapshots, tick data histórico | Referência para dados históricos de microestrutura |
| [Kaiko](https://www.kaiko.com/) | 🔴 Paid | Order book, trade data | Alta qualidade |

---

## Limitações e Cuidados

### Dados On-chain
- Atribuição de exchanges a endereços pode estar errada → validar com múltiplas fontes
- Dados de Glassnode/CryptoQuant podem ser revisados retroativamente → sempre registrar quando os dados foram baixados
- Heurísticas de clustering podem errar → não tratar como verdade absoluta

### Dados de Derivativos
- OI e liquidações podem diferir entre provedores (metodologias diferentes)
- Dados históricos de funding podem ter gaps

### Dados Macroeconômicos
- **Sempre usar "first release", nunca dados revisados em backtests**
- Registrar data de download dos dados

### Consensus/Surpresa
- Consenso de economistas pode variar por fonte (Bloomberg vs Reuters vs Trading Economics)
- Definir a priori qual fonte de consenso usar

---

*Data Sources v1.0 — Market Research Lab*
