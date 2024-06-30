[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/99/video/432479)

# Need for Google Cloud observability
- You can't physically inspect your Cloud assets.

## Need for observability
**Visibility into system health**: Help me understand my application and tell me if it's healthy

**Error reporting and alerting**: Bring problems directly to my attention

**Efficient troubleshooting**: Help me fix it if it's broken

**Performance improvement**: Guide me to optimize it

## Monitoring gives you real-time systems information
In Google's Site Reliability Engineering book, which is available to read at (landing.google.com/sre/books), monitoring is defined as collecting, processing, aggregating, and displaying **real-time quantitative data about a system**, such as:
- Query counts and types
- Error counts and types
- Processing times
- Server lifetimes

## Monitoring is the foundation of product reliability

## Whats needed from products
- Continual improvement
- Dashboards
- Automated alerts
- Incident response

## Four Golden Signals
- Latency
- Traffic
- Saturation
- Errors

## The importance of latency
01. Changes in latency could indicate emerging issues.
02. Its values may be tied to capacity demands.
03. It can be used to measure system improvements.
    - Page loads latency
    - Number of requests waiting for

## The importance of traffic
01. It's an indication of current system demand.
02. Its historial trends are used for capacity planning.
03. Its a core measure when calculating infrastructure spend.
    - # of retrievals per second
    - # active requests

## The importance of saturation
01. It's an indication of current system demand.
02. It focuses on the most constrained resources.
03. It's frequently tied to degrading performance as capacity is reached.
    - % memory utlization
    - % thread pool utilization

## The importance of errors
01. They may indicate configuration or capacity issues.
02. They can indicate service level objective violations.
03. An error might mean it's time to send out an alert.
    - # failed requests
    - # exceptions

## Capture Signals
- Metrics
- Logs
- Trace

## Visualize and Analyze
- Dashboards
- Metrics Explorer
- Logs Explorer
- Service Monitoring
- Log Analytics
- Health Checks
- **Troubleshoot**

## Manage Incidents
- Alerts
- Error Reporting
- SLO

## Google Cloud's operations suite
- **Cloud Monitoring**
- **Cloud Logging**
- **Error Reporting**
- **Cloud Trace**
- **Cloud Profiler**

