# 04 - Azure Monitoring

This section documents the monitoring and observability configuration implemented in the Azure environment.

## Objectives

- Configure Azure Monitor
- Collect VM performance metrics
- Send monitoring data to Log Analytics
- Create a CPU usage alert

## Implementation

### Log Analytics

- Created a Log Analytics workspace: `law-portfolio`
- Resource group: `rg-security`
- Region: Denmark East

### Data Collection

- Created a Data Collection Rule: `dcr-portfolio-vm`
- Associated the rule with `vm-portfolio`
- Configured CPU and memory performance counters
- Sent collected data to `law-portfolio`
- Verified data collection using a KQL query against the `Perf` table

### Alerting

- Created a metric alert rule: `alert-vm-portfolio-high-cpu`
- Monitored metric: Percentage CPU
- Threshold: Greater than 80%
- Aggregation: Average
- Evaluation frequency: 5 minutes
- Lookback period: 5 minutes
- Severity: Sev 3 - Informational
- Action group: None

## Cost Management

- The virtual machine is deallocated when not in use to reduce compute costs.
- Log Analytics ingestion and alert rules may incur charges.

## Status

Completed
