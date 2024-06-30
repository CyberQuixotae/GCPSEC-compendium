[Link to lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/99/video/432509)

# Using Log Based Metrics

## Logs-based metrics
- Logs-based metrics derive metric data from the content of log entries.
    - For example, metrics can track the number of entries that contain specific messages or extract latency information that is reported in the logs.
- These metrics transform into time series data and use it in Cloud Monitoring Charts and Alerting Policies.
- Two types of log-based metrics:
    - **System-defined** log-based metrics are calculated only from logs that have been ingested by Logging.
        - If a log has been explicitly excluded from ingestion by Cloud Logging, it isn't included in these metrics.
    - **User-defined** log-based metrics are created by you to track things in your project that are of particular interest.

## Logs-based metrics are suitable in different cases
- **Count the occurences**: Count the occurences of a message, like a warning or error, in your logs and recieve a notification when the number of occurences crosses a threshold.
- **Observe trends in your data**: Observe trends in your data, like latency values in your logs, and recieve a notification if the values change in an unacceptable way.
- **Visualize extracted data**: Create charts to display the numeric data extracted from your logs.

## Key access control roles
- **Logs configuration Writer**
    - List, create, get, update, and delete log-based metrics.
- **Logs Viewer**
    - View existing logs.
- **Monitoring Viewer**
    - Read the time series in log-based metrics.
- **Logging Admin, Editor, and Owner**
    - Broad-level roles that can create log-based metrics.

## Log-based metric types
- **Counter metrics** count the number of matched log entries
- **Distribution metrics** Record the statistical distribution of the extracted log values
- **Boolean metrics** Record where a log entry matches a specified filter
- All **predefined system** log-based metrics are the **counter type**, but user-defined metrics can be either **counter, distribution or boolean types**.

## Scope of log-based metrics
- System-defined log-based metrics apply at project level
- User-defined log-based metrics can apply **either** at **project** or **bucket** level

## A sample test code
```js
//Basic NodeJS app built with the express server
app.get('/score'),(req, res) => {
//Random score, the containerID is a UUID unique to each
//runtime container (testing was done in Cloud Run).
//funFactor is a random number 1-100
let score = Math.floor(Math.random() * 100) + 1;
 console.log(`/score called, score:${score},
    containerID:${containerID}, funFactor:${funFactor}`);
  //Basic message back to browser
res.send(`Your score is a ${score}. Happy?`);
});
```
- Track the request on the `/score` path
- If a request matches, generated 1-100 score
- Define log entry fields
- Send a msg containing the score

## Filtering entries
-  Now we can filter to select those entries by clicking "/score called", and selecting Show matching entries in the log explorer

## Basic Flow for creating log-based metrics

### In Logs Explorer
1. Find the log with the requisite data
2. Filter to required entries
3. **Actions|Create Metric**
4. Pick a metric type (Counter or Distribution)
5. If Distribution, set configurations
6. You can also add labels

## Labels and logs
- Their prime use is to help with group-by and filtering tasks in Cloud Monitoring.
- Labels allow log-based metrics to contain multiple time series—one for each label value.
- Two types of labels applied:
    - Default
    - User-defined
- User-defined labels can be either of the following:
    - The entire contents of a named field in the `LogEntry` object.
    - A part of a named field that matches a regular expression.
- You can create up to ten user-defined labels per metric.
- A label cannot be deleted once created.
    - Grows the time series significantly.

## Creating user-defined labels
- **User-defined labels** can be created when creating a log-based metric. The form requires:
    - **Name**, which is an identifier which will be used to label in Monitoring.
    - **Description**, which describes the label.
    - **Label type**, choose **String, Boolean, or Integer**
    - Enter name of log entry field containing value of label (supports autocomplete).

