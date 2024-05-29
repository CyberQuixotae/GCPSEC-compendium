### Using Workload Identity Federation, you can grant on-premises or multi-cloud workloads access to data stored in Google Cloud services without service account keys.

- Service account keys are akin to user passwords, allowing the holder to act as the service account and gain access to any resource that service account has access to.

- It's a key without an expiration date and with no guarantee around where it's stored or who has access to it.

- Because of this risk, managing the storage, distribution, and rotation of service account keys becomes a top priority, effectively turning an identity management problem into a secrets management problem.

- Solution? Ditch the keys using **Workload Identity Federation**.

- To set up workload identity federation, you'll first need to create a workload identity pool in your Google Cloud project.
    -   A project can have multiple pools with each one allowing access from a different external identity provider.

- After you have your identity pool set up, your application authenticates to your identity provider and receives account credentials.
    - The application can then call a security token service to exchange the account credentials issued by your identity provider for a short-lived Google Cloud access token.
    - Afterwards, a one-way trust between your identity provider and the workload identity pool is configured by providing relevant metadata about your provider.
    - Now, when an application attempts to exchange their IDP credential, the security token service will be able to validate that the credential is from a trusted provider before issuing an access token to the application.




