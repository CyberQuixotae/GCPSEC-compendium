[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/87/video/450279)

### Connecting to virtual machines
- Linux instances on Google Cloud are accessed using SSH. Require a username and an SSH key for authentication.
    - Password authentication is disabled by default.

- Windows machines are accessed using RDP
    - Require a username and password

### SSH from Cloud Console
- Click SSH control:
    - SSH terminal session opens in a new browser tab.
        - As part of the connection process, the browser window performs an HTTPS connection to a Google Web server, which in turn creates an SSH connection to the instance.
    - Keys are automatically generated.
    - Requires the VM to have an external IP.

### SSH using Cloud SDK
- Install and initialize the Cloud SDK.
- Connect with the gcloud tool:
    - Requires firewall rule to allow IAP TCP forward traffic if no external IP address
    - Keys are automatically generated and placed in your local home/.ssh folder.

    `:~$ gcloud compute ssh web-server --zone us-central1-c`

### SSH from third-party SSH client
- Can access VMs from other SSH clients:
    - Putty on Windows
    - Terminal from Linux or Mac

- Must supply the SSH public key to the instance
    - Private key never leaves your infrastructre

### Adding SSH keys to projects
- Can add SSH keys as project metadata:
- Provide only the public key
- Automatically added to all VMs by default

### Adding SSH keys to instances
- Can configure instances to NOT use project-wide keys:
    - Can specify public key for individual instances.

- Add SSH keys to instance metadata when creating a VM:
    - Provide access to only this machine.
