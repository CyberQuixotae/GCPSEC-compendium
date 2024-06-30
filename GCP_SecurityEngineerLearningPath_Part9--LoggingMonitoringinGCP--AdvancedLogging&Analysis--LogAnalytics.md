[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/99/video/432510)

# Log Analyitcs
Log Analytics gives you the analytical power of BigQuery within the Cloud Logging console and provides you with a new user interface that's optimized for analyzing your logs.

When you create a bucket and activate analytics on it, Cloud Logging makes the logs data available in both the new Log Analytics interface and BigQuery; you don't have to route and manage a separate copy of the data in BigQuery.

## Cloud Logging and Log Analytics use cases
- **Troubleshooting**: Get to the root cause with search, filtering, histogram, and suggested searches.
- **Log Analyisis**: Analyze application performance, data access and network access patterns.
- **Reporting**: Use the logs data in Log Analytics directly from BigQuery to report on aggregated application.

## How different is analytics-enabled bucket log data from logs routed to BigQuery
- Log data in BigQuery is managed by Cloud Logging.
- BigQuery ingestion and storage costs are included in your Logging costs.
- Data residency and lifecycle are managed by Cloud Logging.

## Create a log-analytics enabled bucket
1. Create a log bucket with Log Analytics enabled.
2. Create a sink to route logs to the newly created bucket.
3. Check **Upgrade to use Log Analytics.**
- You can't downgrade the log bucket to remove the use of Log Analytics

### Log Analytics use cases
- **DevOps**: Reduce MTTR by using advanced analytical capabilities to diagnose issues. "Help me quickly troubleshoot an issue by looking at the top count of requests grouped by response type and severity"
- **Security**: Investigate security-related attacks with queries over large volumes of security logs.
"Help me find all audit logs associated with a specific user over the past month"
- **IT or Network Operations**: Provide better network insight and management through advanced log aggregation capabilities
"Help me identify network issues for GKE instances using VPC and firewall rules"

