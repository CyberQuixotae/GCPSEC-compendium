[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/864/video/467975)

# VPC Flow Logs
- VPC Flow Logs is used to monitor network by **recording a portion** of network flows **sent and received** by VM instances (including GKE nodes).

- VPC Flow Logs records a sample (about one out of ten packets) of network flows sent
from and received by VM instances, including Google Kubernetes Engine nodes.
- These logs can be used for network monitoring, traffic analysis, forensics, real-time security analysis, and expense optimization
- Part of **Andromeda**, the software that powers **VPC networks**.
- No delay or performance penalty when enabled :)

## VPC Flow Logs example
**VM to external traffic flow**
Region: us-west-1
Subnet: 10.10.0.0/26
VM IP: 10.10.0.2
VPN Client: 10.30.0.2

Flow logs reported from the VM:
Egress flow: 10.10.0.2 to 10.30.0.2
Ingress flow: 10.30.0.2 to 10.10.0.2

Traffic flows are reported from the **VM only** and include:
- Ingress traffic: The logs reported with VM as its destination. In this example,
the ingress traffic is reported from the source VM 10.30.0.2 to 10.10.0.2
- Egress traffic: The logs reported with VM as its source. In this example, the
egress traffic is reported from the source VM 10.10.0.2 to 10.30.0.2

## VPC Flow Logs properties
- **Samples are from the VM’s perspective**
    - If an egress firewall is denied, those packets are sampled by VPC Flow Logs.
        - Ingress blocked packets are not logged because they're sampled after the ingress firewall rules.
- **Samples are logged for each VMs**
    - TCP, UDP, ICMP, ESP and GRE flows are captured from each VM.
    - Records inbound and outbound flows for each VM, thus capturing traffic between VMs, VM-to on-premises, VM to another host.
- **VMs support multiple network interface** and can be enabled at the subnet level.

## Enabling VPC Flow Logs
**VPC Flow logs is activated or deactivated at a subnet level**
    - All VMs within that subnet have VPC Flow Logs automatically enabled.
**You can enable VPC Flow Logs during subnet creation**
    - To enable VPC Flow Logs, during subnet creation, select **On** next to Flow Logs.
    - You can optionally adjust log sampling and aggregation to adjust the metadata and sample rate written to logs.

## Log entries contain many useful fields
-  Information consists of the source IP address and port, the destination IP address and port, and the protocol number. This set is commonly referred to as 5-tuple.

- Other fields include the start and end time of the first and last observed packet, the bytes and packets sent, instance details including network tags, VPC details, and
geographic details.

- [VPC Flow Logs Documentation](https://cloud.google.com/vpc/docs/flow-logs#record_format)

| ---------- | ---------| ----------------------|
| **Field**  | **Type** | **Description**       |
| src_ip     | string   | Source IP address     |
| src_port   | int32    | Source port           |
| dest_ip    | string   | Destination IP address|
| dest_port  | int32    | Destination port      |
| protocol   | int32    | IANA protocol number  |


## Use Logs Explorer to access your VPC Flow Logs
- The entries will be `vpc_flows` below the Compute Engine section. Searching the log names for `vpc_flows` works well.

## Analyze logs with Log Analytics
- You can analyze ad-hoc query-time without complex pre-processing as before.
- You can use BigQuery to query data and upgrade buckets to use Log Analytics and then create a linked dataset.
- [sample queries](https://github.com/GoogleCloudPlatform/observability-analytics-samples)

