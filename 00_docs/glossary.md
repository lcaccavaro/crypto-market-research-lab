# Glossário — Market Research Lab

> Cada termo é apresentado com: definição simples, definição técnica, exemplo, utilidade e o que **não** podemos concluir a partir dele.

---

## OHLC

**Definição simples:** Os quatro preços que resumem o comportamento de um ativo em um período: abertura, máxima, mínima e fechamento.

**Definição técnica:** Representação canônica de séries temporais de preços. `O` = preço de abertura do período; `H` = preço máximo atingido; `L` = preço mínimo atingido; `C` = preço de fechamento. Volume frequentemente é incluído como quinta coluna (OHLCV).

**Exemplo:** BTC/USDT em 2024-01-15 (1h): `O=43.200`, `H=43.800`, `L=42.900`, `C=43.500`, `V=1.230 BTC`.

**Por que pode ser útil:** Fornece a base para a maioria dos indicadores técnicos, permite comparação entre períodos e é universalmente disponível em todas as exchanges.

**O que NÃO podemos concluir:** OHLC não revela a ordem cronológica intracandle dos movimentos. Um candle com H e L extremos pode ter ido para cima antes de baixar, ou o contrário. Não revela intenção, causa ou origem do fluxo de ordens.

---

## On-chain

**Definição simples:** Dados que estão registrados diretamente na blockchain e são públicos e imutáveis.

**Definição técnica:** Conjunto de informações derivadas do ledger distribuído de uma blockchain: transações, endereços, saldos, smart contracts, gas fees, timestamps de blocos e qualquer evento inscrito on-chain. Contrasta com dados off-chain (exchanges centralizadas, APIs privadas).

**Exemplo:** A quantidade de BTC movida da carteira de uma exchange para uma wallet externa em uma transação específica registrada no bloco 840.000.

**Por que pode ser útil:** Permite observar movimentações reais de capital sem depender de dados de exchanges centralizadas, que podem ser opacos. Pode revelar acumulação/distribuição de grandes detentores.

**O que NÃO podemos concluir:** On-chain não revela identidade, intenção ou motivação por trás de uma transação. Uma saída de exchange pode ser custódia de longo prazo, venda OTC, ou reorganização interna de uma mesma entidade. Correlação com preço não implica causalidade.

---

## Whale

**Definição simples:** Um participante do mercado que detém quantidade suficientemente grande de um ativo para potencialmente influenciar seu preço.

**Definição técnica:** Endereço ou conjunto de endereços (cluster) com saldo ou volume transacionado acima de um limiar quantitativamente definido. **Neste laboratório, o critério deve ser definido explicitamente antes de qualquer análise** (ex.: endereços com saldo > X BTC no percentil 99 da distribuição de saldos).

**Exemplo:** Uma carteira com mais de 1.000 BTC que move fundos para uma exchange é frequentemente categorizada como whale por provedores como Glassnode ou Santiment.

**Por que pode ser útil:** O comportamento de grandes detentores pode antecipar movimentos de preço — mas isso precisa ser testado, não assumido.

**O que NÃO podemos concluir:** Que toda whale é "smart money". Que movimentação de whale implica venda ou compra. Que o critério de uma fonte externa é o correto para o contexto da pesquisa. Não podemos inferir intenção de uma transação isolada.

---

## Holder

**Definição simples:** Participante que mantém um ativo por um período prolongado sem vendê-lo.

**Definição técnica:** Em análise on-chain, um endereço cujos UTXOs (Bitcoin) ou tokens não foram movidos por um período definido (tipicamente 155+ dias para "Long-Term Holder" em métricas do Glassnode). O conceito é operacionalizado via "coin age" ou "UTXO age".

**Exemplo:** Um endereço que recebeu BTC em janeiro de 2022 e não moveu esses UTXOs até julho de 2023 seria classificado como Long-Term Holder.

**Por que pode ser útil:** A proporção de moedas detidas por Long-Term Holders vs Short-Term Holders pode indicar oferta disponível ao mercado (supply shock potential).

**O que NÃO podemos concluir:** Que holders são investidores "pacientes" ou "racionais". Que inatividade de endereço implica intenção de manter. Endereços perdidos, exchanges frias e contratos também aparecem como "holders".

---

## Exchange Flow

**Definição simples:** A quantidade de criptomoeda que entra ou sai de carteiras conhecidas de exchanges.

**Definição técnica:** Métrica on-chain que agrega transferências para/de endereços atribuídos a exchanges (por heurísticas de clustering ou etiquetagem). `Inflow` = transferências para a exchange; `Outflow` = transferências para fora da exchange.

**Exemplo:** Um inflow de 15.000 BTC para Binance em 24h, contra uma média histórica de 3.000 BTC, pode indicar pressão vendedora potencial.

**Por que pode ser útil:** Grandes inflows para exchanges historicamente precedem pressão de venda (usuários depositando para vender). Outflows podem indicar acumulação (saindo para cold storage).

**O que NÃO podemos concluir:** Que inflow = venda garantida. Inflows podem ser para margem de futuros, staking, empréstimos ou simples reorganização de carteiras. Exchanges classificadas incorretamente distorcem os dados.

---

## Netflow

**Definição simples:** A diferença entre entradas e saídas de uma exchange em um período.

**Definição técnica:** `Netflow = Inflow - Outflow`. Valor positivo indica acúmulo líquido na exchange (mais moedas chegando do que saindo); valor negativo indica retirada líquida.

**Exemplo:** Se Binance recebeu 20.000 BTC e enviou 22.000 BTC em 24h, o Netflow é -2.000 BTC (saída líquida).

**Por que pode ser útil:** Netflow negativo persistente pode indicar acumulação por parte de holders (tirando moedas do mercado spot). Netflow positivo pode sinalizar intenção de liquidez.

**O que NÃO podemos concluir:** Que netflow negativo é necessariamente bullish. Exchanges com erros de atribuição de endereços podem distorcer completamente a métrica. Deve-se validar com múltiplas fontes.

---

## Funding Rate

**Definição simples:** A taxa periódica paga entre compradores e vendedores em contratos perpétuos para manter o preço do contrato próximo ao preço spot.

**Definição técnica:** Em contratos perpétuos (sem vencimento), o funding rate é calculado periodicamente (ex.: a cada 8 horas na Binance) com base no premium do contrato sobre o índice spot. Funding rate positivo: longs pagam shorts. Funding rate negativo: shorts pagam longs. Formula simplificada: `Funding = Clamp(Premium Index + Interest Rate Basis, -0.05%, 0.05%)`.

**Exemplo:** Funding rate de +0.10% a cada 8h em BTC/USDT perp implica que um long de $100.000 paga $100 por período.

**Por que pode ser útil:** Funding rate elevado e persistente pode indicar mercado excessivamente alavancado em uma direção, criando condições para short squeeze ou long squeeze.

**O que NÃO podemos concluir:** Que funding rate alto é sinal de topo garantido. Funding pode permanecer elevado durante tendências fortes. É um indicador de sentimento/posicionamento, não de direção.

---

## Open Interest

**Definição simples:** O total de contratos em aberto (não encerrados) no mercado de derivativos.

**Definição técnica:** Número total de contratos futuros ou perpétuos que estão abertos e não liquidados em um dado momento. Aumenta quando novos contratos são criados; diminui quando contratos são encerrados ou liquidados. Frequentemente medido em USD ou em moeda base (BTC, ETH).

**Exemplo:** Se o Open Interest de BTC perp na Binance é $8 bilhões, isso representa o valor nocional total de posições abertas.

**Por que pode ser útil:** Crescimento de OI com alta de preço pode indicar tendência forte com entrada de novo capital. Queda de OI com queda de preço pode indicar liquidações e capitulação.

**O que NÃO podemos concluir:** Que alto OI implica direção. OI mede o tamanho do mercado de derivativos, não o posicionamento net. Shorts e longs somam o mesmo OI.

---

## Liquidation

**Definição simples:** O encerramento forçado de uma posição alavancada quando o trader não tem mais margem suficiente para manter a posição aberta.

**Definição técnica:** Quando o valor da margem de manutenção de uma posição cai abaixo do nível mínimo exigido pela exchange, o sistema de liquidação fecha automaticamente a posição. A exchange vende (para longs) ou compra (para shorts) o ativo ao preço de mercado. Em cascata, liquidações podem alimentar mais liquidações.

**Exemplo:** Um trader com 10x de alavancagem em BTC a $50.000 será liquidado se o preço cair ~10% (para ~$45.000), dependendo da margem inicial.

**Por que pode ser útil:** Grandes clusters de liquidações em um nível de preço específico podem funcionar como "imãs" — o preço tende a atingir zonas de alta concentração de ordens de liquidação.

**O que NÃO podemos concluir:** Que liquidação de longs implica continuação de queda. Liquidações podem ser o ponto final de uma correção, sendo seguidas por recuperação.

---

## Order Flow

**Definição simples:** A pressão direcional gerada pelos trades que acontecem de fato no mercado, distinguindo quem "atacou" a oferta ou a demanda.

**Definição técnica:** Medida da iniciativa de compra vs. venda no mercado. Calculado pelo volume de trades onde o comprador foi o agressor (taker buy) menos o volume onde o vendedor foi o agressor (taker sell). Também chamado de "signed volume" ou "delta".

**Exemplo:** Se em 1 hora houve R$50M em Taker Buy e R$30M em Taker Sell, o Order Flow Delta é +$20M (pressão compradora líquida).

**Por que pode ser útil:** Order flow positivo acumulado com preço estagnado pode indicar absorção — alguém absorvendo a oferta antes de uma alta. É uma das métricas mais próximas de "intenção de mercado".

**O que NÃO podemos concluir:** Que order flow positivo implica alta garantida. Grandes players podem criar order flow enganoso (spoofing, layering). Correlação com retorno futuro deve ser testada empiricamente.

---

## Market Microstructure

**Definição simples:** O estudo detalhado de como o mercado funciona "por dentro" — ordens, execuções, spreads e comportamento dos participantes.

**Definição técnica:** Campo que analisa os mecanismos de formação de preço em nível micro: livro de ordens (order book), spread bid-ask, profundidade de mercado, latência de execução, impacto de preço de ordens grandes, e os incentivos dos diferentes tipos de participantes (market makers, takers, arbitrageurs).

**Exemplo:** Analisar como o spread bid-ask do BTC/USDT na Binance varia em função do volume negociado nas últimas 5 minutos.

**Por que pode ser útil:** Métricas de microestrutura (spread, imbalance, trade size distribution) podem antecipar movimentos de preço de curto prazo e revelar comportamento informado vs. desinformado.

**O que NÃO podemos concluir:** Que padrões de microestrutura são estáveis ao longo do tempo. Mercados de cripto têm microestrutura muito diferente de mercados tradicionais e ela muda com liquidez, regulação e participantes.

---

## Taker Buy

**Definição simples:** Uma compra onde o comprador pagou o preço pedido pelo vendedor (atacou o ask).

**Definição técnica:** Trade executado contra uma ordem limitada de venda existente no livro de ordens. O comprador é o agressor (taker), a ordem de venda é o market maker (maker). Classificado por: se o preço do trade é igual ao ask no momento da execução, é taker buy.

**Exemplo:** BTC ask a $50.000. Trader envia ordem a mercado de compra e paga $50.000. Esse volume é classificado como Taker Buy.

**Por que pode ser útil:** Volume de Taker Buy representa pressão compradora ativa e urgente — traders que querem posição imediatamente e estão dispostos a pagar o spread.

**O que NÃO podemos concluir:** Que Taker Buy elevado implica alta do preço. Em mercados com muita liquidez, grandes taker buys podem ser absorvidos sem movimento de preço significativo.

---

## Taker Sell

**Definição simples:** Uma venda onde o vendedor aceitou o preço oferecido pelo comprador (atacou o bid).

**Definição técnica:** Trade executado contra uma ordem limitada de compra existente no livro de ordens. O vendedor é o agressor (taker). Classificado por: se o preço do trade é igual ao bid no momento da execução, é taker sell.

**Exemplo:** BTC bid a $49.990. Trader envia ordem a mercado de venda e recebe $49.990. Esse volume é Taker Sell.

**Por que pode ser útil:** Volume de Taker Sell elevado indica pressão vendedora ativa. A proporção Taker Buy / Taker Sell é usada para calcular o "buy ratio" e o delta de order flow.

**O que NÃO podemos concluir:** Que Taker Sell elevado implica queda continuada. Pode ser o esgotamento de vendedores antes de uma reversão.

---

## Bid

**Definição simples:** O preço máximo que um comprador está disposto a pagar por um ativo no livro de ordens.

**Definição técnica:** Melhor ordem de compra limitada pendente no livro de ordens. O "best bid" é a maior oferta de compra ativa. Quando uma venda a mercado é executada, ela preenche o bid.

**Exemplo:** Se o livro de BTC/USDT tem ordens de compra em $49.990, $49.985 e $49.970, o best bid é $49.990.

**Por que pode ser útil:** A profundidade do bid (volume acumulado abaixo do best bid) indica suporte de curto prazo e custo de impacto para vendas grandes.

**O que NÃO podemos concluir:** Que ordens no bid representam intenção real de compra. Ordens podem ser retiradas imediatamente (spoofing). O bid não é garantia de suporte.

---

## Ask

**Definição simples:** O preço mínimo que um vendedor está disposto a aceitar por um ativo no livro de ordens.

**Definição técnica:** Melhor ordem de venda limitada pendente no livro de ordens. O "best ask" é a menor oferta de venda ativa. Quando uma compra a mercado é executada, ela preenche o ask.

**Exemplo:** Se o livro tem ordens de venda em $50.000, $50.010 e $50.025, o best ask é $50.000.

**Por que pode ser útil:** A profundidade do ask indica resistência de curto prazo e custo de impacto para compras grandes.

**O que NÃO podemos concluir:** Que ordens no ask são vendas genuínas. Market makers frequentemente postam e cancelam ordens rapidamente.

---

## Spread

**Definição simples:** A diferença entre o preço de compra (ask) e o preço de venda (bid).

**Definição técnica:** `Spread = Ask - Bid`. Frequentemente expresso em termos percentuais: `Spread% = (Ask - Bid) / Mid * 100`, onde `Mid = (Ask + Bid) / 2`. Representa o custo imediato de execução para um participante que usa ordens a mercado.

**Exemplo:** BTC/USDT com bid $49.995 e ask $50.005: spread = $10, spread% ≈ 0.020%.

**Por que pode ser útil:** Spread baixo indica mercado líquido. Spread que se alarga pode indicar stress de liquidez, eventos de mercado ou comportamento de market maker defensivo.

**O que NÃO podemos concluir:** Que spread alto implica direção. Alargamento de spread indica incerteza, não direção.

---

## Order Book Imbalance

**Definição simples:** A assimetria entre o volume de ordens de compra e venda no livro de ordens em um dado momento.

**Definição técnica:** `Imbalance = (Bid Volume - Ask Volume) / (Bid Volume + Ask Volume)`, calculado tipicamente para os N níveis mais próximos do mid price. Valores próximos de +1 indicam dominância de compradores no livro; próximos de -1 indicam dominância de vendedores.

**Exemplo:** 5 primeiros níveis do book: Bid total = $2M, Ask total = $800K → Imbalance ≈ +0.43 (pressão compradora).

**Por que pode ser útil:** Order book imbalance é um dos preditores de curtíssimo prazo mais estudados em market microstructure. Pode antecipar movimento de preço nos próximos milissegundos a segundos.

**O que NÃO podemos concluir:** Que imbalance é estável ou confiável em janelas maiores. Ordens no book podem ser canceladas instantaneamente. É uma métrica relevante para estratégias de alta frequência, não necessariamente para pesquisa de prazo mais longo.

---

## Smart Money

**Definição simples:** Participantes do mercado com acesso a informação privilegiada ou com histórico consistente de performance superior.

**Definição técnica:** **Neste laboratório, o termo "smart money" só pode ser usado com uma definição quantitativa explícita.** Um proxy aceitável: endereços que realizaram compras nos X% de menores preços e vendas nos X% de maiores preços em um período histórico definido, com performance estatisticamente significativa acima de um benchmark (ex.: buy-and-hold).

**Exemplo:** "Endereços que compraram BTC entre $15.000-$20.000 em Q4/2022 e venderam acima de $60.000 em 2024" — isso é uma definição quantitativa, não um rótulo.

**Por que pode ser útil:** Se for possível identificar endereços com histórico de timing consistentemente superior ao acaso, seu comportamento futuro pode ser um sinal relevante.

**O que NÃO podemos concluir:** Que performance passada implica informação privilegiada. Pode ser sorte. Que qualquer endereço chamado de "smart money" por uma fonte externa usa o mesmo critério que o nosso. Look-ahead bias é um risco crítico aqui.

---

## Market Regime

**Definição simples:** Um estado ou "fase" do mercado com características estatísticas distintas (ex.: tendência de alta, tendência de baixa, lateralização, alta volatilidade).

**Definição técnica:** Uma segmentação do tempo de mercado em estados latentes com propriedades estatísticas homogêneas dentro de cada estado. Pode ser identificado via Hidden Markov Models (HMM), clustering de retornos/volatilidade, ou critérios de regras (ex.: preço acima/abaixo de SMA de 200 dias).

**Exemplo:** Regime "bull trend" = retorno anualizado > 50%, volatilidade < 60%, drawdown < 20%. Regime "bear" = retorno anualizado < -30%, volatilidade > 80%.

**Por que pode ser útil:** Um sinal que funciona em regime bull pode falhar completamente em regime bear. Condicionar análise ao regime pode evitar sinais espúrios.

**O que NÃO podemos concluir:** Que regimes são estáveis ou previsíveis. Que a definição de regime é única ou universal. Regimes definidos ex-post podem não ser identificáveis em tempo real.

---

## Event Study

**Definição simples:** Uma metodologia para medir o impacto de um evento específico no preço de um ativo, isolando esse impacto do movimento geral do mercado.

**Definição técnica:** Técnica econométrica que compara o retorno observado de um ativo em torno de um evento com o retorno esperado (baseado em um modelo de benchmark). O retorno anormal é calculado como `AR = R_observado - R_esperado`. Envolve definição de: evento, janela de estimação, janela de evento e janela de pós-evento.

**Exemplo:** Medir o retorno anormal do BTC nas 24h após cada anúncio do FOMC entre 2020-2024.

**Por que pode ser útil:** Permite isolar o efeito de eventos específicos (halvings, anúncios regulatórios, hacks de exchanges) do ruído de mercado.

**O que NÃO podemos concluir:** Que o evento causou o retorno anormal. Outros eventos simultâneos podem contaminar o resultado. Pequena amostra de eventos limita significância estatística.

---

## Abnormal Return

**Definição simples:** O retorno de um ativo que não é explicado pelo comportamento geral do mercado em um período.

**Definição técnica:** `AR_t = R_t - E[R_t]`, onde `R_t` é o retorno observado e `E[R_t]` é o retorno esperado dado um modelo de referência (ex.: retorno do índice de mercado, CAPM, market model). O Cumulative Abnormal Return (CAR) é a soma dos ARs ao longo da janela de evento.

**Exemplo:** BTC subiu 5% no dia de um anúncio de adoção institucional. O mercado cripto como um todo subiu 2%. O Abnormal Return é aproximadamente +3%.

**Por que pode ser útil:** Permite atribuir impacto de preço a eventos específicos, controlando por movimentos gerais do mercado.

**O que NÃO podemos concluir:** Que o AR é atribuível exclusivamente ao evento de interesse. Que um AR positivo implica que o evento foi "bom" para o mercado a longo prazo.

---

## Event Window

**Definição simples:** O período de tempo ao redor de um evento no qual medimos o impacto no preço.

**Definição técnica:** Intervalo de tempo `[t-τ₁, t+τ₂]` ao redor do evento no tempo `t`, dentro do qual calculamos o retorno anormal. A escolha da janela é crítica: janelas muito largas incluem ruído; janelas muito curtas podem perder o efeito.

**Exemplo:** Para anúncios do FOMC, uma event window razoável poderia ser [-1h, +24h] em relação ao horário do anúncio.

**Por que pode ser útil:** Define precisamente onde buscamos o efeito. Deve ser definida a priori (antes de ver os dados).

**O que NÃO podemos concluir:** Que a janela escolhida é a "correta". Diferentes janelas podem produzir resultados diferentes. Se a janela foi escolhida após ver os dados (data snooping), os resultados são inválidos.

---

## Estimation Window

**Definição simples:** O período anterior ao evento usado para estimar o comportamento "normal" do ativo (o baseline).

**Definição técnica:** Intervalo de tempo `[t-T, t-τ₁-1]` antes da event window, usado para calibrar o modelo de retorno esperado. Tipicamente 120-250 dias em estudos com dados diários. Deve ser suficientemente longo para estimar parâmetros estáveis, mas não tão longo que inclua estrutural breaks.

**Exemplo:** Para medir o efeito de um halving em maio de 2020, a estimation window poderia ser janeiro 2019 – abril 2020.

**Por que pode ser útil:** Fornece o baseline contra o qual o retorno anormal é calculado. Sem essa janela, não há como separar "normal" de "anormal".

**O que NÃO podemos concluir:** Que o retorno médio na estimation window representa o verdadeiro "esperado". Regime de mercado pode mudar. A estimation window não deve conter outros eventos significativos.

---

## Surprise

**Definição simples:** A diferença entre o valor real de um indicador econômico e o valor que o mercado esperava.

**Definição técnica:** `Surprise = Actual - Consensus`, onde `Consensus` é a estimativa mediana dos analistas antes do anúncio (ex.: coletada por Bloomberg, Reuters). Frequentemente normalizado: `Standardized Surprise = (Actual - Consensus) / Std(Surprises Históricas)`.

**Exemplo:** CPI esperado: +0.3% m/m. CPI realizado: +0.5% m/m. Surprise = +0.2 pp (inflação acima do esperado).

**Por que pode ser útil:** A hipótese é que o mercado já precifica o consenso. O que move o preço é o desvio do esperado — a surpresa. Isso permite medir a "reação por unidade de surpresa".

**O que NÃO podemos concluir:** Que a mesma surpresa sempre produz a mesma reação. O contexto macroeconômico, o regime de mercado e o posicionamento prévio afetam a sensibilidade do mercado à surpresa.

---

## Consensus

**Definição simples:** A estimativa coletiva dos analistas sobre o valor de um indicador econômico antes de sua divulgação.

**Definição técnica:** Mediana (ou média) das projeções de analistas coletadas antes de um anúncio econômico. Fontes comuns: Bloomberg Survey, Reuters Poll, Trading Economics. Representa a melhor estimativa do mercado sobre o valor que será divulgado.

**Exemplo:** Antes do NFP (Non-Farm Payrolls) de março de 2024: consensus = +200K empregos criados.

**Por que pode ser útil:** Permite calcular a surprise e entender o que já estava precificado pelo mercado no momento do anúncio.

**O que NÃO podemos concluir:** Que o consensus representa toda a informação disponível. Nem todos os participantes pesam igualmente no consenso. O consenso pode ser estrategicamente influenciado.

---

## Actual

**Definição simples:** O valor real e oficial de um indicador econômico após sua divulgação.

**Definição técnica:** O valor publicado pela fonte oficial (ex.: Bureau of Labor Statistics para NFP, Bureau of Economic Analysis para GDP, Federal Reserve para decisões de taxa). Pode ser revisado posteriormente — uma fonte crítica de bias se usarmos dados revisados em backtests de eventos passados.

**Exemplo:** NFP de março 2024: Actual = +303K (acima do consensus de +200K → positive surprise).

**Por que pode ser útil:** O ponto de referência para calcular a surprise. Sempre usar o "first release" (primeiro release), nunca dados revisados.

**O que NÃO podemos concluir:** Que o valor "actual" estava disponível imediatamente. Há latência de publicação. Em backtests, nunca usar dados revisados como se fossem o valor disponível no momento.

---

## Expectancy

**Definição simples:** O resultado médio esperado por trade em uma estratégia, considerando a taxa de acerto e a razão risco/retorno.

**Definição técnica:** `Expectancy = (P_win × Avg_Win) - (P_loss × Avg_Loss)`, onde `P_win` e `P_loss` são as probabilidades de ganho e perda, e `Avg_Win` e `Avg_Loss` são os ganhos e perdas médios. Uma estratégia com expectancy positivo é lucrativa em esperança matemática.

**Exemplo:** Taxa de acerto = 40%, ganho médio = $300, perda média = $100 → Expectancy = (0.4 × 300) - (0.6 × 100) = 120 - 60 = +$60 por trade.

**Por que pode ser útil:** Uma estratégia pode ter baixa taxa de acerto e ainda ser lucrativa se o gain/loss ratio for favorável. Expectancy positiva é condição necessária (mas não suficiente) para uma estratégia ser viável.

**O que NÃO podemos concluir:** Que expectancy positiva em backtest implica performance positiva em live trading. Custos, slippage e overfitting podem eliminar o edge.

---

## Sharpe Ratio

**Definição simples:** Uma medida de retorno ajustado ao risco — quanto de retorno extra se obtém por unidade de risco assumida.

**Definição técnica:** `Sharpe = (R_p - R_f) / σ_p`, onde `R_p` é o retorno do portfólio, `R_f` é a taxa livre de risco, e `σ_p` é o desvio padrão dos retornos. Anualizado: `Sharpe_anualizado = Sharpe_diário × √252` (para dados diários). Um Sharpe > 1.0 é geralmente considerado adequado; > 2.0 é excelente.

**Exemplo:** Estratégia com retorno médio de 25% a.a., taxa livre de risco 5% a.a. e volatilidade de 20%: Sharpe = (25-5)/20 = 1.0.

**Por que pode ser útil:** Permite comparar estratégias com diferentes níveis de risco em uma métrica única. Essencial para avaliar se o retorno justifica o risco.

**O que NÃO podemos concluir:** Que Sharpe alto em backtest se mantém fora da amostra. Sharpe pode ser inflado por overfitting, por janelas curtas ou por ignorar fat tails. Sharpe não captura risco de cauda (drawdowns extremos).

---

## Maximum Drawdown

**Definição simples:** A maior queda percentual do pico ao vale observada durante um período.

**Definição técnica:** `MDD = min((V_t - V_peak) / V_peak)` para todo t no período, onde `V_t` é o valor da estratégia no tempo t e `V_peak` é o valor máximo atingido até t. Mede a pior perda que um investidor teria experimentado.

**Exemplo:** Estratégia que sobe de $100K para $200K e depois cai para $130K antes de se recuperar tem um MDD de -35% (de $200K a $130K).

**Por que pode ser útil:** Responde à pergunta: "qual é o pior cenário que eu teria vivido?" É crítico para dimensionar posição e avaliar viabilidade psicológica/operacional da estratégia.

**O que NÃO podemos concluir:** Que o MDD histórico é o pior que pode acontecer. O futuro pode produzir drawdowns maiores. MDD não informa sobre a frequência ou duração dos drawdowns.

---

## Walk-forward

**Definição simples:** Uma técnica de validação que simula como a estratégia seria recalibrada periodicamente ao longo do tempo, como seria feito na prática.

**Definição técnica:** Processo de validação que divide os dados em janelas: uma janela de treino (in-sample) seguida de uma janela de teste (out-of-sample). O modelo é treinado na janela de treino, testado na janela imediatamente seguinte, depois a janela avança. Repete-se até cobrir todo o período disponível. Simula o processo de re-otimização periódica.

**Exemplo:** Treino: Jan2018-Dec2019. Teste: Jan2020-Mar2020. Avança. Treino: Jan2018-Mar2020. Teste: Apr2020-Jun2020. Avança. Etc.

**Por que pode ser útil:** Mais realista do que um único split in-sample/out-of-sample. Verifica se a estratégia mantém performance ao longo do tempo com re-calibração.

**O que NÃO podemos concluir:** Que walk-forward elimina completamente o risco de overfitting. Se houver muitos parâmetros e períodos de teste pequenos, overfitting ainda é possível.

---

## Out-of-sample

**Definição simples:** Dados que o modelo nunca "viu" durante o desenvolvimento — usados para uma avaliação final imparcial.

**Definição técnica:** Partição dos dados reservada exclusivamente para avaliação final, após todo o desenvolvimento do modelo (incluindo seleção de features, ajuste de parâmetros e validação cruzada). Se o out-of-sample for "tocado" durante o desenvolvimento, ele se torna in-sample efetivamente.

**Exemplo:** Desenvolver e calibrar a estratégia em dados de 2018-2022. Fazer a avaliação final somente com dados de 2023-2024 (nunca acessados durante o desenvolvimento).

**Por que pode ser útil:** A única forma confiável de estimar performance futura genuína. Um modelo que funciona out-of-sample tem muito mais credibilidade.

**O que NÃO podemos concluir:** Que performance out-of-sample garante performance futura. Mercados mudam. Um único período out-of-sample pode ser atipicamente favorável ou desfavorável.

---

## Look-ahead bias

**Definição simples:** O erro de usar informações que não estariam disponíveis no momento da decisão, tornando o backtest artificialmente lucrativo.

**Definição técnica:** Qualquer situação onde o modelo de backtesting utiliza dados futuros (em relação ao momento da decisão simulada) para calcular sinais ou tomar decisões. Fontes comuns: usar o preço de fechamento para gerar o sinal E executar ao preço de fechamento; usar dados revisados; calcular features com toda a janela de dados disponível ao invés de apenas o passado.

**Exemplo:** Calcular a média móvel de 20 dias usando o preço de fechamento do dia D e assumir que o sinal estava disponível *antes* do fechamento de D — esse é look-ahead bias.

**Por que pode ser útil:** Compreender look-ahead bias é essencial para construir backtests válidos. Identificar e eliminar essa fonte de viés é um dos principais desafios da pesquisa quantitativa.

**O que NÃO podemos concluir:** Que um backtest sem look-ahead bias óbvio está livre do problema. Formas sutis de look-ahead bias surgem em feature engineering, normalização de dados e seleção de universo.

---

## Data leakage

**Definição simples:** A "contaminação" do modelo por informações do conjunto de teste que vazam para o processo de treinamento.

**Definição técnica:** Situação onde informações do futuro ou do conjunto de validação/teste influenciam o processo de treinamento ou seleção do modelo. Inclui: normalização calculada sobre todo o dataset (em vez de somente o treino); feature engineering que usa o target futuro; seleção de features baseada em correlação com o target calculada sobre todo o dataset.

**Exemplo:** Normalizar features com média e desvio padrão calculados sobre treino+teste (em vez de somente treino) é data leakage — o modelo "sabe" a distribuição futura dos dados.

**Por que pode ser útil:** Compreender data leakage é crítico para construir pipelines de ML para séries temporais. A distinção entre treino/validação/teste deve ser rigorosa em todas as etapas.

**O que NÃO podemos concluir:** Que ausência de data leakage óbvio garante um pipeline limpo. Leakage sutil pode surgir em joins de dados, imputação de missing values e outras transformações.

---

## Overfitting

**Definição simples:** Quando um modelo aprende padrões do conjunto de treino que são específicos daquele conjunto e não generalizam para dados novos.

**Definição técnica:** Situação onde um modelo tem alta performance in-sample mas baixa performance out-of-sample. Em séries temporais financeiras, overfitting frequentemente surge de: muitos parâmetros relativos ao número de observações; seleção de parâmetros por otimização (curve-fitting); múltiplos testes de hipóteses sem correção (data mining bias).

**Exemplo:** Uma estratégia com 12 parâmetros ajustados sobre 2 anos de dados diários (≈500 observações) tem alta probabilidade de overfitting — há parâmetros demais para poucos dados.

**Por que pode ser útil:** Compreender overfitting é o fundamento de qualquer pesquisa quantitativa séria. Princípio de Occam: entre dois modelos com performance similar, preferir o mais simples.

**O que NÃO podemos concluir:** Que um modelo com baixo número de parâmetros não está overfittado. Overfitting pode ocorrer por seleção implícita (ex.: testar 100 estratégias e apresentar apenas a melhor). A correção para múltiplos testes (ex.: Bonferroni, FDR) é fundamental.

---

*Glossário v1.0 — Market Research Lab*
