[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/88/video/483852)

# DDoS Mitigation & Prevention

## DDoS prevention is a shared responsibility between you and Google

## Successful DDoS mitigation strategies have many layers
- Load balancing: Using proxy-based load balancing to distribute load across resources
- Attack surface: Reducing the attack surface on by reducing externally facing resources
- Internal traffic: Isolating internal traffic from the outside world by restricting access
- API management: Monitor and manage APIs to spot and throttle DDoS attacks
- CDN offloading: Offloading static content to a CDN to minimize impact
- Specialized DDoS protection: Deploying applications that specifically provide deeper DDoS protection

## DDoS prevention on Google Cloud
- Leveraging Google’s load balancer
- Reduce network attack surface in VPCs
- Isolate internal traffic
- Use Cloud CDN
- Use API management and monitoring
- Leverage Google Cloud Armor

## Leveraging Google's load balancer
Cloud Load Balancing provides built-in defense against infrastructure DDoS attacks.
- No additional configuration is required to activate this DDoS defense.
- Leverages Google's central DoS mitigation service.
    - If the system detects an attack, it can configure load balancers to drop or throttle traffic.

## Reducing attack surface
**Attack surface definition:**
Sum of the different points where an unauthorized user can try to enter data to or extract data from an environment.
- Isolate machines within VPCs.
- Set up firewall rules to block unused ports.
- Use firewall rules to block unwanted sources.
- **Use firewall tags and service accounts to control targets.**

## Restricting public access to internal traffic
- Don't give machines public IPs unnecessarily.
- Use bastion hosts to limit machines exposed to the internet.
- Use internal load balancers for internal services.

## Using Cloud CDN
Caches content between your users and your servers.
- Requests for cached content are routed to POPs.
- Google's massive infrastructure can absorb attacks.

## API management and monitoring
- Create an API gateway to manage your backend services.
    - Throttle requests to limit requests from clients.
    - Control access to APIs from a single location.
    - Monitor API usage.
- Can use Cloud Endpoints or Apigee to create API gateways.

