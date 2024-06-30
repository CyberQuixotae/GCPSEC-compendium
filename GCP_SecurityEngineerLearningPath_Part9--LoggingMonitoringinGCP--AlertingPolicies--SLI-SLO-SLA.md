[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/99/video/432497)

# SLI, SLO and SLA

## Service level indicator (SLI)
- Carefully selected monitoring metrics that measure one aspect of a service's reliability.
    - Ideally, SLIs should have a close linear relationship with your users' experience of that reliability, and we recommend expressing them as the ratio of two numbers:
        - The number of good events divided by the count of all valid events.

## Service Level Objective (SLO)
- Combines a service level indicator with a target reliability and will generally be somewhere just short of 100%, for example 99.9%("three nines").

- You can't measure everything, so when possible, you should choose SLOs that are S.M.A.R.T. SLOs should be specific.

 **S** Specific
 **M** Measurable
 **A** Achieveable
 **R** Relevant
 **T** Time-bound

## Service Level Agreement (SLA)
- Commitments made to your customers that your systems and applications will have only a certain amount of down time.

### For SLOs, SLIs and SLAs to help improve service reliability
- All parts of the business must agree that they are an **accurate measure of user experience**.
- Must also agree to use them as a **primary driver for decision making**.

### SLI, SLO and SLA example
The **SLA** agreement is - to Maintain an **error rate**(SLI) of less than **0.3%**(SLO) for the billing system

- If your service has paying customers, you probably have some way of compensating them with refunds or credits when that service has an outage.
    - The problem with SLAs is that you're only incentivized to promise the minimum level of service and compensation that will stop your customers from replacing you with a competitor.
