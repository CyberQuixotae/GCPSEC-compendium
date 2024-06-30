[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/99/video/432505)

# Cloud Logging overview and architecture

## Cloud Logging help you understand your application
- **Gather data from various workloads**: Gathers the information required to troubleshoot and understand the workload and application needs
- **Analyze large volumes of data**: Tools like Error Reporting, Log Explorer, and Log Analytics let you drive insights from large sets of data
- **Route and store logs**: Route your logs to the region or service of your choice for additional compliance or business benefits.
- **Get Compliance Insights**: Leverage audit app logs for compliance patterns and issues

## Cloud Logging Architecture
Cloud Logging architecture consists of the following components:
    - Log collection: These are the places where log data originates.
        - Log sources can be Google Cloud services, such as Compute Engine, App Engine, and Kubernetes Engine, or your own applications.
    - Log routing: Responsible for routing log data to its destination.
        - The Log Router uses a combination of inclusion filters and exclusion filters to determine which log data is routed to each destination.
    - Log sinks: Destinations where log data is stored.
        - Cloud Logging supports a variety of log sinks, including Cloud Logging log buckets, Cloud Pub/Sub topics, BigQuery, cloud storage bucket.
    - Log analysis:
        - logs explorer is optimized for troubleshooting use cases with features like log streaming.
        - error reporting helps users react to critical application errors through automated error grouping and notifications.
        - logs-based metrics, dashboards, and alerting provide other ways to understand and make logs actionable.
        - log analytics feature expands the toolset to include ad hoc log analysis capabilities.

