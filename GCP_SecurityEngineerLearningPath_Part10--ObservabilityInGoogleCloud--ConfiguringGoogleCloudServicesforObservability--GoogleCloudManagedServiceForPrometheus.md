[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/864/video/467969)

# Google Cloud Managed Service for Prometheus
- Collects, stores, and analyzes Prometheus metrics.
- Collects metrics from both GKE and Compute Engine environments.
- Helps make GKE easier to use with maintained metric collectors.

## The Managed Service for Prometheus ecosystem
- Built on top of **Monarch** which is the same globally scalable data store as Cloud Monitoring.
- You can replace your existing Prometheus deployment to collect cluster and workload metrics
- And then query the data across multiple clusters by using PromQL
- Managed Service for Prometheus splits responsibilities for data collection, query
evaluation, rule and alert evaluation, and data storage into multiple components:
    - **Monarch** handles query evaluation and data storage. It can execute queries and union results across all Google Cloud regions. Also supports two years of metric retention by default at no additional cost.
    - For data collection, multiple choices available; includes self-deployed, Ops Agent, OpenTelemetry, and managed collection. These collectors are responsible for scraping local exporters and forwarding that data to **Monarch**
    - Rule evaluation is handled by locally run and configured rule evaluators. Refer to documentation on storage granularity and retention timeline.

- Any UI that can call the Prometheus query API is also supported in the managed service for Prometheus.
- PromQL can be used to query:
    - 1,500 free metrics in Cloud Monitoring
    - Free Kubernetes metrics, custom metrics, and log-based metrics

## Data collection options
- **Managed data collection:** Managed data collection in Kubernetes environment
    - Recommended to use managed collection; because it eliminates the complexity of deploying, scaling, sharding, configuring, and maintaining Prometheus servers.
    - Managed collection is supported for both GKE and non-GKE Kubernetes environments.
- **Self-deployed data collection:** Prometheus installation managed by the user
    - Only difference from upstream Prometheus is that you run the Managed Service for Prometheus drop-in replacement binary instead of the upstream Prometheus binary.
- **Using Ops Agent**: Prometheus metrics scraped and sent by the Ops Agent
    - Using an agent simplifies VM discovery and eliminates the need to install, deploy, or configure Prometheus in VM environments.
- **OpenTelemetry collection**: Deployed in any compute or Kubernetes environment
    -  It is deployed either manually or by using Terraform in any compute or Kubernetes environmen

### Other consideration options
- Managed collection is a recommended approach for all Kubernetes environments and is especially suitable for more hands-off fully managed experience.
- Self-deployed collection is suitable for quick integration into more complex
environment.
- Using the Ops Agent is the easiest way and is recommended to collect and
send Prometheus metric data originating from Compute Engine environments,
including both Linux and Windows distros.
- The OpenTelemetry Collector is best to support cross-singal workflows such
as exemplars

## Rule and alert evaluation
- No need to co-locate the data in a single Prometheus server or on a single Google Cloud project.
- The rule evaluator uses the standard Prometheus rule files format, which
makes migration to Managed Service for Prometheus easier.

## Setting up managed collection for GKE clusters
- You can enable a managed collection for your resource by selecting the GKE cluster you need and clicking `ENABLE SELECTED`

## Deploy a PodMonitoring resource to scrape metrics
- After enabling managed collection, the in-cluster components are running, but no metrics are generated yet. You must deploy a PodMonitoring resource that scrapes a metrics endpoint to see any data in the Query UI

- The manifest below defines a PodMonitoring resource, `prom-example`, in the namespace.
- The resource uses a Kubernetes label selector to find all the pods in the namespace that have the label app with the value `prom-example`.
    - The matching pods are scraped on a port named metrics, every 30 seconds on the /metrics HTTP path.

```yaml
apiVersion: monitoring.googleapis.com/v1
kind: PodMonitoring //PodMonitoring resource
metadata:
  name: prom-example
spec:
  selector:
    matchLabels:
      app: prom-example //find pods that matches the label and value
endpoints:
- port: metrics
   interval: 30s //scrape on a prot every 30 second
```

- To apply this resource, run the command:
`kubectl -n NAMESPACE_NAME apply -f <pod-monitoring.yaml>`

- To configure a horizontal collection that applies to a range of pods across all
namespaces, use the `ClusterPodMonitoring` resource. The ClusterPodMonitoring
resource provides the same interface as the PodMonitoring resource but does not
limit discovered pods to a given namespace.

## Using PromQL
- When working with metric data, you can use the following query tools provided by Cloud Monitoring:
    - PromQL
    - Monitoring Query Language (MQL)
    - Monitoring filters

- Simplest way to verify your Prometheus data is being exported is to use the Cloud Monitoring Metrics Explorer page in the Google Cloud console:
    - Go to **Monitoring**
        1. In the Monitoring navigation pane, click Metrics Explorer.
        2. Select the PromQL tab.
        3. Enter the query. Here we are running a simple up query.
        4. And simply click Run Query.
