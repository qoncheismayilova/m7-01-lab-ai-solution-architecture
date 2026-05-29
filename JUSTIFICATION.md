# System Justification

## Serving Pattern

I selected a batch serving pattern because the business scenario only requires churn scores to refresh once per week. The sales team revisits the predictions during the week, but the scores do not need real-time updates. This makes batch inference more cost-efficient and operationally simpler than online serving.

The system processes approximately 120,000 accounts weekly. Since predictions are generated on a fixed schedule every Monday morning, low-latency online inference is unnecessary.

## Inference Location

Inference runs in the cloud. Batch jobs are executed in a centralized cloud environment where compute resources can scale during weekly prediction runs. Cloud inference simplifies model deployment, monitoring, and retraining workflows.

Edge inference is unnecessary because sales representatives access predictions through a CRM dashboard rather than mobile or offline systems.

## Optimization Targets

The system primarily optimizes for:

* Cost efficiency
* Reliability

Latency is less critical because predictions are not user-facing in real time. The main operational requirement is that all predictions are available before Monday morning business hours.

The throughput target is processing all 120,000 accounts within a scheduled batch window.

## Fallback Strategy

If the ML model becomes unavailable, the system falls back to the previous week's churn predictions stored in the predictions database.

If model quality degrades, monitoring alerts trigger retraining or rollback to a previous stable model version from the model registry.

This ensures the sales team can continue outreach operations even during ML system failures.
