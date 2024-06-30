[Link to Lesson:] (https://www.cloudskillsboost.google/paths/15/course_templates/99/video/432518)

# Best practices

## Plan and create test projects
- **Create a plan** for Data Access audit logs.
- **Create a test project** and test plan.
- **Roll out the plan**.

## Determine and set organization-level data access
**Advantages:**
- Detailed information on who accessed, edited, or deleted what and when
- Free tier
- Some free logs

**Disadvantages:**
- Logs can be large and the queries per second can be high based on the number of data access requests.

## Infrastructure as Code (IaC)
- Run open source or pay for enterprise version.
- State can be stored locally or remote in Cloud Storage or Terraform Cloud.
- You can use Terraform to enable audit logs.
- Audit logs keep you informed of the resources provisioned using an IaC tool.

## Aggregate and store your organization's logs
- Centralize or subdivide log storage by creation user-defined buckets.
- Configure a default storage location at the organization level to automatically apply a region.
- Project your audit logs storage by configuring customer-managed encryption keys (CMEK)

## Plan and configure exports
- Decide on logs
- Decide on level
- Decide on filters
- Consider the exclusions

## Principle of least privilege
- Side-channel leakage of data through logs is a common issue
- Plan the project to monitoring project relationships
- Use appropriate IAM controls on both Google Cloud based and exported logs
- Data Access audit logs contain personally identifiable information (PII)

## Configure log views
- Help control access to logs in a log bucket.
- Help control access specific to a project or a set of users.
- Help protect sensitive log data.

## Scenario:Operational monitoring
- CTO:`resourcemanager.organizationAdmin`
    - Assigns permissions to security team and service account.
    - Security team: `logging.viewer`
        - Ability to view Admin Activity audit logs.
    - Security team: `logging.privateLogViewer`
        - Ability to view Data Access audit logs.
    - Assign all permissions at organization level.
    - Control exported data access through Cloud Storage and BigQuery IAM roles.
    - Use Cloud Data Loss Prevention to **redact PII**

## Scenario: Development team monitoring Audit Logs
- Security team remains the same:
    - `logging.viewer,logging.privateLogViewer`
- Dev team: `logging.viewer` at folder level
    - See Admin Activity audit logs by dev projects in folder.
- Dev team: `logging.privateLogViewer` at folder level
    - See Data Access audit logs.
- Use Cloud Storage or BigQuery IAM to control access to exported logs.
    - Providing a dashboard might be helpful.

## Scenario: External auditors
- Provide pre-created dashboards for auditor usage.
- Provide **Logs Viewer** at organization level.
- Provide **BigQuery Data Viewer** at exported dataset.
    - Backend for dashboards.
- Use IAM and/or temporary access URLs for Cloud Storage.

