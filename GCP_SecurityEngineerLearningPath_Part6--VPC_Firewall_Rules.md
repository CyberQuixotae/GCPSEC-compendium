### A Virtual Private Cloud
- A global, private, isolated virtual network partition that provides managed networking functionality for your Google Cloud resources.
- Google Cloud firewall rules let you allow or deny traffic to and from your VM instances based on a configuration you specify and can be applied to both inbound (or ingress) and outbound (or egress) traffic.
- Google Cloud firewall rules are defined for the VPC network as a whole, and since VPC networks can be global in Google Cloud, firewall rules are also global.
- Every VPC network functions as a distributed firewall.
- You can think of the Google Cloud firewall rules as existing not only between your instances and other networks, but between individual instances within the same network.

### Applying Firewall rules to your network and resources
- All instances in the network.
- Instances with a specific target tag.
- Instances using a specific account.
- Firewall Rules are "stateful"
    - Allow bi-directional communication

### Firewall rules:

Direction - Ingress or Egress

Source or destination - Source parameter is only applicable to ingress rules; destination is only applicable to egress rules

Protocol and port - Rules can be restricted to apply to specific protocols only, or combinations of protocols and ports only.

Action - allow or deny

Priority -  0-65535. The order in which rules are evaluated; the highest priority (lowest priority number) rule whose other components match traffic is applied.
