[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/864/video/467976)

# Firewall Rules Logging

## VPC firewall rules
- VPC firewall rules let you **allow or deny connections** to or from your (VM) instances based on a configuration that you specify.
- Enabled VPC firewall rules are always enforced, and **protect your instances**
regardless of their configuration and operating system, even if they didn’t start

## Firewall Rules Logging
- Lets you audit, verify, and analyze the effects of your firewall rules. Helps you answer questions like:
    - Did my firewall rules cause that application outage?
    - How many connections match the rule I just created?
    - Are my firewall rules stopping (or allowing) the correct traffic?
    - [Firewall Rules Logging](https://cloud.google.com/firewall/docs/firewall-rules-logging)

## Enabling Firewall Rules Logging in the console
- Firewall Rules Logging is disabled by default.
- You can enable it on a per-rule basis.
- Firewall Rules Logging can only record TCP and UDP connections. For other
protocols, use Packet Mirroring
- Caution: Firewall Rules Logging can generate a lot of data, which might have a cost
implication

## Enabling Firewall Rules Logging in the CLI
- To activate:
```bash
compute firewall-rules update [NAME] --enable-logging
```
- To deactivate:
```bash
gcloud compute firewall-rules update [NAME] --no-enable-logging
```
    - In both, the `[NAME]` tag will be the name of your firewall rule

## Viewing the firewall rules logs
- Logs Explorer to view logs in real time or to configure exports.
- To filter for firewall logs and network policy firewall logs, below the Compute Engine resource, select **firewall**

## Firewall rules provide microsegmentation
- **Segmentation or gateway-centric**
    - Designed to segment and secure a protected network from an outside insecure network.
    - Considered typical, classic segmentation

- Google Cloud VPC firewalls are **micro-segmentation** firewalls
        - These function more like a bunch of micro-firewalls, each operating over the **Network Interface Controller (NIC)** of every VM connected to the VPC.

## Troubleshooting: Using rules to catch incorrect traffic
- **Logging all denied connections creates too many log entries**
- **Temporarily create a high-priority rule to allow traffic to the server**
- **If traffic now gets through, examine the logs to find the root cause**
