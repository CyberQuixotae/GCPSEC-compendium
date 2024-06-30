[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/99/video/432516)

# Data Access audit logs

## Enabling Data Access audit logs in the organization
- Data Access audit logs can be enabled at different levels:
    - **Organization**
    - **Folder**
    - **Project**
    - **Resource**
    - **Billing accounts**
- You can even exempt principals from recording data access logs.
- Final scope is the union of the configurations
    - For example, at a project level, you can enable logs for a Google Cloud service.
    - But you can't disable logs for a Google Cloud service that is enabled in a parent organization or folder.
    - The added logging does add to the cost, currently: $0.50 per gigabyte for ingestion.
    - Data Access audit logs are disabled by default, for everything but BigQuery.
    - They may be enabled and configured at the organization, folder, project, or service level.

## Enabling Data Access access logs per Google Cloud service
- Data Access logs can be enabled and configured at the service level
- You can control what type of information is recorded in the Data Access audit logs.

There are three types of Data Access audit logs information:
    - **Admin-read** records operations that read **metadata** or **configuration** information.
        - For example, you looked at the configurations for your bucket.
    - **Data-read** records operations that read user-provided data.
        - For example, you listed files and then downloaded one from Cloud Storage.
    - **Data-write** records operations that write user-provided data.
        - For example, you created a new Cloud Storage file.

## Exempt specific users or groups
- **You can exempt specific users or groups from having their data accesses recorded**
- This functionality comes in handy when you want to reduce the cost and noise associated with the volume of logs that are not of your interest.

## Programatically enabling Data Access audit logs
**Step 1** `gcloud projects get-iam-policy [project-id] > policy.yaml`
**Step 2**
```yaml
auditConfigs:
- auditLogConfigs:
- logType: ADMIN_READ
- logType: DATA_WRITE
service: run.googleapis.com #Could also be all Services bindings:
- members:
etc...
```
**Step 3** `gcloud projects set-iam-policy [project-id] policy.yaml`


