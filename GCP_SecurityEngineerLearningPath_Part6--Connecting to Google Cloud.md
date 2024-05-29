
### Link to Lesson:
[Connecting to Google Cloud](https://www.cloudskillsboost.google/paths/15/course_templates/21/video/449947)

### Connecting to Google Cloud
- **Cloud VPN**: Securely connects your peer network to your Virtual Private Cloud (VPC) network through an IPsec VPN connection
- **Cloud Interconnect**: Extends your on-premises network to Google's network through a highly available, low latency connection.

### Cloud VPN
- Supports IKEv1 and IKEv2 using a shared secret (also known as an IKE pre-shared key)
- Cloud VPN traffic will either traverse the public Internet or can use a direct peering link to Google’s network.
- Each Cloud VPN tunnel can support up to 3 gigabits per second when the traffic is traversing a direct peering link, or 1.5 gigabits per second when it’s traversing the public internet.

### VPN with static routes
- With static routing, updating the tunnel requires:
    - The addition of static routes to Google Cloud
    - Restarting the VPN tunnel to include the new subnet

- A **Cloud Router** enables you to dynamically exchange routes between your VPC network and on-premises networks by using Border Gateway Protocol (or BGP).

### Google Cloud routes
- Define paths network traffic take from a VM to other destinations.
    - Can be inside VPC or outside of it.
- Routes created when a network or subnet is created.
- Consists of single destination prefix and next hop.

### Static vs dynamic routes
- **Static routes**
    - Defined with static route parameters
    - Support static route next hops

- **Dynamic Routes**
    - Managed by Cloud Routers in the VPC network
    - Destinations always represent IP address ranges outside your VPC network
    - Used by:
        - Dedicated Interconnect
        - Partner Interconnect
        - HA VPN tunnels
        - Classic VPN tunnels that use dynamic routing


