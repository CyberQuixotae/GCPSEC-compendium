[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/87/video/450292) <!--Increment the end number by 1 for the duration of each numbered section!-->

# Auditing Cloud Data

### Auditing storage buckets
- Cloud Storage bucket administrative activity is logged automatically: Logs of bucket data access must be turned on.

### Enable logging within a bucket
- Make a bucket to hold the logs.
- Allow write access to the bucket.
- Set logging on and specify the log bucket:
    - Storage logs are created once a day
    - Usage logs are created every hour

```shell
    gcloud storage buckets create gs://example-logs-bucket
    gsutil acl ch -g cloud-storage-analytics@google.com:W gs://example-logs-bucket
    gsutil defacl set project-private gs://example-logs-bucket
    gsutil logging set on -b gs://example-logs-bucket gs://example-bucket
```

### Export the logs to BigQuery for analysis
- Create a BigQuery dataset.
- Use a load job to copy log data into BigQuery tables.

```shell
$   bq mk storageanalysis
$   bq load --skip_leading_rows=1 storageanalysis.usage gs://example-logs-bucket/example-bucket_usage_2018_01_15_14_00_00_1702e6_v0 ./cloud_storage_usage_schema_v0.json

$   bq load --skip_leading_rows=1 storageanalysis.storage gs://example-logs-bucket/example-bucket_storage_2018_01_05_14_00_00_091c5f_v0 ./cloud_storage_storage_schema_v0.json
```
