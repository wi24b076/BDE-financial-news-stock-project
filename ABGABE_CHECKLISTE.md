# Abgabe-Checkliste

## Ergebnis

Das Projekt ist inhaltlich abgabefähig. Die wichtigsten Pflichtpunkte sind abgedeckt:

- 3 unterschiedliche Datenquellen:
  - Datei: Tesla Stock CSV
  - Web Scraping: Google News RSS
  - REST API: Alpha Vantage News & Sentiment API
- Kafka Producer im Notebook `06_kafka_spark_streaming_tesla.ipynb`
- Spark Structured Streaming liest aus Kafka im Notebook `06_kafka_spark_streaming_tesla.ipynb`
- Transformierte Ergebnisse werden gespeichert:
  - `data/results/tesla_stock_news_merged.csv`
  - `data/results/tesla_kafka_stream_summary.csv`
  - Spark-Ausgaben aus Notebook 04
- Datenfluss ist im `README.md` als Mermaid-Diagramm dokumentiert
- Alle Schritte sind in Jupyter Notebooks dokumentiert

## Wichtige Korrekturen

1. README aktualisiert und vollständigen Datenfluss ergänzt.
2. REST-API-Notebook bereinigt:
   - kein hartcodierter privater API-Key mehr
   - Cache-Fallback über vorhandene Rohdaten
   - TSLA-spezifische Sentiment-Spalten aus `ticker_sentiment` extrahiert
3. Merge-Notebook korrigiert:
   - vorher verschwanden REST-API-News im finalen Merge, weil die lokale Stock-Datei früher endet
   - jetzt wird eine äußere Date-Spine verwendet, sodass Stock, Scraping und API erhalten bleiben
4. Spark-Notebook 04 rerun-sicher gemacht:
   - RDD-Ausgabeordner wird vor `saveAsTextFile` gelöscht
   - Parquet-Ausgabe nutzt `mode("overwrite")`
5. Kafka/Spark-Streaming-Notebook 06 korrigiert:
   - fehlerhafte harte Windows-JAVA_HOME-Setzung entfernt bzw. abgesichert
   - fehlende Spark-Imports ergänzt
   - Schema an neue Merge-Spalten angepasst
   - alte Error-Outputs entfernt

## Vor Abgabe noch beachten

Wenn die Lehrperson Outputs im Kafka/Spark-Notebook sehen will, Notebook 06 auf der FH/BDENG-JupyterHub-Umgebung nochmals komplett ausführen, weil der Kafka-Broker aus einer externen Umgebung nicht zuverlässig erreichbar ist.

Wenn ein PDF verlangt wird, Notebook mit sichtbaren Outputs exportieren.
