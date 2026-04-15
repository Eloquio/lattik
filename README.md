# Lattik

Open-source data platform by [Eloquio](https://github.com/Eloquio). Lattik combines an agentic analytics studio, a columnar stitch engine, and an expression language into a unified stack for building and operating data pipelines on top of S3 + Iceberg.

## Repositories

| Repository | Description | Language |
|---|---|---|
| [lattik-studio](https://github.com/Eloquio/lattik-studio) | Agentic analytics platform — chat-driven data pipelines, business questions, root cause analysis, and ML feature engineering | TypeScript (Next.js) |
| [lattik-stitch](https://github.com/Eloquio/lattik-stitch) | Read-side engine for Lattik Tables — stitches N column families from S3 into a single logical Iceberg table, with Spark and Trino connectors | Rust, Kotlin, Java |
| [lattik-expression](https://github.com/Eloquio/lattik-expression) | Expression language for parsing, type-checking, and emitting SQL expressions against a known schema | TypeScript |

## Getting started

### System requirements

- macOS, Linux, or Windows (WSL2)
- 12+ GB RAM recommended (8 GB minimum — the full stack runs ~10 services in a local Kubernetes cluster)
- 20+ GB free disk space (Docker images, kind PVCs)

### Prerequisites

- [Docker](https://docs.docker.com/get-docker/) (make sure Docker Desktop is running)
- [kind](https://kind.sigs.k8s.io/) (Kubernetes in Docker)
- [Node.js](https://nodejs.org/) 22+
- [pnpm](https://pnpm.io/) 10+
- [portless](https://github.com/nicolo-ribaudo/portless) (`npm install -g portless`)
- [helm](https://helm.sh/) (for Spark Operator)

### Setup

```bash
# Start the HTTPS proxy (requires sudo for port 443 — serves lattik-studio.dev)
sudo portless proxy start --tld dev

# Clone
git clone --recurse-submodules https://github.com/Eloquio/lattik.git
cd lattik/lattik-studio

# Install dependencies
pnpm install

# Start everything — preflight checks, environment setup, services, and dev server
pnpm dev:up
```

`pnpm dev:up` runs through these phases automatically:

1. **Preflight checks** — validates Docker, kind, helm, Node, pnpm, RAM, disk, and port availability
2. **Environment bootstrap** — generates `apps/web/.env` (prompts for your AI Gateway key, auto-generates all secrets)
3. **Required services** — creates the kind cluster, starts PostgreSQL, pushes the DB schema, and seeds data
4. **Dev server** — starts the Next.js app at https://lattik-studio.dev
5. **Background services** — builds images and starts Gitea, Trino, MinIO, Kafka, Spark, Airflow, etc. (progress logged to `.dev-services.log`)

First run takes **15-20 minutes** (image builds + container pulls). Subsequent runs take ~2 minutes.

Sign in with **admin / admin** — no Google OAuth setup required for local development.

### Verify

Check the status of all services at any time:

```bash
pnpm dev:status
```

### Teardown

```bash
pnpm dev:down   # Deletes the kind cluster — all data is wiped
```

## License

Apache License 2.0 — see [LICENSE](LICENSE) for details.
