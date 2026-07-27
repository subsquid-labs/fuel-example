# fuel-example

> **⚠️ Data source discontinued.** The SQD Network gateway and Portal dataset for
> Fuel have been retired — `https://v2.archive.subsquid.io/network/fuel-mainnet`
> and `https://portal.sqd.dev/datasets/fuel-mainnet` both return 404. As a result
> **this template can no longer sync from SQD infrastructure.** It is kept for
> reference and still builds, but it will not ingest data without an alternative
> source. See the deprecation announcement:
> https://docs.sqd.dev/announcements/gateway-deprecations-may-2026

This project shows how one can index Fuel network using Subsquid SDK.

## Getting started

### Prerequisites

* Node.js (version 20.x and above)
* Docker

### Run indexer

```bash
# Install dependencies
npm i

# Compile the project
npx tsc

# Launch Postgres database to store the data
docker compose up -d

# Apply database migrations to create the target schema
npx squid-typeorm-migration apply

# Run indexer
node -r dotenv/config lib/main.js

# Checkout indexed logs
docker exec "$(basename "$(pwd)")-db-1" psql -U postgres \
  -c "SELECT id, logs_count, found_at FROM contract ORDER BY logs_count desc LIMIT 10"
```

Visit the documentation page for more details on using subsquid for Fuel.
