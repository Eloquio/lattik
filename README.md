# Lattik

Open-source data platform by [Eloquio](https://github.com/Eloquio). Lattik combines an agentic analytics studio, a columnar stitch engine, and an expression language into a unified stack for building and operating data pipelines on top of S3 + Iceberg.

## Repositories

| Repository | Description | Language |
|---|---|---|
| [lattik-studio](https://github.com/Eloquio/lattik-studio) | Agentic analytics platform — chat-driven data pipelines, business questions, root cause analysis, and ML feature engineering | TypeScript (Next.js) |
| [lattik-stitch](https://github.com/Eloquio/lattik-stitch) | Read-side engine for Lattik Tables — stitches N column families from S3 into a single logical Iceberg table, with Spark and Trino connectors | Rust, Kotlin, Java |
| [lattik-expression](https://github.com/Eloquio/lattik-expression) | Expression language for parsing, type-checking, and emitting SQL expressions against a known schema | TypeScript |

## Getting started

### Prerequisites

- [Docker](https://docs.docker.com/get-docker/)
- [kind](https://kind.sigs.k8s.io/) (Kubernetes in Docker)
- [Node.js](https://nodejs.org/) 22+
- [pnpm](https://pnpm.io/) 10+
- [portless](https://github.com/nicolo-ribaudo/portless) (`npm install -g portless`)
- [helm](https://helm.sh/) (for Spark Operator)

### Clone

```bash
git clone --recurse-submodules https://github.com/Eloquio/lattik.git
cd lattik
git submodule foreach git checkout main
```
### Setup

All commands below run from the `lattik-studio/` directory:

```bash
cd lattik-studio

# Install dependencies
pnpm install

# Generate .env (prompts for your AI Gateway key, auto-generates all secrets)
pnpm env:bootstrap

# Start the portless proxy (requires sudo for port 443)
portless proxy start --tld dev

# Bring up the full dev stack (kind cluster, Postgres, Gitea, Trino, MinIO, etc.)
pnpm dev:up

# Start the dev server (serves at https://lattik-studio.dev)
pnpm dev
```

Sign in with **admin / admin** — no Google OAuth setup required for local development.

## License

Apache License 2.0 — see [LICENSE](LICENSE) for details.
