[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/99/video/432515)

# Cloud Audit Logs
- In terms of sheer volume of useful information, probably the most important group of logs in Google Cloud are the Cloud Audit Logs.

## Cloud Audit Logs: "Who did what, where, and when?"
- **Admin Activity audit logs**: Record modifications to configuration or metadata.
    - For example, these logs record when users create VM instances or change Identity and Access Management permissions.
    - They are always on, are retained for **400 days**, and are available at no charge.
- **System Event audit logs**: Record Google CLoud non-human admin actions that modify configurations.
    - They are always enabled, free, retained for **400 days**.
    - To view these logs, you must have the IAM role Logging/Logs Viewer or Project/Viewer.
- **Data Access audit logs**: Record calls that read metadata, configurations, or that create, modify, or read user-provided data.
    - They are disabled by default (except for BigQuery), and when enabled, the default retention is **30 days**.
    - To view these logs, you must have the IAM roles Logging/Private Logs Viewer or Project/Owner.
- **Policy Denied audit logs**: Record a security policy violation.
    - You can't disable Policy Denied audit logs.However, you can use exclusion filters to prevent these logs from being ingested and stored in Cloud Logging.

## Filtering audit logs
- To view and filter audit logs: Navigate to **Logs Explorer Filter** by using the **Log name drop-down menu**.
    - Typing cloudaudit into the filter box is frequently quicker than scrolling.
    - This query is auto populated in the query section when using the UI.

## Access Transparency logs
- Show **how** and **why** customer data is accessed after it is stored in Google Cloud.
    - Log access actions.
    - Track actions by **Google personnel**.
    - Support approval and events are surfaced through Security Command Center and apps' APIs and UIs.

