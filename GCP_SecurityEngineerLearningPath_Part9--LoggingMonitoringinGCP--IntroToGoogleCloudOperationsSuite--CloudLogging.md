[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/99/video/432481)

# Cloud Logging
- Allows users to collect, store, search, analyze, monitor, and alert on log entries and events.
    - Automated logging is integrated into Google Cloud products like App Engine, Cloud Run, Compute Engine VMs running the logging agent, and GKE.
- Provides automatic ingestion with simple controls for routing, storing, and displaying your log data.
- Leverage tools like Log Analytics to view trends, or Error Reporting and Log Explorer to quickly examine problems.

## Logging has multiple aspects

#### Collect
- Cloud events, configuration changes, and data from customer services
- Logs at various levels of the resource hierarchy

#### Analyze
- Log data in real time with the integrated Logs Explorer
- Exported logs from Cloud Storage or BigQuery

#### Export
- Export to Cloud Storage, Pub/Sub, or BigQuery
- Logs-based metrics for augmented monitoring

#### Retain
- Data access and service logs for 30 days and admin logs for 400 days
- Longer-term in Cloud Storage or BigQuery

## Developer use cases
- Integration into popular SDKs - Get started quickly with a large collection of system metrics and logs
- Real time log analysis - Analyze log data in real time, debug code, troubleshoot your apps
- Quick error detection - Find errors via stack traces automatically with Error Reporting

## Operator use cases
- Collect the right telemetry - Instrumentation for GCE, on-premises, and other cloud providers
- Centralize logs - Centralize logs for specific users, teams, and/or organizations
- Manage logs - Set retention periods, select supported regions for regional data storage
- Set alerts - Understand log volume/cost, set alerts on important application metrics
- Export logs - Export to Google Cloud for storage, analysis, and integration with 3rd parties

## Security operations use cases
- Collect audit logs - Collect Google Cloud audit logs by default, advanced security logs such as data access logs
- Collect network telemetry data - Collect and analyze VPC flow logs, GKE network, firewall, load balancer logs
- Analyze logs for security events - View audit logs and other events to investigate possible security events

