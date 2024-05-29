
### Link to Lesson:
[VPC Peering and Interconnect Options](https://www.cloudskillsboost.google/paths/15/course_templates/21/video/449946)

### VPC Peering
- Can connect two nonoverlapping VPC networks.
- Networks do not need to be in the same project.
- A network can have up to 25 directly peered networks

### VPC Network Peering advantages
- Decreased network latency
    - Public IP networking suffers higher latency than private networking.

- Increased network security
    - Service owners do not need to have their services exposed to the public internet and deal wis6th its associated risks.

- Lower network cost
    - Peered networks can use internal IPs to communicate and saves you on egress costs.
    - Google Cloud charges egress bandwidth pricing for networks using external IPs to communicate even if the traffic is within the same zone. If the networks are peered, however, they can use internal IPs to communicate and save on those egress costs.

### Shared VPCs
- Make a VPC network shareable across several projects in your organization.
- Require a host project
    - Attach one more other service projects to it.
- Allow you to implement a security best practice of least privilege for network administration, auditing, and access control.
    - Shared VPC Admins can delegate network administration tasks to Network and Security Admins in the Shared VPC network.

