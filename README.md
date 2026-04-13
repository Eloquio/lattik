# Lattik

Open-source data platform by [Eloquio](https://github.com/Eloquio). Lattik combines an agentic analytics studio, a columnar stitch engine, and an expression language into a unified stack for building and operating data pipelines on top of S3 + Iceberg.

## Repositories

| Repository | Description | Language |
|---|---|---|
| [lattik-studio](lattik-studio) | Agentic analytics platform — chat-driven data pipelines, business questions, root cause analysis, and ML feature engineering | TypeScript (Next.js) |
| [lattik-stitch](lattik-stitch) | Read-side engine for Lattik Tables — stitches N column families from S3 into a single logical Iceberg table, with Spark and Trino connectors | Rust, Kotlin, Java |
| [lattik-expression](lattik-expression) | Expression language for parsing, type-checking, and emitting SQL expressions against a known schema | TypeScript |

## Getting started

Clone with submodules:

```bash
git clone --recurse-submodules https://github.com/Eloquio/lattik.git
```

Or if already cloned:

```bash
git submodule update --init --recursive
```

See each repository's README for setup instructions.

## License

Apache License 2.0 — see [LICENSE](LICENSE) for details.
