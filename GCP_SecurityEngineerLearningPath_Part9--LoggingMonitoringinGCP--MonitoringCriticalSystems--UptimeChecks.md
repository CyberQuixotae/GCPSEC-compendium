[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/99/video/432492)

# Uptime Checks

## Uptime checks test public service availability
- Uptime checks can be configured to test the availability of your public services from locations around the world
- The type of uptime check can be set to:
    - HTTP
    - HTTPS
    - TCP
- For each uptime check, you can create an alerting policy and view the latency of each global location.

## Uptime check example
- The resource is checked every minute with a 10-second timeout. Uptime checks that **do not get a response** within this timeout period are considered failures.
- So far, there is a 100% uptime with no outages.

## Creating an Uptime check
- In **Monitoring**, navigate to **Uptime Checks** and click **Create Uptime Check**.
    - Give the uptime check a name or title that is descriptive.
    - Select the check type protocol, the resource type, and appropriate information for that resource type.
    - A number of optional advanced options are available, including logging failures, narrowing the locations in the *world from where test connections are made, the addition of custom headers, check timeout, and authentication.
