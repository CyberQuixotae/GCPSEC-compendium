[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/87/video/450281)

# OS Login - Overview
- Manage SSH access to your instances using IAM without having to create and manage individual SSH keys.
- Maintains a consistent Linux user identity across VM instances
- Recommended way to manage many users across multiple instances or projects.
- Simplifies SSH access management by linking your Linux user account to your Google identity.

# OS Login - Benefits
- Automatic Linux account lifecycle management
    - Fine grained authorization using IAM
        - For example, you can grant a user permissions to log into the system, but not the ability to run commands such as sudo.
    - Automatic permission updates: With OS Login, permissions are updated automatically when an administrator changes IAM permissions.
        - For example, if you remove IAM permissions from a Google identity, then access to VM instances is revoked.
    - Ability to import existing Linux accounts
        - Administrators can choose to optionally synchronize Linux account information from Active Directory (AD) and Lightweight Directory Access Protocol (LDAP) that are set up on-premises.
    - Supports 2-factor authentication




