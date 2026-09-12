Platform engineer focused on ingestion pipelines and data infrastructure.

## Emmalee Yundt

I build and operate ingestion systems that move tens of millions of events per day through queues, workers, and object storage. I own the full lifecycle: schema design, partition tuning, retry semantics, and the runbooks that keep the pipeline alive during partial outages. I prioritize durable writes and idempotent consumers over low latency, and I accept the operational cost of backpressure and replay windows to avoid silent data loss.

### 🛠 Tech & Infrastructure
- **Core**: `Python`, `PostgreSQL`, `Redis`, `Kafka`
- **Data**: `Parquet`, `Avro`, `S3`, `Snowflake`
- **Infra**: `Docker`, `Kubernetes`, `Terraform`
- **Tooling**: `pytest`, `ruff`, `Prometheus`, `Grafana`

### ⚙️ Engineering Areas
- Designing idempotent ingestion workers with exactly-once processing semantics using transactional outboxes and deduplication keys.
- Partitioning Kafka topics by tenant and time to bound consumer lag and enable independent replay per shard.
- Building schema validation gates that reject malformed events before they enter the warehouse, with clear error payloads for upstream teams.
- Tuning autoscaling policies for consumers based on queue depth and lag metrics, not CPU or memory.

### 🔭 Current Focus
- Reducing end-to-end ingestion latency from 5 minutes to under 60 seconds without sacrificing exactly-once guarantees.
- Migrating from a monolithic batch loader to a stream-native architecture while keeping the existing warehouse schema stable.
- Implementing a backpressure mechanism that pauses upstream producers when downstream storage degrades, instead of dropping events.
- Introducing column-level lineage tracking to trace a single event from ingestion to final table, for audit and debugging.

### 📌 Engineering Notes
- Tests that don't include failure injection for network timeouts, queue outages, and duplicate deliveries are not testing the system.
- Migrations should be additive, backward-compatible, and reversible; never rewrite a schema in one deployment.
- Retries belong at the edge with exponential backoff and jitter; internal retries should be rare and always idempotent.
- Every deployment must be observable: metrics on lag, error rates, and replay progress, plus a runbook that matches the dashboard.

### 🧭 How I Work
- Prefer small, reversible changes over big-bang rewrites; keep the pipeline green at every commit.
- Write operational documentation at the same time as the code, so the runbook is not an afterthought.
- Default to boring, proven technology; introduce novelty only when it solves a measured problem.

*Reliability is a feature, and it ships in the retry logic, not the roadmap.*