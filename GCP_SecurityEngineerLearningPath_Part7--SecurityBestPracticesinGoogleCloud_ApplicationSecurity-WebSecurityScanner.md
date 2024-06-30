[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/87/video/450309) <!--Increment the end number by 1 for the duration of each numbered section!-->

# Web Security Scanner
- A web security scanner which probes for common vulnerabilities in App Engine, Google Kubernetes Engine, and Compute Engine applications.


### Web Security Scanner checks your applications for common vulnerabilities
- XSS
- Flash injection
- Mixed content
- Clear text passwords
- Use of insecure JavaScript libraries
- Supports categories in OWASP Top Ten


### How the scanner works
- Navigates every link it finds (except those excluded).
- Activates every control and input.
- Logs in with specified credentials.
- User-agent and maximum QPS can be configured.
- Scanner is optimized to avoid false positives.
- Vulnerabilities reported in:
    - Web Security Scanner "Results" tab
    - Security Command Center
    - Cloud Logging

### Scan scheduling
- Scans can be scheduled or manually initiated.
- Scans can be configured to run on a preset schedule.
- Scan duration scales with size and complexity of application; large apps can take hours to complete.

### Security scanner considerations
- The scanner generates real load against your application.
- The scanner can change state data in your application.

### Avoiding unwanted impact
Use one or more of the following tactics:

- Run scans in test environment
- Use test accounts
- Block specific UI elements
- Block specific URLs
- Use backup data

