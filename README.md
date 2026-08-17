# Market Research Lab

> Laboratório local de pesquisa quantitativa de mercados de criptomoedas.

## Objetivo

Investigar se informações **além de preço/OHLC/análise técnica** possuem poder explicativo ou preditivo sobre o comportamento futuro do mercado de criptomoedas.

Este projeto é **exclusivamente** um laboratório de pesquisa executado localmente em Python, notebooks e scripts.

## O que este projeto NÃO é

| ❌ Não é | ✅ É |
|---|---|
| Aplicativo / frontend | Laboratório de pesquisa local |
| API / SaaS | Notebooks Python |
| Bot de trading | Scripts de análise |
| Sistema de execução de ordens | Validação estatística rigorosa |
| Deploy / cloud | Pesquisa quantitativa |

## Áreas de Investigação

1. **On-chain analytics** — dados registrados diretamente na blockchain
2. **Wallet behavior** — padrões de comportamento de carteiras
3. **Whale behavior** — grandes detentores e seus movimentos
4. **Wallet clustering** — agrupamento de carteiras por comportamento
5. **Exchange inflows/outflows** — fluxos para/de exchanges
6. **Stablecoin flows** — movimentação de stablecoins como proxy de demanda
7. **Smart-money proxies** — carteiras com histórico de performance superior (definido quantitativamente)
8. **Order flow** — pressão direcional via trades de takers
9. **Market microstructure** — estrutura do livro de ordens
10. **Derivatives** — mercado futuro e perpétuo
11. **Funding rate** — taxa de financiamento de contratos perpétuos
12. **Open Interest** — contratos abertos em aberto
13. **Liquidations** — liquidações forçadas e seu impacto
14. **Macro events** — eventos macroeconômicos globais
15. **News/events** — notícias e seu impacto no preço
16. **Expectation vs actual** — surpresa de evento vs. consenso
17. **Quantitative research** — métodos estatísticos rigorosos
18. **Market regimes** — identificação de regimes de mercado
19. **Risk/reward** — análise de risco-retorno
20. **Statistical validation** — validação estatística robusta
21. **Out-of-sample validation** — validação fora da amostra
22. **Walk-forward validation** — validação walk-forward
23. **Monte Carlo / robustness** — testes de robustez
24. **Look-ahead bias prevention** — prevenção de viés de antecipação

## Princípio Fundamental

> **Não queremos provar uma teoria. Queremos tentar REFUTÁ-LA.**

Se uma hipótese não possuir edge estatístico robusto, registramos o resultado e a abandonamos.

## Estrutura do Projeto

```
market-research-lab/
├── 00_docs/          # Documentação, glossário, princípios
├── 01_data/          # Dados brutos, processados, metadados
│   ├── raw/
│   │   ├── market/
│   │   ├── derivatives/
│   │   ├── onchain/
│   │   ├── macro/
│   │   └── events/
│   ├── processed/
│   └── metadata/
├── 02_external/      # Repositórios externos clonados
├── 03_notebooks/     # Notebooks de exploração e análise
│   ├── 01_data_exploration/
│   ├── 02_onchain/
│   ├── 03_whales/
│   ├── 04_exchange_flows/
│   ├── 05_orderflow/
│   ├── 06_derivatives/
│   ├── 07_macro/
│   ├── 08_events/
│   ├── 09_quant/
│   └── 10_regimes/
├── 04_features/      # Feature engineering
├── 05_hypotheses/    # Hipóteses formalizadas
│   ├── H001_funding_oi/
│   ├── H002_exchange_flows/
│   ├── H003_whale_accumulation/
│   ├── H004_event_surprise/
│   └── H005_multifactor_confluence/
├── 06_backtesting/   # Backtests rigorosos
├── 07_validation/    # Validação out-of-sample e walk-forward
├── 08_results/       # Resultados e relatórios
├── scripts/          # Scripts utilitários
├── tests/            # Testes unitários
└── requirements/     # Dependências Python
    ├── base.txt
    └── dev.txt
```

## Como Começar

### 1. Ativar o ambiente virtual

```bash
source market-research-lab/.venv/bin/activate
```

### 2. Instalar dependências (se necessário)

```bash
pip install -r market-research-lab/requirements/base.txt
# ou para desenvolvimento:
pip install -r market-research-lab/requirements/dev.txt
```

### 3. Executar JupyterLab

```bash
jupyter lab
```

### 4. Executar um notebook específico (sem interface)

```bash
jupyter nbconvert --to notebook --execute 03_notebooks/01_data_exploration/meu_notebook.ipynb
```

## Documentação

| Arquivo | Descrição |
|---|---|
| [glossary.md](00_docs/glossary.md) | Glossário técnico completo |
| [research_principles.md](00_docs/research_principles.md) | Princípios científicos do projeto |
| [experiment_protocol.md](00_docs/experiment_protocol.md) | Protocolo obrigatório para hipóteses |
| [hypotheses.md](00_docs/hypotheses.md) | Registro de hipóteses |
| [data_sources.md](00_docs/data_sources.md) | Fontes de dados |
| [repositories.md](00_docs/repositories.md) | Repositórios externos relevantes |

---

*Market Research Lab — Pesquisa quantitativa rigorosa, sem atalhos.*
