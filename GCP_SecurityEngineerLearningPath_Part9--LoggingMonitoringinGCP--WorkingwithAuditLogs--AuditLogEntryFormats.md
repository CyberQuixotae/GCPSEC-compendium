[Lesson Link:](https://www.cloudskillsboost.google/paths/15/course_templates/99/video/432517)

# Audit logs entry format
- Every audit log entry in Cloud Logging is an object of type `LogEntry`.
- Identify the resource generating log by looking at the `producer` field.
- What distinguishes an audit log entry from other log entries is the `protoPayload` field, which contains an `AuditLog` object that stores the audit logging data.
- Identify the principal generating log by looking at the `principalEmail`.
