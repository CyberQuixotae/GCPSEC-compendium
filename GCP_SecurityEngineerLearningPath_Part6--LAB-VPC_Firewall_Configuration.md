### [Configuring VPC Firewalls](https://www.cloudskillsboost.google/paths/15/course_templates/21/labs/449944)

- Note: When an auto mode VPC network is created, one subnet from each region is automatically created within it. These automatically created subnets use a set of predefined IP ranges that fit within the 10.128.0.0/9 CIDR block.

- To create the network *privatenet* with custom subnets, run the following command:

```
gcloud compute networks create privatenet \
--subnet-mode=custom
```

- To create a custom subnet in the privatenet network, run the following command:

```
gcloud compute networks subnets create privatesubnet \
--network=privatenet --region=us-central1 \
--range=10.0.0.0/24 --enable-private-ip-google-access
```

- Note: Because the default network allows relatively open access, we recommend that you delete it for production projects.

- Note: As you just verified, the browser-based console SSH feature used to connect to VM instances does not currently work. If you want to allow that, you need a firewall rule that allows the source IP address. However, source IP addresses for browser-based SSH sessions are dynamically allocated by the Cloud Console and can vary from session to session.

- For the feature to work, you must allow connections either from any IP address, or from Google's IP address range, which you can retrieve using public SPF records. Either of these options may pose unacceptable risks, depending on your requirements. Instead, you would allow the IP address of the SSH clients you are using to connect.

- To add a firewall rule that allows port 22 (SSH) traffic from the Cloud Shell IP address, run the following command:

```
gcloud compute firewall-rules create \
mynetwork-ingress-allow-ssh-from-cs \
--network mynetwork --action ALLOW --direction INGRESS \
--rules tcp:22 --source-ranges $ip --target-tags=lab-ssh
```

- Note: You have just created and applied a firewall rule using a tag. One issue with tags is that they must be added to instances and could possibly be added or removed inadvertently. Firewall rules can also be applied to instances by the service account used. These rules will be applied automatically to all instances that use the specified service account.

- To add the lab-ssh network tag to the mynet-eu-vm and mynet-us-vm instances, run the following commands in Cloud Shell:

```
gcloud compute instances add-tags mynet-eu-vm \
    --zone europe-west1-b \
    --tags lab-ssh
gcloud compute instances add-tags mynet-us-vm \
    --zone us-central1-a \
    --tags lab-ssh
```

- In VPC networks, firewall rules are stateful. Which means bi-directional traffic is allowed.

- To add a firewall rule that allows ALL instances in the mynetwork VPC to ping each other, run the following command:

```
gcloud compute firewall-rules create \
mynetwork-ingress-allow-icmp-internal --network \
mynetwork --action ALLOW --direction INGRESS --rules icmp \
--source-ranges 10.128.0.0/9
```
- In the second Cloud Shell, create a firewall ingress rule to deny ICMP traffic from any IP with a priority of 500:

```
gcloud compute firewall-rules create \
mynetwork-ingress-deny-icmp-all --network \
mynetwork --action DENY --direction INGRESS --rules icmp \
--priority 500
```
- Which will not allow for any internal pings whatsoever. The allow rule is 1,000


- To change the priority of the rule to 2000:
```
gcloud compute firewall-rules update \
mynetwork-ingress-deny-icmp-all \
--priority 2000
```

- To create a firewall egress rule to block ICMP traffic from any IP with a priority of 10K

```
gcloud compute firewall-rules create \
mynetwork-egress-deny-icmp-all --network \
mynetwork --action DENY --direction EGRESS --rules icmp \
--priority 10000
```

- To list all the current firewall rules again:
```gcloud compute firewall-rules list \
--filter="network:mynetwork"
```

- It should no longer work. Even though the egress rule has a much higher priority of 10,000, it is still blocking traffic. This is because for traffic to be allowed, there must be both an ingress and egress rule allowing that traffic. The priority of ingress rules does not affect the priority of egress rules.
