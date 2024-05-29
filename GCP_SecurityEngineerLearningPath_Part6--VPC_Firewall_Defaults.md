### All VPCs have implied firewall rules
1. Implied IPv4 firewall rules are present in all VPC networks
- Implied IPv4 allow egress rules
    - Lets any instance send traffic to any destination

- Implied IPv4 deny ingress rule
    - Protects all instances by blocking incoming connections to them.


2. If IPv6 is enabled, the VPC network also has these two implied rules:
- Implied IPv6 allow egress rule
    - Lets any instance send traffic to any destination

- Implied IPv6 deny ingress rule
    - Protects all instances by blocking incoming connections to them.

- Implied rules cannot be removed, but have the lowest possible priorities.

### Default VPCs have additional allow rules
- `default-allow-internal`: Allows ingress connections for all protocols and ports among instances within the VPC network

- `default-allow-ssh`: Allows port 22 - secure shell (ssh) access

- `default-allow-rdp`: Allows port 3389 - remote desktop protocol (RDP) access

- `default-allow-icmp`: Allows ICMP traffic

- All of these rules have the second-to-lowest priority of 65534.
- These rules can (and should) be deleted or modified as necessary.

### Some VPC network trafic is always allowed
- Packets sent to and recieved from the Google Cloud metadata server.
- Packets sent to an IP address assigned to one of the instance's own network interfaces (NICs) where packets stay within the VM itself.

### Some VPC network traffic is always blocked
- Ingress and egress traffic exceeding VM's machine type limits
- DHCP offers and acknowledgements
- All traffic other than external IPv4 and IPv6
- SMTP (port 25) traffic


