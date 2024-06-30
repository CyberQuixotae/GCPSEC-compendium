[Link to Lab:](https://www.cloudskillsboost.google/paths/15/course_templates/87/labs/450318)

# Objectives
In this lab, you learn to:
- Enable the Secret Manager API.
- Create and use a new secret.
- Create a new version of a secret, and disable the old version(s).
- Reinstate and verify an older version of a secret.

## Enable the Secret Manager API
- **Navigation menu** > **API & Services**
- Top of page, click **Enable API and Services**
- Enter `Secret Manager` in searchbox, the result you want is: `Secrets Manager API`
- Click **Secret Manager API** > click **Enable** on page

## Create a secret
- **Navigation menu**  **Security** > **Secret Manager**
- On Secret Manager main page, click **+ Create Secret**
- **Name** = `password`
- **Secret value** = `xyzpdq`
- Click **+ Add Label.**
- Key Value Pair = `team::acme`
- Click **Create Secret**

## Use a secret
- Activate Cloud Shell and wait for machine to provision.
- At Cloud Shell Terminal enter:
```shell
gcloud secrets versions access 1 --secret="password"
```
## Create and use a new secret version
- **Navigation menu** of Google Cloud Console, select **Security > Secret Manager**
- Under **Actions**, click the More actions menu (i.e., the “three dots” menu) and then click **Add New Version**.
- **Secret value** = `abc123`
- Click **Add New Version**

## Use the new secret
- At Cloud Shell Terminal, enter:
```shell
gcloud secrets versions access 2 --secret="password"
```
- Use the latest alias:
```shell
gcloud secrets versions access latest --secret="password"
```

## Create a new secret version (and invalidate previous versions)
- **Navigation menu** of Google Cloud Console, select **Security > Secret Manager**
- Under **Actions**, click the More actions menu (i.e., the “three dots” menu) and then click **Add New Version**
- **Secret value** = `def123`
- Select **Disable all past versions** checkbox.
- Click **Add New Version**
- Verify that only the latest version is accessible.
```shell
gcloud secrets versions access latest --secret="password"
```
- Try to access version 2:
```shell
gcloud secrets versions access 2 --secret="password"
```
It will produce the following type of error:

```shell
ERROR: (gcloud.secrets.versions.access) FAILED_PRECONDITION: Secret Version [projects/[PROJECTIDHERE]/secrets/password/versions/2] is in DISABLED state.
```
## Reinstate and verify a previous secret version
- **Navigation menu** of Google Cloud Console, select **Security > Secret Manager**
- Click **password** secret. Note all three versions are shown. Version 3 should be **enabled** and versions 1, 2 are **disabled**
- For Version 2, under **Actions**, click **More > Enable**
- Click **Enable Selected Versions**. Version 2 should be enabled in `Status` column
- At Cloud Shell Terminal, enter:
```shell
gcloud secrets versions access 2 --secret="password"
```
You should see the version 2 value of the password secret (abc123)

