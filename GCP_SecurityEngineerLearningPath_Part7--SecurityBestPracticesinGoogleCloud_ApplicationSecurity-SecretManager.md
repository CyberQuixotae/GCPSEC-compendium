[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/87/video/450316)

# Secret Manager

## Storing Credentials Securely
- Many applications require credentials to authenticate; for example, API keys, passwords, or certificates.
- Storing this information in a flat text file makes the information easy to access, but it requires file protection.
- Secret Manager provides a secure, convenient way to store sensitive information.

## Secret Manager features
- Global names and replication
- Versioning
- Follows principles of least privilege
- Audit logging
- Strong encryption

## Access control using IAM
- By default, only project owners can create and access secrets within their project.
- Use IAM to grant roles and permissions at the level of the Google Cloud organization, folder, project, or secret.

## Working with IAM roles
- IAM roles:
    - `secretmanager.admin`: Can view,edit, and access a secret.
    - `secretmanager.secretAccessor`: Can only access secret data.
    - `secretmanager.viewer`: Can view a secret's metadata and its versions, but can't edit or access secret data.
- As always, apply permissions at the lowest level of the resource hierarchy to obtain the result you desire.

## Versioning
- Secrets can be versioned.
- Each version is assigned a version ID.
- The most recent version is automatically assigned the label `latest`
- Secrets cannot be modified, but they can be disabled or deleted.
- Individual versions can be seleted and disabled or destroyed.

## Secret rotation
- To rotate a secret, add a new version to it.
- Any enabled version can be accessed.
- Secrets Manager supports rotation scheduled on secrets.
    - Sends messages to Pub/Sub topics configured on the secret based on the provided rotation frequency and rotation time.

## Admin Activity Access audit logs
- Admin Activity Access audit logs cannot be disabled.
- All activity that creates or changes secret data is logged here.
- Setting or getting IAM policy information about secrets is logged.

## Data Access audito logs
- Data Access audit logs are disabled by default.
- If logs are enabled, all access to the secret data is logged.

