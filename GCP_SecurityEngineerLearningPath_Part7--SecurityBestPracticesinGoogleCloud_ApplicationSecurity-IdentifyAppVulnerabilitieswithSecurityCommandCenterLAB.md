[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/87/labs/450311)

# Objectives
In this lab, you will perform the following tasks:

- Launch a vulnerable Python Flask application on a Compute Engine instance
- Use Web Security Scanner to scan the application and find vulnerabilities
- Fix the application vulnerability
- Scan the application again and verify vulnerabilities no longer exist

### Task 1. Launch a Virtual machine and deploy a vulnerable application

#### Create a static IP address that will be used for scanning a vulnerable web application:
```shell
gcloud compute addresses create xss-test-ip-address --region=lab region
```

#### Run the following command to output the static IP address you just generated:
```shell
gcloud compute addresses describe xss-test-ip-address \
--region=lab region --format="value(address)"
```

#### Run the following command to create a VM instance to run the vulnerable application:
```shell
gcloud compute instances create xss-test-vm-instance \
--address=xss-test-ip-address --no-service-account \
--no-scopes --machine-type=e2-micro --zone=us-east1-b \
--metadata=startup-script='apt-get update; apt-get install -y python3-flask'
```

#### Open a firewall rule for Web Security Scanner to access a vulnerable application. Note the source ranges from which Web Security Scanner scans applications.
```shell
gcloud compute firewall-rules create enable-wss-scan \
--direction=INGRESS --priority=1000 \
--network=default --action=ALLOW \
--rules=tcp:8080 --source-ranges=0.0.0.0/0
```
#### SSH into the instance and run the following command to download and extract the vulnerable web application files:
```shell
gsutil cp gs://cloud-training/GCPSEC-ScannerAppEngine/flask_code.tar  . && tar xvf flask_code.tar
```
#### Now run the following command to deploy your application:
`python3 app.py`

#### Soon after, you should receive a message that indicates your application is up and running:

#### Replace YOUR_EXTERNAL_IP in the URL field below with that IP address, and open the URL in a new browser tab:
`http://<YOUR_EXTERNAL_IP>:8080`

- A Cymbal Bank corporate banking portal with a web form should appear.
- In the web form enter the following string:

```js
<script>alert('This is an XSS Injection')</script>
```
- Now press the POST button.

### The rest of this lab just goes over stuff that I don't think will specifically on the test so I am not going to bother notating it here.
