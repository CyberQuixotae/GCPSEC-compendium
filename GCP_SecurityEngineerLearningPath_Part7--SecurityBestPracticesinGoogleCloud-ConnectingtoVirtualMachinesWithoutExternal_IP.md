[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/87/video/450280)

### Connecting to virtual machines WITHOUT external IPs
- One solution is to use a **Bastion Host**
    - To implement this solution, create a second VM with a Public IP address in the same network as the instance you want to connect to.
    - Then, connect to the bastion host and from there SSH to the private VM.

- An even better practice would be to use a VPN or some other more secure form of connection, such as Cloud Interconnect, for ordinary activities.
    - Provides access directly to the instances internal IP

- **Only** using SSH with the bastion host as the maintenance avenue of **LAST RESORT**

### IAP TCP forwarding

#### Can connect using IAP TCP forwarding for SSH, RDP, and other traffic
- IAP creates a listening port on the local host
- IAP wraps all traffic from the client
- Users gain access to the interface and port if they pass the authentication and authorization check

#### Connecting to Windows with RDP
- Set the username and password using the Google Cloud console or gcloud.
- Can download an RDP file.
- From the console, click the down arrow next to the RDP button and select Set Windows password.
- From gcloud the command is: `gcloud compute reset-windows-password instance-name --user=USER HERE`
