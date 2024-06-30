[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/99/video/432491)

# Query metrics
- Cloud Monitoring supports two query languages:
    - **MQL** and **PromQL**

## MQL
- Query Cloud Monitoring time-series data by using the text-based interface
- Manipulate, retrieve, and perform complex operations on time-series data

## PromQL
- Query metrics from Google Cloud Managed Service for Prometheus
- Query system metrics from GKE and Compute Engine
- Integrate with Grafana to chart metrics
    - You can use PromQL to query and chart Cloud Monitoring data from the following sources:
        - Google Cloud services, like Google Kubernetes Engine or Compute Engine, that **write metrics described in the lists of Cloud Monitoring system metrics**.
        - User-defined metrics, like log-based metrics and Cloud Monitoring user-defined metrics.
        - Google Cloud Managed Service for Prometheus, the fully managed multi-cloud solution for Prometheus from Google Cloud.

## Why use MQL?
- Create ratio-based charts and alerts
- Perform time-shift analysis (compare metric data week over week, month over month, year over year, etc.)
- Apply mathematical, logical, table operations, and other functions to metrics
- Fetch, join, and aggregate over multiple metrics
- Select by arbitrary, rather than predefined, percentile values
- Create new labels to aggregate data by, using arbitrary string manipulations including regular expressions.

## MQL example to analyze error rate
**Environment** |A distributed web service that runs on **Compute Engine VM** instances and uses **Cloud Load Balancing.**
**Visualize |A chart that displays requests that return **HTTP 500 responses:total number of requests.**
- You want to see a chart that displays the ratio of requests that return HTTP 500 responses (internal errors) to the total number of requests; that is, the request-failure ratio.
```
fetch https_lb_rule::loadbalancing.googleapis.com/https/request_count | group_by [matched_url_path_rule],
    sum(if(response_code_class = 500, val(), 0)) / sum(val)())
```
- The `loadbalancing.googleapis.com/https/request_count` metric type has a `response_code_class` label, which captures the class of response codes.
- This query uses an aggregation expression built on the ratio of two sums:
    - The first sum uses the if function to count 500-valued HTTP responses and a count of 0 for each other HTTP response codes. The sum function computes the count of the requests that returned 500.
    - The second sum adds up the counts for all requests, as represented by val().
    - The two sums are then divided, which results in the ratio of 500 responses to all responses.

