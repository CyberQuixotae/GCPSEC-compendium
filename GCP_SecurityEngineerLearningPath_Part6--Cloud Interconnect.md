
### Link to Lesson:
[Cloud Interconnect](https://www.cloudskillsboost.google/paths/15/course_templates/21/video/449948)

- **Cloud Interconnect** connections provide RFC 1918 communication, which means internal (private) IP addresses are directly accessible from both networks. Offers either **Dedicated Interconnect** or **Partner Interconnect**

### Dedicated Interconnect
- Dedicated interconnect provides a direct physical connection between your on-premises network and Google Cloud VPC networks.
- Minimum bandwidth of 10Gbps
    - If more than 10 gigabits per second bandwidth is needed, multiple interconnects can be provisioned.
- Requires routing equipment in a colocation facility that supports the Google Cloud regions that you want to connect to.
- Google provides an end-to-end SLA for the connection

### Partner Interconnect
- Partner Interconnect provides connectivity between your on-premises network and Google Cloud VPC networks through a supported service provider.
- Minimum bandwidth of 50 Mbps
- Use any supported service provider to connect to Google.
- Traffic flows through a service provider, not through the public internet.
- Google provides an SLA for the connection between Google and service provider. An end-to-end SLA for the connection depends on the service provider.
