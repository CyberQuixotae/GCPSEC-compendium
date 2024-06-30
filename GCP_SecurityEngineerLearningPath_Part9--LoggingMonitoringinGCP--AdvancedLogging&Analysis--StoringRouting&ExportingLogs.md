[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/99/video/432507)

# Storing, routing, and exporting the logs
- What we call Cloud Logging is actually a collection of components exposed through a centralized logging API.
- Cloud Logging recieved log entries through Cloud Logging API
- Sinks contain the inclusion and exclusion filters that determine the log destination of those recieved log entries
- Cloud Storage buckets are different storage entites than Cloud Logging buckets.

## Default Log Buckets for Projects
- For each Google Cloud project, Logging automatically creates two logs buckets: _Required and _Default, and corresponding log sinks with the same names.

**_Required**
- Routes admin activity, system event and access transparency logs automatically
- No charges
- Retention period: Non-configurable 400 days
- Cannot be deleted or modified

**_Default**
- Logs not ingested by `_Required` buckets are routed by the `_Default` sink.
- No charges
- Configurable retention period. By default it is 30 days.
- Cannot be deleted by can be disabled.

## Logs Storage and usage
- At the top displays a summary of statistics for the logs that your project is recieving, including:
    - **Current total volume:** The amount of logs your project has received since the first date of the current month.
    - **Previous month volume:** The amount of logs your project received in the last calendar month.
    - **Projected volume by EOM:** The estimated amount of logs your project will receive by the end of the current month, based on current usage.

## Log router sinks and sink locations
- Log Router sinks can be used to forward copies of some or all of your log entries to non-default locations.
- Sink Locations:
    - **Cloud Logging bucket** works well to help pre-separate log entries into a distinct log storage bucket.
    - **BigQuery dataset** allows the SQL query power of BigQuery to be brought to bear on large and complex log entries.
    - **Cloud Storage bucket** is a simple external Cloud Storage location, perhaps for long-term storage or processing with other systems.
    - **Pub/Sub topic** can export log entries to message handling third-party applications or systems created with code and running somewhere like Dataflow or Cloud Functions.
    - **Splunk** is used to integrate logs into existing Splunk-based system.
    - The **Other** project option is useful to help control access to a subset of log entries.

## Create a log sink
- It involves writing a query that selects the log entries you want to export in Logs Explorer, and choosing a destination of Cloud Storage, BigQuery, or Pub/Sub. The query and destination are held in an object called a **sink**.

## Exclusions: Identify log entries
- Use Logs Explorer to build a query that selects the logs you want to exclude.

## Exclusions: Build the exclusion
- Give the filter a name
- Use the Log Explorer query to create an exclusion filter that filters the unwanted entries out of the sink.
- Take care here, because excluded log events will be lost forever.

## Log archiving and analysis
**Example Pipeline**:
1. Events -> 2. Logging -> 3. Pub/Sub -> 4. Dataflow -> 5. BigQuery
    - Dataflow is an excellent option if you're looking for real-time log processing at scale.
    - In this example, the Dataflow job could react to real-time issues, while streaming the logs into BigQuery for longer-term analysis.

## Archive logs for long-term storage
**Example Pipeline**:
1. Events -> 2. Logging -> 3. Cloud Storage
- Sink pipelines targeting Cloud Storage tend to work best when your needs align with Cloud Storage strengths.

## Exporting back to Splunk
**Example Pipeline**:
1. Events -> 2. Logging -> 3. Pub/Sub -> Splunk

## Aggregation levels

#### Project
A **project-level log sink** exports all the logs for a specific project.

A log filter can be specified in the sink definition to include/exclude certain log types.

#### Folder
A **folder-level log sink** aggregates logs on the folder level.

You can also include logs from children resources (subfolders, projects)

#### Organization
An **organization-level log sink** aggregates logs on the organization level.

You can also include logs from children resources (subfolders, projects).

## Log Entry Fields
- There are a few naming conventions that apply to log entry fields.
- For log entry fields that are part of the LogEntry type, the corresponding BigQuery field names are precisely the same as the log entry fields.
- For any user-supplied fields, the letter case is normalized to lowercase, but the naming is otherwise preserved.

