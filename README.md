# BDE Financial News & Stock Project – Tesla

This project looks at Tesla stock data together with Tesla-related financial news.

The main idea was to build a small Big Data Engineering pipeline and check how stock data, scraped news and API-based sentiment data can be combined and processed.

## Project idea

We wanted to answer the following question:

> What can we observe when Tesla stock prices are combined with Tesla-related news volume and sentiment?

The goal was not to predict the stock price. The focus was on collecting data from different sources, cleaning it, merging it, sending it through Kafka and processing it with Spark.

## Data sources

| Type | Source | Used for |
|---|---|---|
| File | Tesla stock CSV | Historical Tesla stock prices |
| Web scraping | Google News RSS | Tesla-related news headlines |
| REST API | Alpha Vantage News & Sentiment API | News sentiment and relevance for TSLA |

## Data flow

```mermaid
flowchart LR
    A[Tesla stock CSV] --> B[Clean stock data]
    C[Google News RSS] --> D[Clean scraped news]
    E[Alpha Vantage API] --> F[Clean API sentiment data]

    B --> G[Merge by date]
    D --> G
    F --> G

    G --> H[Final merged CSV]
    H --> I[Kafka Producer]
    I --> J[Kafka Topic]
    J --> K[Spark Streaming]
    K --> L[Stream summary result]