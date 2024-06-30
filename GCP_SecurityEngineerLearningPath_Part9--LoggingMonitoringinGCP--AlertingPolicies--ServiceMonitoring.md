[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/99/video/432501)

# Service Monitoring

## Service monitoring helps with SLO and alert creation
- What are the **commitments regarding the availability and performance** of those services, and are your services meeting them?
- For microservices-based apps, what are the **inter-service dependencies**?
- How to double **check new code rollouts and triage problems** if a service degradation occurs?
- Can you **look at all the monitoring signals for a service holistically** to reduce MTTR?

## Consolidated services overview
- The Service Monitoring consolidated services overview page is your point of entry.
- Services pane provides a summary of the health of your various services.

## Windows-based versus request-based SLOs
- Request-based SLOs = good request : total requests
- Window-based SLO = total number of good requests : total number of bad requests

## Windows-based versus request-based SLOs
- Imagine you get 1,000,000 requests a month and your compliance period is a rolling 30 days.
- A 99.9% request-based SLO can allow 1,000 bad requests every 30 days.
- A 99.9% windows-based SLO based on a 1-minute window can allow a total of 43 bad windows.
    - 43,200 total windows * 99.9% = 43,157 good windows.
- Windows-based SLOs can be tricky, because they can hide burst-related failures.

## Creating an SLO
- Select a listed service
- Create an SLO, select an option from the SLI metric:
    - Availability = Ratio of the number of successful responses : the number of all responses
    - Latency = Ratio of the number of calls that are below the specified Latency Threshold to the number of all calls.
    - Other = Gives you the **Metrics Explorer** and lets you create your own SLI from the beginning.

## Set Compliance and Period Goals
- In the Compliance period section, select the **Period Type** and **Period Length.**
    - The two compliance period types are calendar-based and rolling.
- In the **Performance Goal** section, enter a percentage in the Goal field to set the performance target for the SLI.
- Service Monitoring uses this value to calculate the error budget you have for this SLO.
