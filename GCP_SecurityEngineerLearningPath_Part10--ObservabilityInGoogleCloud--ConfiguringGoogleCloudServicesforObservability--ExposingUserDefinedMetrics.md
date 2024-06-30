[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/864/video/467970)

# User-defined metrics
- Any metrics not defined by Google Cloud are user-defined metrics.
- They are used to extract metrics that are not captured by the built-in metrics.

Two approaches:
1. Use OpenTelemetry Protocol and OpsAgent(recommended)
2. Use the Cloud Monitoring API

## Collect user-defined metrics by using OTLP reciever
- The OpenTelemetry (OTLP) receiver is a plugin installed on the Ops Agent that helps collect the **user-defined metrics from the applciation** and send those metrics to Cloud Monitoring for analysis and visualization. These metrics can then be used to create dashboards, uptime checks, and alerting policies

- Ingestion and authorization is not required as it is handled at the agent level. To
configure OTLP, you must install an Ops Agent and modify the user configuration file
to include the OTLP file.

- By default, the receiver uses the Prometheus API; the default value for the
metrics_mode option is googlemanagedprometheus

- To receive the custom metrics from the OTLP receiver, set the OTLP receiver
metrics_mode to googlecloudmonitoring

## Create user-defined metrics by using the API
- [Create user-defined metrics with the API](https://cloud.google.com/monitoring/custom-metrics/creating-metrics#monitoring_create_metric-python)

```python
//Custom metric descriptor example in Python
from google.cloud import monitoring_v3

client = monitoring_v3.MetricServiceClient()
project_name = client.project_path(project_id)

descriptor = monitoring_v3.types.MetricDescriptor()
descriptor.type = ('custom.googleapis.com/my_metric')
descriptor.metric_kind = (monitoring_v3.enums.MetricDescriptor.MetricKind.GAUGE)

descriptor.value_type = (monitoring_v3.enums.MetricDescriptor.ValueType.DOUBLE)

descriptor.description = 'Custom metric example.'

client.create_metric_descriptor(project_name, descriptor)
```
---

1. To begin, the data you collect for a custom metric must be associated with a
descriptor for a custom metric type. In this example, we create a gauge double
metric named my_metric. It's a gauge metric of type double, with the
description "Custom metric example."

2. Once you collect the information you need for creating your custom metric
type, call the create method, passing into a MetricDescriptor object. You write
data points by passing a list of `TimeSeries` objects to `create_time_series`.

## Writing user-defined metrics

```python
from google.cloud import monitoring_v3

client = monitoring_v3.MetricServiceClient()
project_name = f"projects/{project_id}"

series = monitoring_v3.TimeSeries()
series.metric.type = "custom.googleapis.com/my_metric" + str(uuid.uuid4())
series.resource.type = "gce_instance"
series.resource.labels["instance_id"] = "1234567890123456789"
series.resource.labels["zone"] = "us-central1-c"
series.metric.labels["TestLabel"] = "My Label Data"
now = time.time()
seconds = int(now)
nanos = int((now - seconds) * 10**9)
interval = monitoring_v3.TimeInterval(
    {"end_time": {"seconds": seconds, "nanos": nanos}}
)
point = monitoring_v3.Point({"interval": interval, "value": {"double_value": 3.14}})
series.points = [point]
client.create_time_series(name=project_name, time_series=[series])
```

- You write data points by passing a list of TimeSeries objects to the function
create_time_series. Each time series is identified by the metric and resource fields of the TimeSeries object.

- These fields represent the metric type and the monitored resource from which the
data was collected.

## Query custom metrics
- After you configure the metrics_mode to Prometheus API or the Cloud Monitoring API
in the OTLP receiver, you can then query the metrics by using Metrics Explorer,
dashboards or even alternate interface.
