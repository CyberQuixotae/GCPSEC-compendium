## These are course screens and notes regarding [Networking in Google Cloud: Defining and Implementing Networks](https://www.cloudskillsboost.google/paths/15/course_templates/35)

![[Pasted image 20240416112425.png]]

![[Pasted image 20240416112747.png]]

![[Pasted image 20240416112930.png]]

If you delete the default route and do not replace it, packets to IP ranges not covered by other routes are dropped.

Some organizations do not want a default route pointing to the internet; instead, they want the default route to point to an on-premises network.

To do that, you can create a custom route.

![[Pasted image 20240416113154.png]]

![[Pasted image 20240416113330.png]]

![[Pasted image 20240416113401.png]]

![[Pasted image 20240416113456.png]]

![[Pasted image 20240416113529.png]]

BGP peer routers are typically outside the Google network (like on-premises or another cloud provider).

![[Pasted image 20240416113609.png]]

![[Pasted image 20240416113726.png]]

![[Pasted image 20240416113844.png]]

![[Pasted image 20240416113936.png]]

![[Pasted image 20240416114103.png]]

![[Pasted image 20240416114139.png]]

For some situations, you might require multiple interfaces; for example, to configure an instance as a network appliance for load balancing.

Multiple network interfaces are also useful when applications running in an instance require traffic separation, such as separation of data plane traffic from management plane traffic.

![[Pasted image 20240416114228.png]]

Each interface must belong to a subnet whose IP range does not overlap with the subnets of any other interfaces.

![[Pasted image 20240416114258.png]]

# [Working with multiple VPC networks Lab](https://www.cloudskillsboost.google/paths/15/course_templates/35/labs/432887)

![[OBtRY37ZCmWiHi_HsG8XCSGDBfsuKk3IMJVgQscsg2E=.png]]https://cdn.qwiklabs.com/OBtRY37ZCmWiHi%2FHsG8XCSGDBfsuKk3IMJVgQscsg2E%3D
### [Create/Modify VPC Networks](https://cloud.google.com/vpc/docs/create-modify-vpc-networks)

### [Set the dynamic routing mode](https://cloud.google.com/network-connectivity/docs/router/how-to/configuring-routing-mode)

### [Create custom mode VPC networks with firewall rules](https://www.cloudskillsboost.google/paths/15/course_templates/35/labs/432887#step3)


**Note:** You can ping the external IP address of all VM instances, even though they are in either a different zone or VPC network. This **confirms** that public access to those instances is only controlled by the **ICMP** firewall rules that you established earlier.

**Note:** You can ping the internal IP address of **mynet-eu-vm** because it is on the same VPC network as the source of the ping (**mynet-us-vm**), even though both VM instances are in separate zones, regions, and continents!

VPC networks are by default isolated private networking domains. However, no internal IP address communication is allowed between networks, unless you set up mechanisms such as VPC peering or VPN.

---

![[Pasted image 20240416154900.png]]

![[Pasted image 20240416154931.png]]

![[Pasted image 20240416155006.png]]

![[Pasted image 20240416155106.png]]

![[Pasted image 20240416155119.png]]

![[Pasted image 20240416155140.png]]The policy can specify inbound DNS forwarding, outbound DNS forwarding, or both.

![[Pasted image 20240416155312.png]]
For example, you can use response policies to block access to specified HTTP servers.

![[Pasted image 20240416155454.png]]


![[Pasted image 20240416162212.png]]
### Controlling Access to VPC Networks

![[Pasted image 20240430105250.png]]

![[Pasted image 20240430105330.png]]
### [Controlling Access to VPC Networks Lab](https://www.cloudskillsboost.google/paths/15/course_templates/35/labs/432899)

| Property | Value (type value or select option as specified) |
| -------- | ------------------------------------------------ |
| Name     | blue                                             |
| Region   | us-central1 (Iowa)                               |
| Zone     |  us-central1-a                                   |
gcloud compute instances create test-vm --machine-type=e2-medium --subnet=default --zone="us-central1-a"

Notes:

- I ran into issues with assigning a user created service account to the test-vm in the lab. Would like to loop back around to this later if I can. Hopefully I will review these notes if I need ideas on what else to study or review. :P

## Sharing Networks across Projects


![[Pasted image 20240430142250.png]]

Shared VPC networks allow an organization to connect resources from multiple projects to a common VPC network.

The resources can communicate with each other securely and efficiently using internal IP addresses from that network.

When you use shared VPC, you designate a project as a **host project** and attach one or more other **service projects** to it.

The overall VPC network is called the **shared VPC network**.

### Provision Shared VPC

- Required Roles:
	- Organization Admin
	- Shared VPC Admin
	- Service Project Admin

- Note that shared VPC is also referred to as “XPN” in the API and command-line interface.

![[Pasted image 20240430143412.png]]

- [How to Provision Shared VPCs](https://cloud.google.com/vpc/docs/provisioning-shared-vpc)

---
### VPC Network Peering

![[Pasted image 20240430150236.png]]

### Using VPC Network Peering

![[Pasted image 20240430150501.png]]

![[Pasted image 20240430150649.png]]
### Importing and exporting custom routes

![[Pasted image 20240430151046.png]]
	NOTE: WHEN TAKING IMAGES OF DIAGRAMS IN THE FUTURE EITHER DO IT FROM A 1080 YT VID OR FROM A PAGE.

![[Pasted image 20240430151242.png]]

![[Pasted image 20240430151340.png]]

![[Pasted image 20240430151434.png]]

### Lab - Configure VPC Network Peering (GO BACK AND COMPLETE THIS)

![[Pasted image 20240430151656.png]]
### Migrating a VM between networks

![[Pasted image 20240430152008.png]]

![[Pasted image 20240430152217.png]]

---
## Load Balancing

![[Pasted image 20240502115223.png]]

The internal load TCP/UDP balancer uses Andromeda, which is a a network virtualization stack that is software-defined and made by Google Cloud.

The network load balancer uses Maglev, which is a large, distributed software system.

The internal HTTP(S) load balancer is a proxy-based Layer 7 load balancer.

![[Pasted image 20240502115349.png]]

![[Pasted image 20240502115423.png]]

![[Pasted image 20240502115459.png]]

A hybrid connectivity NEG points to Traffic Director services that run outside of Google Cloud (on-premises or other public cloud backends).

The focus in this module is on hybrid connectivity NEGs.

---
## Hybrid Load Balancing

![[Pasted image 20240502115847.png]]

![[Pasted image 20240502115907.png]]

![[Pasted image 20240502120004.png]]
##### [Understanding Cloud Load Balancing for hybrid and multicloud environments](https://cloud.google.com/blog/products/networking/how-cloud-load-balancing-supports-hybrid-and-multicloud)

##### [Hybrid connectivity network endpoint groups overview](https://cloud.google.com/load-balancing/docs/negs/hybrid-neg-concepts)

![[ext-https-hybrid.svg]]

![[Pasted image 20240502120943.png]]

![[Pasted image 20240502121012.png]]

---
### Traffic Management

![[Pasted image 20240502121353.png]]

![[Pasted image 20240502122043.png]]

![[Pasted image 20240502122139.png]]

---
### Simple Routing

![[Pasted image 20240502122350.png]]

![[Pasted image 20240502122601.png]]

![[Pasted image 20240502122653.png]]

![[Pasted image 20240502122909.png]]

---
### Advanced routing and routing caveats

![[Pasted image 20240502123031.png]]

![[Pasted image 20240502123047.png]]

![[Pasted image 20240502123109.png]]

![[Pasted image 20240502123307.png]]

![[Pasted image 20240502123422.png]]

![[Pasted image 20240502123443.png]]

### Lab Notes & Links for Configuring Traffic Management with a Load Balancer

##### [Lab Page](https://www.cloudskillsboost.google/paths/15/course_templates/35/labs/432920)

##### [Use Health Checks](https://cloud.google.com/load-balancing/docs/health-checks)


![[FgrZkcSEqghVxKV14KPVgNzTUMo0lQfmqTgpG45+TYA=.png]]


Future Note: Even if you cannot FULLY iterate on a lab, make sure to follow along as CLOSELY as you can to ensure you are still understanding the why. It WILL HELP YOU!!

---

### Internal TCP/UDP Load Balancers

![[Pasted image 20240502161839.png]]

https://cloud.google.com/load-balancing/docs/internal#tcp-udp-request-return

---

### HA VPN Topologies

[How to Configure HA VPN Interconnect](https://cloud.google.com/network-connectivity/docs/interconnect/how-to/configure-ha-vpn-interconnect)

HA VPN supports site-to-site VPN for different configuration topologies. These
topologies are:
● An HA VPN gateway to peer VPN devices
● An HA VPN gateway to an Amazon Web Services (AWS) virtual private
gateway
● Two HA VPN gateways connected to each other

---

### HA VPN Recommendations

Use HA VPN for BGP routing and to support multiple tunnels.

VPN tunnels connected to HA VPN gateways must use dynamic (BGP) routing.

---

### Configuring Google Cloud HA VPN (Lab)

[Lab Page](https://www.cloudskillsboost.google/paths/15/course_templates/36/labs/456738)

![[VLAXpKCCD3vR0NwjlabV3gVp9Zzf1PPu7D91KCm9VY4=.png]]

![[Pasted image 20240507133422.png]]

**Note:** In your own environment, if you run HA VPN to a remote VPN gateway on-premises for a customer, you can connect in one of the following ways:

- _Two on-premises VPN gateway devices:_ Each of the tunnels from each interface on the Cloud VPN gateway must be connected to its own peer gateway.
- _A single on-premises VPN gateway device with two interfaces:_ Each of the tunnels from each interface on the Cloud VPN gateway must be connected to its own interface on the peer gateway.
- _A single on-premises VPN gateway device with a single interface:_ Both of the tunnels from each interface on the Cloud VPN gateway must be connected to the same interface on the peer gateway.

- [Beginners Guide to Understanding BGP](https://blog.cdemi.io/beginners-guide-to-understanding-bgp/)
	- Layer 4 (Transport Layer Protocol
	- [RFC1771: BGP Protocol](https://www.ietf.org/rfc/rfc1771.txt)

- [Cloud Router - Advertised Prefixes and Priorities](https://cloud.google.com/network-connectivity/docs/router/concepts/overview#advertised-prefixes-and-priorities)
	- Cloud Routers implement dynamic VPN that allows topology to be discovered and shared automatically, which reduces manual static route maintenance.

---

### Manage multi-site connectivity with Network Connectivity Center

- [Data Transfer Locations for Site-to-Site](https://cloud.google.com/network-connectivity/docs/network-connectivity-center/concepts/locations)
### Review Suggestions and Notes

- Review what Cloud Routers are and what they do
- Review Site-To-Site configuration for Network Connectivity Center component
- Topics in Module:
	- Direct Interconnect
	- Partner Interconnect
	- Cross-Cloud Interconnect
	- Cloud VPN

---
### Private Connection Options

#### Private Google Access Overview

- ![[Pasted image 20240507143833.png]]

- ![[Pasted image 20240507143904.png]]

- Unless a consumer connects to Google Cloud by using an external connection, private access communication does not go through the public internet.

- Each option allows VM instances with internal ip addresses to reach certain APIs and services

- [VPC Docs - Private access options for services](https://cloud.google.com/vpc/docs/private-access-options#connect-serverless-vpc)


---
### Private Google Access

- [VPC - Private Google Access](https://cloud.google.com/vpc/docs/private-google-access#pga-supported)

---

### Private Connection Options Review

- 

