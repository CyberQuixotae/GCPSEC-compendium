[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/864/video/467977)

# Load Balancer logs

## Load balancers support for Cloud Logging
- All the Google Cloud load balancers support Cloud Logging and Cloud Monitoring. Log type and log fields vary based on the type of load balancers. These include:
    - Internal and External HTTP(S) load balancers
    - Internal and External TCP/UDP Network load balancers
    - External SSL Proxy and TCP Proxy load balancers
    - Internal TCP Proxy load balancers

- The log type, log fields, and metrics supported vary based on the the load balancer type.
- Load balancing logs is used to debug and analyze user traffic

## The internal and external HTTP(S) load balancers support logging
- **Activated and deactivated on a per backend service basis**
    - For external HTTP(S) load balancers with backend buckets, logging is automatically enabled and cannot be deactivated.
        - Backends created before the Globally Available (GA) release of load balancer logging might require manual configuration
    - Logging can be enabled on a per backend service basis.
    - URL map might reference more than one backend service.
    - Use exclusion, if you do not want the logs to be stored in Cloud Logging.

## Fields in a log record
- LogEntry format includes general information shown in most logs, such as
severity, project ID, project number, timestamp, etc.
- However, HttpRequest.protocol is not populated for HTTP(S) load balancing
logs. This can include a method, a URL, remote IP address, a protocol, a
latency string or a user agent.
- Resource contains the monitored resource type associated with the log entry.
- jsonPayload contains the statusDetails field. This field holds a string that
explains why the load balancer returned the HTTP status that it did.
- Redirects (such as HTTP response status code 302 Found) issued from the
load balancer are not logged. Redirects issued from the backend instances
are logged
- [Global external Application Load Balancer logging and monitoring](https://cloud.google.com/load-balancing/docs/https/https-logging-monitoring#what_is_logged)

## Example of using a load balancing log record
- Consider a scenario where the load balancer generates an HTTP error resource code `5XX` and sends the same error code to the client.
- Refer to Load Balancer logs to determine the source of error.
    - `statusDetails field: response_sent_by_backend` indicates it is a backend issue.
    - `statusDetails field: failed_to_pick_backend` indicates that the load balancer failed to pick a healthy backend to handle a request.
