[Link to Lab:](https://www.cloudskillsboost.google/paths/15/course_templates/88/labs/483877)

#  Configuring and Viewing Cloud Audit Logs

## Objectives
In this lab, you will learn how to perform the following tasks:

- View audit logs in the Activity page.
- View and filter audit logs in Cloud Logging.
- Retrieve log entries with gcloud.
- Export audit logs.

## Enable data access audit logs
- At command prompt, run command to retrieve the current IAM policy for your project and save it as policy.json:
```shell
gcloud projects get-iam-policy $DEVSHELL_PROJECT_ID \
--format=json >./policy.json
```
- Click the Open Editor button to view the Cloud Shell code editor.
- In Cloud Shell code editor, click **policy.json** file to expose its contents.
- Add following text to `policy.json` file to **enable data Access audit logs for all services**. This text should be added just after the first { and before "bindings": [. (Be careful not to change anything else in the file).
```json
   "auditConfigs": [
      {
         "service": "allServices",
         "auditLogConfigs": [
            { "logType": "ADMIN_READ" },
            { "logType": "DATA_READ"  },
            { "logType": "DATA_WRITE" }
         ]
      }
   ],
```
- Click the Open Terminal button to return to the Cloud Shell command line.
- At the command line, run the following command to set the IAM policy:
```shell
gcloud projects set-iam-policy $DEVSHELL_PROJECT_ID \
./policy.json
```
The command will return and display the new IAM policy.

## Generate some account activity
- In Cloud Shell, run the following commands to create a few resources. This will generate some activity that you will view in the audit logs:
```shell
gsutil mb gs://$DEVSHELL_PROJECT_ID
echo "this is a sample file" > sample.txt
gsutil cp sample.txt gs://$DEVSHELL_PROJECT_ID
gcloud compute networks create mynetwork --subnet-mode=auto
gcloud compute instances create default-us-vm \
--machine-type=e2-micro \
--zone="ZONE" --network=mynetwork
```
```shell
gsutil rm -r gs://$DEVSHELL_PROJECT_ID
```
## View the Admin Activity logs

#### Use the Cloud Logging page
- From the Cloud Console, select **Navigation menu > Logging > Logs Explorer**.
- Paste the following in the **Query builder** field and replace [PROJECT_ID] with your project ID.
- Click **Run Query** button.
- Locate the log entry indicating that a Cloud Storage bucket was deleted. This entry will refer to `storage.googleapis.com`, which calls the `storage.buckets.delete` method to delete a bucket. The bucket name is the same name as your project id.

- Within that entry, click on the **storage.googleapis.com** text and select **Show matching entries**.
- Notice a line was added to the query preview textbox (located where the query builder had been) to show only storage events.
```
logName = ("projects/qwiklabs-gcp-xxxxxxxxx/logs/cloudaudit.googleapis.com%2Factivity")
protoPayload.serviceName="storage.googleapis.com"
```
- Within that entry, click on the **storage.buckets.delete** text and select **Show matching entries**.
- Notice another line was added to the Query preview textbox and now you can only see storage delete entries.
- In the Query results, expand the **Cloud Storage delete** entry and then expand the **protoPayload** field.
- Expand the **authenticationInfo** field and notice you can see the email address of the user that performed this action.

#### Using the Cloud SDK
- In Cloud Shell, use this command to retrieve only the audit activity for storage bucket deletion:
```shell
gcloud logging read \
"logName=projects/$DEVSHELL_PROJECT_ID/logs/cloudaudit.googleapis.com%2Factivity \
AND protoPayload.serviceName=storage.googleapis.com \
AND protoPayload.methodName=storage.buckets.delete"
```
## Export the audit logs
Audit log type 	Retention period
Admin Activity 	400 days
Data Access 	30 days

- When exporting logs, the current filter will be applied to what is exported.
- In Logs Explorer, enter a query string in the **Query builder** to display all the audit logs. (This can be done by deleting all lines in the filter except the first one.) Your filter will look like what is shown below. (Note that your project ID will be different.
```
logName = ("projects/[PROJECT_ID]/logs/cloudaudit.googleapis.com%2Factivity")
```
- Click **Run Query** button.
- Click on **More actions > Create Sink** button.
- For the **Sink Name** name, enter `AuditLogsExport` and click Next.
- For the **Sink service**, enter `BigQuery dataset`
- Click **Select BigQuery dataset** and then select **Create new BigQuery dataset**.
- For the **Dataset ID**, enter `auditlogs_dataset` and click **Create Dataset**.
- Uncheck **Use Partitioned Tables** checkbox, if it is already selected, and click **Next**.
- In the Build inclusion filter list box, make sure that this filter text is entered `logName = ("projects/[PROJECT_ID]/logs/cloudaudit.googleapis.com%2Factivity")`.
- Click **Create Sink** button. The Logs Router Sinks page appears. Now click on **Logs Router**.
- To the right of the AuditLogsExport sink, click the button with three dots (More icon) and select **View sink details**.
- Click **Cancel** when done.
- In Cloud Shell, run the following commands to generate some more activity that you will view in the audit logs exported to BigQuery:
```shell
gsutil mb gs://$DEVSHELL_PROJECT_ID
gsutil mb gs://$DEVSHELL_PROJECT_ID-test
echo "this is another sample file" > sample2.txt
gsutil cp sample.txt gs://$DEVSHELL_PROJECT_ID-test
gcloud compute instances delete --zone="ZONE" \
--delete-disks=all default-us-vm
```
When prompted, enter `y`
```shell
gsutil rm -r gs://$DEVSHELL_PROJECT_ID
gsutil rm -r gs://$DEVSHELL_PROJECT_ID-test
```
## Use BigQuery to analyze logs
- Go to **Navigation menu > BigQuery**. If prompted, log in with the Qwiklabs-provided credentials.
- Click **Done**
- Under the **Explorer** section (left pane), click your project. You should see an **auditlogs_dataset** dataset under it.
- Verify that the BigQuery dataset has appropriate permissions to allow the export writer to store log entries. Click on the **auditlogs_dataset** dataset.
- From the **Sharing** dropdown, select **Permissions**.
- On the Dataset Permission page, you will see the service account listed as **BigQuery Data Editor** member.
- Click the **Close** button to close the **Share Dataset** screen.
- Expand **dataset** to see the table with your exported logs. (Click on the expand icon to expand the dataset.)
- Click **table name** and take a moment to review the **schemas** and **details** of the tables that are being used.
- Click the **Query > In new tab** button.
- In Cloud Shell, run the following commands to generate more activity that you will view in the audit logs exported to BigQuery:
```shell
gcloud compute instances create default-us-vm \
--zone="ZONE" --network=mynetwork
```
```shell
gcloud compute instances delete --zone="ZONE" \
--delete-disks=all default-us-vm
```
When prompted, enter `y`

```shell
gsutil mb gs://$DEVSHELL_PROJECT_ID
gsutil mb gs://$DEVSHELL_PROJECT_ID-test
gsutil rm -r gs://$DEVSHELL_PROJECT_ID
gsutil rm -r gs://$DEVSHELL_PROJECT_ID-test
```
- Delete the text provided in the **Query editor** window and paste in the query below. This query will return the users that deleted virtual machines in the last 7 days.
```sql
#standardSQL
SELECT
  timestamp,
  resource.labels.instance_id,
  protopayload_auditlog.authenticationInfo.principalEmail,
  protopayload_auditlog.resourceName,
  protopayload_auditlog.methodName
FROM
`auditlogs_dataset.cloudaudit_googleapis_com_activity_*`
WHERE
  PARSE_DATE('%Y%m%d', _TABLE_SUFFIX) BETWEEN
  DATE_SUB(CURRENT_DATE(), INTERVAL 7 DAY) AND
  CURRENT_DATE()
  AND resource.type = "gce_instance"
  AND operation.first IS TRUE
  AND protopayload_auditlog.methodName = "v1.compute.instances.delete"
ORDER BY
  timestamp,
  resource.labels.instance_id
LIMIT
  1000
```
`NOTE: I believe the schemas are different than what is shown in the lab so just be aware!`
- Click the **Run** button. After a couple of seconds you will see each time someone deleted a virtual machine within the past 7 days. You should see two entries, which is the activity you generated in this lab. Remember, BigQuery is only showing activity since the export was created.
- Delete the text in the **Query_editor** window and paste in the query below. This query will return the users that deleted storage buckets in the last 7 days.

```sql
#standardSQL
SELECT
  timestamp,
  resource.labels.bucket_name,
  protopayload_auditlog.authenticationInfo.principalEmail,
  protopayload_auditlog.resourceName,
  protopayload_auditlog.methodName
FROM
`auditlogs_dataset.cloudaudit_googleapis_com_activity_*`
WHERE
  PARSE_DATE('%Y%m%d', _TABLE_SUFFIX) BETWEEN
  DATE_SUB(CURRENT_DATE(), INTERVAL 7 DAY) AND
  CURRENT_DATE()
  AND resource.type = "gcs_bucket"
  AND protopayload_auditlog.methodName = "storage.buckets.delete"
ORDER BY
  timestamp,
  resource.labels.instance_id
LIMIT
  1000
```
`NOTE: I believe the schemas are different than what is shown in the lab so just be aware!`

- Click the **Run** button. After a couple seconds, you will see entries showing each time someone deleted a storage bucket within the past 7 days.


