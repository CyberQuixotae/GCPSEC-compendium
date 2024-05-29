### Google Cloud provides resource containers such as Organizations, Folders, and Projects, which allow you to group and hierarchically organize cloud resources.

- Folders can be used to implement organizational structure and/or group projects by department, team, application or environment.
    - While a folder can contain multiple child folders or other resources, each folder or resource can only have exactly one parent.
    - Folders are used to group resources that share common IAM policies.
    - You can use folder-level IAM policies to control access to the resources the folder contains.

### Service Accounts:

- There are two types of Google Service Accounts: Service accounts that Google manages, and service accounts that you manage.
- By default, you can create up to 100 user-managed service accounts in a project.

- Two types of service account keys:
    - Google-managed account keys
        - All service accounts have Google-managed keys.
        - Google stores both the public and private portion of the key.
        - Each public key can be used for signing for a maximum of two weeks.
        - Private keys are never directly accessible. Held securely in escrow

    - User-managed account keys:
        - Google only stores the public portion of a user-managed key and does not save your user-managed private keys.
        - Users are responsible for private key security. If you lose them, Google cannot help you recover them.
        - Can create up to 10 user-managed service account keys per service.
        - Can be administered via the IAM API, gcloud, or the Google Cloud console.

- Service accounts use RSA key pairs for authentication: If you know the private key of a service account's key pair, you can use the private key to create a JWT bearer token and use the bearer token to request an access token.

- The resulting access token reflects a service account's identity and you can use it to interact with Google Cloud APIs on the service account's behalf.

- To list all of the keys assicated with a service account:
`gcloud iam service-accounts keys list --iam-account service-account-email-id`



