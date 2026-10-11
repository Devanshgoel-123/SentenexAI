# SentenexAI

### Sentiment and on-chain analyzer for perpetual trading on Aptos

![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?logo=fastapi&logoColor=white)
![OpenAI](https://img.shields.io/badge/GPT--4o-412991?logo=openai&logoColor=white)
![Aptos](https://img.shields.io/badge/Aptos-000?logo=aptos&logoColor=white)

This repo is the standalone Python service behind **Sentenex**. It combines CoinMarketCap market data, GPT-4o sentiment analysis, and Aptos on-chain metrics into a LONG / SHORT / HOLD recommendation, with a confidence score and suggested leverage.

The full app (React dashboard, plus an Express backend that executes trades on Kana Perps) is in **[AptosHack](https://github.com/Devanshgoel-123/AptosHack)**.

The complete service documentation (setup, endpoints, polling, and examples) is in **[Sentenex-main/README.md](Sentenex-main/README.md)**.

```mermaid
flowchart LR
    Req["POST /api/analyze<br/>{token, amount}"] --> MD["market_data.py<br/>CoinMarketCap"]
    Req --> SA["sentiment_analyzer.py<br/>GPT-4o"]
    Req --> OC["aptos_analyzer.py<br/>on-chain"]
    MD & SA & OC --> DE["decision_engine.py<br/>weighted score"]
    DE --> Out["LONG / SHORT / HOLD<br/>confidence · leverage · PnL estimate"]
    DE --> PM["position_manager.py<br/>stop-loss · take-profit"]
```

## Quick start

```bash
cd Sentenex-main
pip install -r requirements.txt
printf "CMC_API_KEY=...\nOPENAI_API_KEY=...\n" > .env
python app.py            # http://localhost:8000/docs
```
