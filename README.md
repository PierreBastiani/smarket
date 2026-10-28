# Smarket

Supermarket price tracking. Scrapers collect product prices from French drive sites, and a Rust pipeline cleans them, matches each product to Open Food Facts and keeps the price history.

```
Node + Puppeteer scrapers  ->  one SQLite file per shop and run  ->  smarket-hub (Rust)  ->  MySQL (current prices) + SQLite (history)
(Carrefour, Leclerc Drive)                                                ^
                                                                          |
                                                    Open Food Facts in MongoDB, for matching
```

- Scrapers: a shared Node core (browser handling, cache, export, notifications) and one adapter per retailer.
- smarket-hub: a Rust workspace that normalizes each retailer's data, matches products against Open Food Facts and writes prices and availability over time.
- smarket-models: the shared Rust data contract (cleanup model, JSON Schema, SQL migrations).
- Infra: Docker Compose with MongoDB (the Open Food Facts dump, kept up to date with deltas) and MySQL, plus a self-hosted GitHub Actions runner.

Built in spring 2026 as private repos. I'm reworking it before publishing the code here.
