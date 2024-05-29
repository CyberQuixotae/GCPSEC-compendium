[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/87/video/450276)

### Service accounts, IAM roles, and API scopes

- Compute Engine virtual machines can run under a particular service account - or not be assigned any service account.

### Default service account
- Created automatically when the Compute Engine is enabled.
- Assigned the Project Editor role.
- Used by default when creating a VM.

### Create service accounts using IAM
- You can also create and manage your own service accounts using Identity and Access Management.
- These user-managed service accounts are granted “necessary” permissions just like any member in IAM - by assigning roles.
- This gives you full control over exactly which permissions the service account will have.

### Assign custom service accounts to machines
- Access to APIs controlled by the roles, not by scopes:
    - Assign 1 or more roles to those service accounts.
    - Scopes are only used by default service accounts.
    - The only difference is user-managed service accounts do not use the “access scope” concept
        - Instead, permissions are controlled through the IAM roles assigned to the account.
            - Applications running on instances associated with the service account can make authenticated requests to other Google APIs using the service account identity.

### Scopes control what VMs can do
- The default service account has Project Editor role - this can be dangerous.
- Scopes are used to limit permissions when using the default service accounts.

### Setting Access Scopes

#### Allow default access
- The default access scope is actually very narrow and allows **read-only** access to Cloud Storage, as well as access to Cloud Logging and Cloud Monitoring.

#### Allow full access scope
- Machines often need access to other APIs like BigQuery, Datastore, Cloud SQL, Pub/Sub, Cloud Bigtable
- Not a best practice

#### Set access for each API with scopes
- Can grant access to only the APIs required by the programs running on the machine:
- Choose only the scopes required by your application
- Better practice than granting full access
