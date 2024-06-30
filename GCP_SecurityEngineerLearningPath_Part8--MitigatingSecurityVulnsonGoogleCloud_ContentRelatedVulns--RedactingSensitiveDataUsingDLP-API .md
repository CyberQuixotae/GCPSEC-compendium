[Link to Lab:](https://www.cloudskillsboost.google/paths/15/course_templates/88/labs/483865)

# Redacting Sensitive Data with the DLP API

## Objectives
In this lab, you will learn how to do the following:
- Enable the DLP API.
- Install the Node JS DLP API and sample.
- Inspect string data for sensitive data.
- Redact sensitive data from string data and images.

## Enable the DLP API
- **Navigation menu > APIs & Services**.
- Click **Enable APIs and Services** button.
- In **Search for APIs and Services field, enter `DLP` and click on **Cloud Data Loss Prevention (DLP) API**

## Install the DLP API and Node JS samples
- On Google Cloud Console tile bar, click **Activate Cloud Shell** to open Cloud Shell.
- Run following command to create `GCLOUD_PROJECT` env variable and set it to the project ID:
```shell
export GCLOUD_PROJECT=$DEVSHELL_PROJECT_ID
```
- Run command in Cloud Shell to download the Node JS DLS API and samples:
```shell
git clone https://github.com/GoogleCloudPlatform/nodejs-docs-samples
```
- Once download completes, change into **nodejs-docs-samples/dlp** directory:
```shell
cd nodejs-docs-samples/dlp
```
- Install required dependencies:
```shell
npm install @google-cloud/dlp
npm install yargs
npm install mime
```
## Inspect and redact sensitive data
- In Cloud Shell run the command below:
```shell
node inspectString.js $GCLOUD_PROJECT "My email address is joe@example.com."
```

**Output example:**
```shell
Findings:
        Info type: PERSON_NAME
        Likelihood: POSSIBLE
        Info type: EMAIL_ADDRESS
        Likelihood: LIKELY
```
- In Cloud Shell, run the following command:
```shell
node inspectString.js $GCLOUD_PROJECT "My phone number is 555-555-5555."
```
**Output example:**
```shell
Findings:
        Info type: PHONE_NUMBER
        Likelihood: VERY_LIKELY
```
### Make sensitive information from a string
- In Cloud Shell:
```shell
node deidentifyWithMask.js $GCLOUD_PROJECT "My phone number is 555-555-5555."
```

**Output example:**
```shell
My phone number is ************.
```
### Redact sensitive data from images
- Right-click on image below and save to local machine as `dlp-input.png`
- In bar above terminal, click button at top right with three vertical dots and select **Upload**
- Click **Choose Files**, select the downloaded **dlp-input.png** image file, and Upload it to Cloud Shell.
- From **Cloud Shell**, click **Open Editor**. This will launch the Cloud Shell code editor, which includes a file browser.
- In the Cloud Shell code editor, on the left, you should see **dlp-input.png**.
- From **Cloud Shell**, click **Open Terminal**.
- In terminal, run following command to redact email address values from image:
```shell
node redactImage.js $GCLOUD_PROJECT ~/dlp-input.png "" EMAIL_ADDRESS ~/dlp-redacted.png
```
- Open **Editor**
- In Cloud Shell code editor, click **dlp-redacted.png**. You will see the image with the domain name redacted.
