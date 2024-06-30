[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/864/video/467967)

# Non-VM resources

## Services with built-in logging and monitoring support
- [Monitored resource types](https://cloud.google.com/monitoring/api/resources)
When monitoring any of the following non-virtual machine systems in Google Cloud,
the Ops Agent is not required, and should not be installed:

- App Engine standard environment has monitoring built-in.
- App Engine flexible environment is built on top of GKE; has Monitoring agent pre-installed and configured.
- With Standard Google Kubernetes Engine nodes (VMs), Cloud Monitoring and Cloud Logging is enabled by default.
- Cloud Run and Cloud Function provides integrated monitoring support.

## App Engine
- Standard and flexible environments support Cloud Monitoring.

### Standard and flexible environments support Cloud Logging.
- Support writing to `stdout` or `stderr` from code.
- Support language-specific logging APIs (like Winston on Node.js).
- Let you view logs under GAE Application resource

## Monitoring and logging in Cloud Functions
- Cloud Functions monitoring is **automatic** and can privde you with access to invocations, execution times, memory usage, and active instances in the Google Cloud console.
- Metrics also available in Cloud Monitoring, where you can set up custom alerting and dashboards.
- Cloud Functions also support simple logging by default. Logs written to standard out or standard error will appear automatically in the Google Cloud console. Logging API can also be used by extending log support.

## Monitoring and logging in Cloud Run
- **Cloud Run** is Google's managed container service.
- **Two** types of logs automatically sent to Cloud Logging:
    - **Request Logs** are logs of requests sent to Cloud Run services.
    - **Container logs** are logs emitted from the container instances from your own code, written to standard out or standard error streams, or using the logging API.

- Cloud Run is automatically integrated with Cloud Monitoring with **no setup or configuration required**
- Metrics of your Cloud Run services are captured automatically
- You can view metrics either in Cloud Monitoring or on Cloud Run page in the console. Cloud Monitoring provides more charting/filtering options.



### Resource type - Cloud Run vs Cloud Run for Anthos
- For fully managed Cloud Run, the monitoring resource name is "Cloud Run Revision" (cloud_run_revision).
- For Cloud Run for Anthos, the monitoring resource name is "Cloud Run on GKE Revision" (knative_revision).


