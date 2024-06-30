[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/99/video/432508)

# Query and view logs

## Logs Explorer
Contains the following panes:
1. The Action toolbar - To refine logs to projects or storage views, share a link and learn about logs explorer
2. Query pane - where you can build queries, view recently viewed and saved queries and a lot more
3. Results Toolbar - Used to quickly show or hide logs and histogram pane and create a lot based metric or alert
4. Query results -  The Action toolbar to refine logs to projects or storage views, share a link and learn about logs explorer
5. Log fields -  used to filter your options based on various factors such as a resource type, log name, project ID, etc
6. Histogram - where the query result is visualized as histogram bars, where each bar is a time range and is color coded based on severity.

## Ultimately, it’s the query that selects the entries displayed by Logs Explorer.
- Start with what you know about the entry you're trying to find.
- If it belongs to a resource, a particular log name, or has a known severity, use the query builder drop-down menus.

### Query builder-drop down menu
- Makes it easy to start narrowing down your log choices
- **Resource** lets you specify `resource.type`
    - You can select a single resource at a time to add to the Query builder
- **Entries** use the logical operator `AND`
- **Log name** lets you specify `logName`
    - You can select multiple log names at once to add to the Query builder
        - When selecting multiple entries, the logical operator `OR` is used
- **Severity** lets you specify severity.
    - You can select **multiple severity levels at once**

## Comparison operators to filter queries

`[FIELD_NAME] [OP] [VALUE]`
---
**=** **Equals** = `resource.type="gce_instance"`
**!=** **does not equal** = `resource.labels.instance_id!="123456789"`
**>< >= <=** **numeric ordering** = `timestamp <= "2018-08-13T20:00:00Z"`
**:** **has** = `textPayload:"GET /check"`
**`:*`** **presence** = `jsonPayload.error:*`
**=~** **search for a pattern** = `jsonPayload.message =~ "regular expression pattern"`
**!-** **search not for a pattern** = `jsonPayload.message !~ "regular expression pattern"`

## Finding log entries, set the time range
- You can select one of the pre-created choices, set a custom range, or jump to a particular time.

## Narrow with Logs fields and Histogram
- **Log fields panel** offers a high-level summary of logs data and provides a more efficient way to refine a query.
    - Shows count of log entries, sorted by decreasing count, for the given log field.
    - Log field counts correspond to time range used by Histogram panel
        - You can add fields from the Log fields panel to the Query builder to narrow down and refine a query by clicking a field.

- **Histogram panel** lets you visualize distribution of logs over time
    - To analyze your log data, point to a bar in the Histogram panel and select Jump to time to drill into a narrower time range. A new query runs with that time-range restriction.
        - Advanced queries support the AND, OR, and NOT boolean expressions for joining queries.

## Supported Boolean operators
---
**AND** `textPayload:("foo" AND "bar")`
**NOT** `textPayload:("foo" AND NOT "bar")`
**OR** `textPayload:("foo" OR "bar")`
---
- Ensure to use the all caps for the operator name.
- The NOT operator has the highest precedence, followed by OR and AND in that order.
- The Boolean operators AND and OR are short-chircut operators.

## The recipe for finding entries
- What do you know about the log entry?
    - Log filename, resource, and some text
- Full text searches are slow, but may be effective:
    - `"/score called"`
- Use indexed SEARCH function for complete text matches, because they perform a case-insensitive match
    - `SEARCH(textPayload,"hello world")`
- If possible, restrict text searches to a log field
    - `jsonPayload:"/score called"`
    - `jsonPayload.message="/score called"`

## Finding entries quickly
- Search on an indexed field
    - `httpRequest.status, logName, operation.id, resource.type, timestamp, severity`
- Apply constraints on `resource.type` and `resource.labels` field
    - `resource.type = "gke_cluster"`
    - `resource.labels.namespace = "my-cool-namespace"`
- Be specific on which logs you're searching
    - `logName="projects/benkelly-test/logs/apache-access"`
- Limit the time range that you're searching
    - `timestamp >= "2018-08-08T10:00:00Z" AND timestamp <= "2018-08-08T10:10:00Z"`
