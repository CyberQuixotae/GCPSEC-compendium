[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/99/video/432490)

# Data model and dashboards

## Cloud Monitoring data model
- In general terms, monitoring data is recorded in **time series**. Four pieces of information:
    - **Metric**
        - `metric label` represents one combination of label values
        - `metric type` specifies the available labels and describes what is represented by the data point
    - **Resource**
        - `resource label` represents one combination of label values and the specific monitoring
        - `resource information` represents the source of the metrics
    - **metricKind and valueType**
        - Tell you how to interpret the values
    - **Points**
        - Are an array of timestamped values that tells you what the values of the metrics are

## Cloud Monitoring metrics are one of three kinds
    - A **Gauge metric** is a value that measures a specific instance in time.
        - For example, metrics measuring CPU utilization are gauge metrics; each point records the CPU utilization at the time of measurement.
    - A **Delta metric** is a value that measures the change in a time interval.
        - For example, metrics measuring request counts are delta metrics; each value records how many requests were received after the start time, up to and including the end time.
    - A **Cumulative metric**, in which the value constantly increases over time.
        - For example, a metric for “sent bytes” might be cumulative; each value records the total number of bytes sent by a service at that time.

## Sample time series notes
- Metric collected is a set of activity logs of the type **log_entry_count** with a severity level INFO

- A Compute Engine instance with the specified instance_id, zone and project_id
- The metric kind is of the type DELTA and value type integer
- Points are the actual array of time stamp and value of the metric

## To monitor your Google Cloud systems
1. First, identify the Google Cloud monitoring resources you want to monitor.
2. Next check the **Monitoring > Dashboards** for an auto-created dashboard.
3. You can monitor any of the more than 1500 metrics and custom metrics, and can even build custom dashboards.

## Metrics Explorer
- When you can't find what you need, or need something specific, use the Monitoring and navigate to Metrics Explorer.

- The Metrics Explorer interface consists of three primary regions:
    - A **configuration region**, where you pick the metric and its options
    - The **chart that displays the selected metric**
    - The **display panel**, where you can configure the axis, set a threshold lines, and more

## Metric Configuration
- `Metric:`To populate the chart, you must specify at least one pair of values, the monitored resource type, and the metric type.

- `Filter:`You can reduce the amount of data returned for a metric by specifying a filter.
    - When you click in the Filter field, a panel that contains lists of criteria by which you can filter appears.
    - In broad strokes, you can filter by resource group, by name, by resource label, and by the metric label.
        - The zone can then be compared to a direct value, like `"=n1-standard-4,"` or by using the `“=”` operator, to any valid regular expression.

- `Group by:`You can reduce the amount of data returned for a metric by combining different time series.
    - To combine multiple time series, you typically specify a grouping and a function.
    - Grouping is done by **label values**

- `Alignment`Creates a new time series in which the raw data has been regularized in time so it can be combined with other aligned time series.
    - Alignment produces time series with regularly spaced data.
    - A **time series** is a set of data points in temporal order.
        - To align a time series to break the data points into regular buckets of time, the alignment period is used.
        - Multiple time series **must** be aligned before they can be combined.
            - You can override these defaults by using the alignment options, which are the Alignment function and the Min alignment period.

## Display Configuration
- `Widget type:` modifies how the values will be displayed like if it will show as a line chart, a bar chart, etc.
- `Analysis Mode:`There are three analysis modes:
    - Standard mode displays each time series with a unique color.
    - Stats mode displays common statistical measures for the data in a chart.
    - X-Ray mode displays each time series with a translucent gray color.
        - Each line is faint, and where lines overlap or cross, the points appear brighter. This mode is most useful on charts with many lines.
- `Threshold:` The Threshold option creates a horizontal line from a point in the Y-axis.
- `Legend:` In this example, you can see the mix of the variable, ${resource.labels.zone} - ${metric.labels.instance_name}.

