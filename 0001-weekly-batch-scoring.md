# ADR 0001: Use Weekly Batch Scoring Instead of Daily Refresh

## Context

The sales team only reviews churn predictions weekly. The system must generate predictions for approximately 120,000 customer accounts.

## Decision

We decided to refresh churn predictions once per week using a scheduled batch inference pipeline. This approach reduces infrastructure cost and operational complexity while still satisfying business requirements.

## Alternatives rejected

* Daily refresh: rejected because the business team does not require daily updates.
* Real-time online inference: rejected because churn predictions are not user-facing and do not require low latency.
* Streaming inference: rejected because continuous event processing would unnecessarily increase system complexity.

## Consequences

* Lower infrastructure and compute costs.
* Simpler deployment and monitoring workflows.
* Predictions may become slightly outdated during the week.

## Revisit if

Reconsider this decision if the business later requires near real-time churn alerts or daily account risk updates.
