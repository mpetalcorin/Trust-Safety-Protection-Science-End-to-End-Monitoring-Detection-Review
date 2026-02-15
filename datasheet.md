# Data Sheet, Synthetic Trust & Safety Telemetry Dataset
## Dataset Summary
This dataset is a synthetic, notebook-generated collection of product telemetry events designed to demonstrate Trust & Safety workflows, including monitoring, detection, human review operations, and incident response.

It is intended for:
- demonstrations,
- prototyping pipeline logic,
- and portfolio-style examples.

It is not derived from real users.
## Motivation
Real Trust & Safety systems are built on:
- raw event logs,
- reliable core tables,
- monitoring dashboards,
- detection models,
- and operational review workflows.

This synthetic dataset provides a safe way to illustrate that full workflow without using sensitive data.

## Composition

### Raw events table
Saved as:
- `out_notebook/raw_events.csv`

**Columns**
- `event_id`: unique event identifier
- `ts`: timestamp (UTC)
- `user_id`: synthetic user identifier
- `ip`: synthetic IP string
- `device_id`: synthetic device identifier
- `payment_id`: synthetic payment token (may be null)
- `surface`: e.g., web, ios, android, api
- `product`: e.g., chat, assistants, files, images
- `event_type`: signup, login, chat, upload, billing, policy_block, warning
- `prompt`: text field for chat events (synthetic)
- `tokens_in`, `tokens_out`: simulated token counts
- `latency_ms`: simulated request latency
- `blocked`: 0/1 event-level indicator
- `warned`: 0/1 event-level indicator
- `is_abuse_gt`: 0/1 synthetic ground-truth label (simulated)

### Core tables (SQLite)
Saved in:
- `out_notebook/sqlite.db`

Tables include:
- `raw_events`
- `core_users` (user aggregates)
- `core_user_day` (user-day aggregates)
- `core_day_metrics` (daily monitoring metrics)

### Derived exports
- `monitoring_metrics.csv`
- `alerts.csv`
- `user_day_scored.csv`
- `review_queue.csv`
- `audit_log_template.csv`
- `review_queue_dedup.csv`
- `clusters.csv`
- `entity_resolution_edges.csv`
- `entity_resolution_components.csv`
- `enforcement_actions.csv`
- `incident_log.csv`

## Data Generation Process
The notebook:
1) creates a population of synthetic users,
2) assigns a small fraction as abuse-like users,
3) generates events over a multi-day window,
4) injects patterns commonly associated with abuse, such as bursts, repeated prompts, policy-evasion attempts, and shared identifiers to mimic coordinated actors,
5) derives core tables and features for detection and monitoring.

The generation uses fixed random seeds to support reproducibility.

## Uses
**Appropriate uses**
- demonstration of SQL core tables and monitoring,
- prototyping a detection workflow and evaluation loop,
- building a human review queue and audit logs,
- illustrating deduplication, clustering, and entity resolution,
- drift monitoring examples.

**Inappropriate uses**
- any attempt to infer behavior about real people,
- claims about real-world abuse rates,
- training production systems without real data governance and evaluation.

## Labeling
`is_abuse_gt` is synthetic ground truth assigned by the generator. It is not created by human labeling and does not represent the complexity of real Trust & Safety adjudication.

## Privacy and Sensitive Data
This dataset contains no real personal data. All identifiers and prompts are synthetic. If adapting this workflow to real data, implement:
- data minimization,
- access controls,
- retention policies,
- privacy review and compliance.

## Known Limitations
- Simulated patterns are simplified compared to real adversarial behavior.
- The synthetic label is not noisy like real labels, and may overstate model performance.
- Limited variety of event types and abuse modalities.
- Not calibrated to any specific product or policy taxonomy.

## Maintenance
The dataset is generated on demand by running the notebook. There is no ongoing data collection.

## How to Reproduce
Run the notebook top-to-bottom. Outputs are written into:
- `out_notebook/`

## Contact
Repository: Github https://github.com/mpetalcorin/Trust-Safety-Protection-Science-End-to-End-Monitoring-Detection

