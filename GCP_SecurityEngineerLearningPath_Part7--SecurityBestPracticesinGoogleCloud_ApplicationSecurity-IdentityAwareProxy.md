[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/87/video/450313)

# BeyondCorp Enterprise and Identity-Aware Proxy

### BeyondCorp (zero trust) security model
- Access is granted based on a **user's identity and context** of the request.
- Shifts controls from the **network** layer to the **application** layer.
- Allows users to work from **any location & device**.
    - It started as an internal Google initiative to enable every employee to work from untrusted networks without the use of a traditional VPN.

### BeyondCorp Enterprises uses
BeyondCorp Enterprise lets you:
- Protect sensitive data
- Ensure key systems only accesible from certain devices
- Provide DLP for corporate data
- Gate access based on user location
- Protect apps in hybrid deployments

### Enforcement points
- Cloud Identity
- VPC Service Controls
- IAP

### Cloud Identity - for Google Workspace apps
- Extend content-aware for Google Workspace tools
- Enforce access controls for Gmail, Docs, Sheets
- 3rd party solutions via SAML

### VPC Service Controls - for Google Cloud APIs
VPC Service Controls allow users to define a security perimeter around Google Cloud resources.

With VPC Service Controls, you can:
- Enforce context-aware access.
- Mitigate data exfiltration risks.
- Extend security boundaries across cloud environments.
- Centrally manage security policies.

### IAP - for web apps/VMs

**A reverse proxy sits in front of every data request**
- Provides a central authentication and authorization layer for applications over HTTPS.
- Replaces end-user VPN tunnels.
- Replaces authentication and authorization layers nedded for web applications hosted on Google Cloud.

#### The proxy needs to have near zero latency to provide "invisible" security.

### Identity-Aware Proxy (IAP)
- Controls access to your cloud applications running on Google Cloud.
- Verifies a user's identity.
- Determines whether that user should be allowed to access the application.

### IAP provides a simpler administration process
- Deploys in minutes
    - No VPN to implement/maintain
    - No VPN clients to install
- Saves end user time
- Faster to sign in to than a VPN


