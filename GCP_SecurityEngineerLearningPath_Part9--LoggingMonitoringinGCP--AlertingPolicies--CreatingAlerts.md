[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/99/video/432499)

# Creating Alerts

## Use alerting policies to define alerts
An alerting policy has:
    - A name
    - One or more conditions
    - Notifications
    - Documentation

- Alert policies can also be created from the gcloud CLI, the API and Terraform.

## Alerting policies are of two types
**Metric-based alerting policies:**
- Used to **track metric data collected** by Cloud Monitoring.
- Add a metric-based alerting policy by starting from the Alerts page of Cloud Monitoring.
    - Example: Notify when the **application that runs on a VM has high latency** for a significant time period.

**Log-based alerting policies:**
- Used to notify anytime a **specific message occurs in a log.**
- Add a log-based alerting policy by using the Logs Explorer in Cloud Logging or under Cloud Monitoring.
    - Example: Notify when a **human user accesses the security key** of a service account.

## Alert Conditions
Where you spend the most alerting policy time and make the most decisions.

- You start with a target resource and metric you want the alert to monitor.
- You can filter, group by, and aggregate to the exact measure you require.
- Then the yes-no decision logic for triggering the alert notification is configured.
    - Includes the **Trigger condition**, **Threshold**, and **Duration**

## Configure Alert Triggers
    - Three types of conditions for metric-based alerts:
    - Metric-threshold conditions trigger when the values of a metric are more than, or less than, a threshold for a specific duration window.
    - Metric-absence conditions trigger when there is an absence of measurements for a duration window.
    - Forecast conditions predict the future behavior of the measurements by using previous data.

## Configure Notifications
#### Notification Channels:
    - Direct-to-human notification channels (Email, SMS, Slack, Mobile Push)
    - Third-party integration uses Webhook and Pub/Sub.
    - Manage your notifications and incidents by adding user-defined labels to an alerting policy.
        - If you send notifications to a third-party service like PagerDuty, Webhooks, or Pub/Sub then you can parse the JSON

#### Supported notification channels
Include:
    - Email
    - SMS
    - Slack
    - Google Cloud app
    - PagerDuty
    - Webhooks
    - Pub/Sub

## Documentation to guide troubleshooting
- Use the documentation section to guide your troubleshooting.
- Include internal playbooks, landing links and dynamic labels.
- Make it easy for the team to understand what is wrong.

## Alerting web interface
- When one or more alert policies are created, the alerting web interface provides a summary of incidents and alerting events.
    - An event occurs when the conditions for an alerting policy are met.
    - When an event occurs, Cloud Monitoring opens an incident.
    - Incidents appear in one of 3 states:

        - **Incident firing**: If an incident is open, the alerting policy's set of conditions is being met.
            - Or there's no data to indicate that the condition is no longer met.

        - **Open incidents**: Usually indicate a new or unhandled alert

        - **Acknowledged incidents**: A technician spots a new open alert. Before one starts to investigate, they mark it as acknowledged as a signal to others that someone is dealing with the issue.

## Resource groups can monitor multiple resources
- Trigger based on the group instead of on individual resources.
- Groups can contain subgroups up to six levels deep.
- Resources can be members of more than one group.

## Use multiple criteria to create resource groups
Criteria can include:
    - Cloud projects
    - Resource name
    - Resource type
    - Tags and labels
    - Security groups
    - Regions
    - App Engine apps and services

## Attach alerts to logs-based metrics
- The logs-based metrics serve as the basis for an alerting condition.
