[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/99/video/432498)

# Developing an Alerting Strategy

## Goal: A person is notified when needed
- A service is down
- SLOs or SLAs are heading toward not being met
- Something needs to change

- The events are processed through a time series: a series of event data points broken into successive, equally spaced windows of time.
- Based on need, the duration of each window and the math applied to the member data points inside each window are both configurable.
- Because of the time series, events can be summarized, error rates can be calculated, and alerts can be triggered where appropriate.

## When something puts the error budget in danger: Alert!
Error budget = The proportion of alerts detected that were relevant to the sum of relevant alerts and missed alerts.
- **SLIs** are the things you measure
- **SLOs** represent an achieveable target

If the SLO is "90% of requests must return in 200 ms," the the error budget is 100% - 90% = 10%

## Evaluating alerts
- Four major attributes are considered when attempting to measure the accuracy or effectiveness of a particular alerting strategy:
    - **Precision**: `Relevant alerts = Relevant alerts + irrelevant alerts.`
        - Adversely affected by false positives.

    - **Recall**: `Relevant alerts = Relevant alerts + missed alerts.`
        - Striving for precision might cause events to be missed
        - **Recall is adversely affected by missed alerts.**

    - **Detection time:** `How long it takes the system to notice an alert condition.`
        - Long detection times can negatively affect the error budget.
        - **Raising alerts too fast may result in poor precision**

    - **Reset time:** `How long alerts fire after an issue is resolved.
        - **Continued alerts on repaired systems can lead to confusion.**

## When error count is trending greater than error budget: Alert!
- The concept windows, as related to SRE and alerting, is frequently used in two main ways:
    - An SLO of 99.9% is meaningless without a time period.
    - A **window** is the period over which the error calculation is made.

## Alert window lengths
**Small windows**
- Faster alert detection
- Shorter reset time
- Poor precision

For a 99.9% availability SLO over 30 days, a 10-minute window would alert in 0.6 seconds if a full outage occurs.

Consume only 0.02% of the error budget.

---

**Longer windows**
- Better precision
- Longer reset and detection times
- More error budget spent before alert

For a 99.9% availability SLO over 30 days, a 36-hour window would alert in 2 minutes 10 seconds if a full outage occurs.

Represents 5% of the error budget.

## Try short windows with successive failure counts
An error is spotted quickly but treated as an anomaly until **three** windows fail in a row.

Recall becomes worse:
- If the duration is 10 minutes, a 100% outage for 5 minutes is not detected.
- If errors spike up and down, they might never be detected.

## Use multiple conditions for better precision and recall
- Many variables can affect a good alerting strategy:
    - Amount of traffic
    - Error budget
    - Peak and slow periods
- You can define multiple conditions in an alerting policy to try to get better precision, recall, detection time, and rest time.
- You can also define multiple alerts through multiple channels.

## Prioritize alerts based on customer impact and SLA
- Involve humans only for critical alerts.
- Use severity level to assess the priority of an alert.
- Configure how to triage low- and high-priority alerts.
