[Link to Lab:](https://www.cloudskillsboost.google/paths/15/course_templates/88/labs/483874)

# Configuring and Using Cloud Logging and Cloud Monitoring -- LAB

## Objectives
In this lab, you will learn how to perform the following tasks:
    - View logs using a variety of filtering mechanisms.
    - Exclude log entries and disable log ingestion.
    - Export logs and run reports against exported logs.
    - Create and report on logging metrics.
    - Use Cloud Monitoring to monitor different Google Cloud projects.
    - Create a metrics dashboard.

Note: There are 2 projects in this lab:
- A project of active Google Cloud Resources, which will generate logs and monitoring metric data.
- The second project will contain your Monitoring account configuration data.

## Set up resources in your first project
- Click **Activate cloud shell**. If prompted, click **Continue**
- In Cloud Shell, download and unpack an archive that contains setup code:
```shell
curl https://storage.googleapis.com/cloud-training/gcpsec/labs/stackdriver-lab.tgz | tar -zxf -
```
```shell
cd stackdriver-labs
```
- Click **Open Editor** icon in top-right corner of Cloud Shell session
- Click **Open in a new window**
- Open **stackdriver-lab** folder and select **linux_startup.sh** file
- Replace the `# install Ops Agent` section with the following:
```shell
# install Ops Agent
curl -sSO https://dl.google.com/cloudagents/add-google-cloud-ops-agent-repo.sh
sudo bash add-google-cloud-ops-agent-repo.sh --also-install
```
- Save file
- Open `setup.sh` file
- Update image version in `# create vms` section for windows-server (row 17) after `--image` with following:
```shell
windows-server-2016-dc-core-v20240214
```
- Add following flag at end of line 16 to set machine type for Linux VM:
```shell
--machine-type=e2-micro
```
- Add following flag at end of line 17 to set machine type for Windows VM:
```shell
--machine-type=e2-standard-2
```
- Save file.
- In Cloud Console, click **Open Terminal** in top right corner.
    - Created resources will include:
        - Service accounts (for use by VMs).
        - Role assignments (granting service accounts permissions to write to Monitoring).
        - A Linux VM with Apache and the Ops Agent installed.
        - A Windows VM with Ops Agent installed.
        - A Google Kubernetes Engine cluster with an Nginx deployment.
        - A Pub/Sub Topic and Subscription.

- Run following command to replace zones in setup script with new one:
```shell
sed -i 's/us-west1-b/lab zone/g' setup.sh
```
- Now run following command. If prompted, click **Authorize**
```shell
./setup.sh
```
- Ensure you recieve similar output that states both Linux and Windows VMs are created:
```shell
Created [https://www.googleapis.com/compute/v1/projects/qwiklabs-gcp-00-029875ba6255/zones/"Zone"/instances/linux-server-qwiklabs-gcp-00-029875ba6255].
NAME: linux-server-qwiklabs-gcp-00-029875ba6255
ZONE: "Zone"
MACHINE_TYPE: e2-micro
PREEMPTIBLE:
INTERNAL_IP: 10.138.0.2
EXTERNAL_IP: 34.83.92.58
STATUS: RUNNING
Created [https://www.googleapis.com/compute/v1/projects/qwiklabs-gcp-00-029875ba6255/zones/"Zone"/instances/windows-server-qwiklabs-gcp-00-029875ba6255].
......
......
NAME: windows-server-qwiklabs-gcp-00-029875ba6255
ZONE: "Zone"
MACHINE_TYPE: e2-standard-2
PREEMPTIBLE:
INTERNAL_IP: 10.138.0.3
EXTERNAL_IP: 35.247.97.91
STATUS: RUNNING
Updated [https://www.googleapis.com/compute/v1/projects/qwiklabs-gcp-00-029875ba6255/zones/"Zone"/instances/linux-server-qwiklabs-gcp-00-029875ba6255].
```

## View and filter logs in first project
- Go to Google Cloud Console homepage
- Verify you are still working in project 1
- View Cloud Logging by opening **Navigation menu > Logging > Logs Explorer**. If prompted, close notification
- On left-hand panel **Log fields** will be visible. Under **Resource Type** you will see several Google Cloud services that are creating logs.

#### View VM instance logs with simple filtering
- In **Log fields** panel, under **Resource Type**, click **VM instance**
    - The contents of the Log fields panel changes. You'll see a new field named `INSTANCE ID`. It shows all the instance IDs of the VM instances that are writing log entries.
    - Query box near top of page is populated with `resource.type="gce_instance"`. This means only entries from VM instances will be logged and displayed.

- In **Instance Id** field, select one instance ID. Logs for assicated VM instance appear in Query results pane.
- Click inside **Query** box. Box is now editable
- In **Query** box, remove everything after line 1. You should see only line 1, which contains `resource.type=gce_instance`.
- Click **Run query** (located in top-right corner). In Query results, you should see entries from all VM instance logs.
    - Note that logs panel reverts to its previous state.
- Turn on streaming logs by clicking **Stream logs** (top-right corner, next to the "Run query" button)
    - You should see new log entries showing up every 1-2 seconds as the background activity is generating unauthorized requests against your Web servers.
- You will now view overall web activity on any Linux Apache server.
- Stop log streaming by click on **Stop stream** in top-right corner.
- Now click on **All Log Names** dropdown, select **syslog**, then click **Apply**
- Entries from **syslog** appear in Query results pane.

### Use log exports
- Cloud Logging retains log entries for 30 days. In most circumstances, you'll want to retain some log entries for an extended time (and possibly perform sophisticated reporting on the archived logs).
    - Google Cloud provides a mechanism to have all log entries ingested into Cloud Monitoring also written to one or more archival sinks.

#### Configure export to BigQuery
- Go to Cloud Logging Exports (**Navigation menu > Logging > Log Router**)
- Click **Create Sink**
- For the **Sink name** type `vm logs` then click **Next**
- For **Select sink service** select **BigQuery dataset**
- For **Select BigQuery dataset** select **Create new BigQuery dataset**
- For **Dataset ID**, type `project_logs` and click **Create Dataset**
- Click **Next**
- In **Build inclusion filter** list box, copy and paste `resource.type="gce_instance"`
- Click **Create Sink**. You will now return to a Log Router *Create log sink* next steps page

```
Note: You could also export log entries to Pub/Sub or Cloud Storage.

Exporting to Pub/Sub can be useful if you want to flow through an ETL process prior to storing in a database (Monitoring > Pub/Sub > Dataflow > BigQuery/Bigtable).

Exporting to Cloud Storage will batch up entries and write them into Cloud Storage objects approximately every hour.
```
#### Configure HTTP load balancing exports to BigQuery
- From left-hand navigation menu, select **Log Router** to return to the service homepage.
- Click **Create Sink**
- For **Sink name**, type `load_bal_logs` then click **Next**
- For **Select sink service** select **BigQuery dataset**
- For **Select BigQuery dataset** select **project_logs**
- Click **Next**
- In **Build inclusion filter** list box, copy and paste `resource.type="http_load_balancer"`
- Click **Create Sink**
- You will now be on the *Create log sink next steps* page
- From left-hand navigation menu, select **Log Router** to return to the service homepage.
    - The Log Router page appears, displaying a list of sinks (including the one you just created—load_bal_logs).

#### Investigate the exported log entries
- Open BigQuery (**Navigation menu > BigQuery**)
- In the left pane in Explorer section, click arrow next to your project. You should see a `project_logs` dataset revealed under it.
- Verify that the BigQuery dataset has appropriate permissions to allow the exporter writer to store log entries.
- Click on three dotted menu item ("View actions") next to `project_logs` dataset and click **Open**
- From top-right hand corner of Console, click **Sharing** dropdown and select **Permissions**
- On Dataset permission page, you will see that your service accounts have the "BigQuery Data Editor" role.
- Close dataset permissions panel
- Expand `projects_logs` dataset to see the tables with your exported logs
- Click on **syslog_(1)** table, then click **Details** to see number of rows and other metadata.
- In **Details**, under table info you will see the full table name in **Table ID**, copy table name.

```
Note: Cloud Logging exports incoming log entries before any decision is made about ingesting the entry into logging storage. As a result, only new log entries will be exported to the sink. As a result, you may not see a syslog_(1) table as all the syslog entries were generated prior to the export.

Existing log entries already ingested into Cloud Logging can be extracted using commands like:

gcloud logging read "resource.type=gce_instance AND logName=projects/[PROJECT_ID]/logs/syslog AND textPayload:SyncAddress" --limit 10 --format json.
```
#### Create a logging metric
- Go back to Logs Explorer page (**Navigation menu > Logging > Logs Explorer**)
- Select **Create Metric** (right-hand side of Console) to create a logging metric based on this filter.
- In Log-based metric Editor, set **Metric Type** as **Counter**
- Under the **Details** section, set the **Log-based metric name** to **403s**
- Under **Filter section** for **Build filter**, enter following and replace `PROJECT_ID` with **GCP Project ID 1**
```shell
resource.type="gce_instance"
log_name="projects/PROJECT_ID/logs/syslog"
```
- Click **Create Metric**

### Create a monitoring dashboard

#### Switch projects
- Switch to second project

#### Create a monitoring workspace
- In Cloud Console, click on **Navigation menu > Monitoring**
- Wait for workspace to be provisioned
- In left menu, click **Monitoring Settings**, and then click **+ Add GCP Projects**
- Click **Select Projects**
- Select the checkmark next to your first project ID and click **Select**
- Click **Add Projects**

#### Create a monitoring dashboard
- In left pane, click **Dashboards**
- Click **+ Create Dashboard**
- Click **Add Widget > Line**
- For **Widget Title** enter in **CPU Usage**
- Click **Metric** dropdown
- Click **Active** to deselect it.
- For **Metric**, select **VM Instance > Instance > CPU Usage**
- Click **Apply**
- Now click **Apply** in top-right corner
- Click **Add Widget > Line**
- For **Widget Title** enter in **Memory Utilization**
- Click **Metric** dropdown
- Click **Active** to deselect it.
- For **Metric**, select **VM Instance > Memory > Memory Utilization**
- Click **Apply**
- Now click **Apply** in top-right corner
















