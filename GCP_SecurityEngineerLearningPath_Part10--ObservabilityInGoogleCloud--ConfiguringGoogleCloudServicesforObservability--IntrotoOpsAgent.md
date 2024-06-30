[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/864/video/467966)

# Introduction to Ops Agent

## What is Ops Agent?
- Primary agent for collecting telemetry data from Compute Engine instances.
- Combining logging and metrics into a **single agent**
- Ops Agent uses **Fluent Bit for logs**, which supports high-throughput logging, and the **Open Telemetry Collector for metrics**
- Agents required for security reasons; hypervisor cannot access some of the internal metrics inside a VM, (example: memory usage)
- You can use Ops Agent to monitor and troubleshoot [third-party applications](https://cloud.google.com/stackdriver/docs/solutions/agents/ops-agent/third-party)
- Ops Agent supports most major operating systems

## Why Ops Agent?
- Monitors your VM instances without the need for any additional configuration after the
installation.
- Monitors third-party applications and supports both Windows and Linux guest OS.
- Exposes many additional process metrics beyond memory and gives you better visibility to CPU, disk, and network performance.
- Unifies gathering of metrics and logs into a single agent.
- Ingests user-defined metrics in Prometheus format.

**Other Benefits**
- It monitors your VM instances without the need for any additional
configuration after the installation.
- It helps monitor 3rd party applications and also supports both Windows and
Linux guest OS.
- Exposes additional process metrics beyond memory; gives you
better visibility to CPU, disk, and network performance. Exposes metrics
beyond 80+ metrics that Cloud Monitoring already supports for Compute
Engine.
- The Ops Agent unifies gathering of metrics and logs into a single agent.
- And also ingests any user defined (Custom) metrics in Prometheus format.

## Three ways to install Ops Agent
- Using CLI - Install agent on a single VM by using command line.
- Using agent policies - Install agents on a fleet of VMs by using agent policies.
- [Using automation tools - Install agents on a fleet of VMs by using automation tools](https://cloud.google.com/logging/docs/agent/ops-agent/fleet-installation)

## Installing the Ops Agent by using the agent policy
- Step 1: Install the beta component of the gcloud CLI
- Step 2: Enable the APIs
- Step 3: Create a policy
- [Manage agent policies](https://cloud.google.com/monitoring/agent/ops-agent/managing-agent-policies)

## Installing the Ops Agent by using the agent policy
```bash
gcloud beta compute instances \
    ops-agents policies create ops-agents-policy-safe-rollout \
    --agent-rules="type=ops-agent,version=current-major,package-state=installed,enable-autoupgrade=true" \
    --os-types=short-name=centos,version=7 \
    --group-labels=env=test,app=myproduct \
    --project=my_project
```
## Installing the Ops Agent on individual VMs (1/2)
1. Go to the VM instances page in the Google Cloud console.
2. Click the name of the VM that you want to install the agent on. The Details
page opens.
3. Click the Observability tab. The Observability page opens. Click Install

## Installing the Ops Agent on individual VMs (2/2)
- A new window open. Click Run in Cloud Shell. Cloud Shell opens and pastes the
installation command.
- [Installing Ops Agent on individual VM](https://cloud.google.com/logging/docs/agent/ops-agent/installation)
1. Press Enter on your keyboard to run the command.
2. Click Authorize to allow Cloud Shell to install the agent.

## Troubleshooting: Agent is not sending metrics to Cloud Monitoring
- Check the metrics module in syslog.
- If there are no logs, then the agent service is not running.
- If you see `permission_denied` errors when writing to the Monitoring API, enable the **Monitoring API** and the **Monitoring Metric Writer** role.
- [Troubleshoot Ops Data Ingestion](https://cloud.google.com/stackdriver/docs/solutions/agents/ops-agent/troubleshoot-run-ingest#agent-not-running)

