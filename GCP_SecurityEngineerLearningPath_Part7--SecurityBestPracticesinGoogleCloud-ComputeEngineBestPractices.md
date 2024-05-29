[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/87/video/450287) <!--Increment the end number by 1 for the duration of each numbered section!-->

# Compute Engine best practices
- Control access to resources with projects and IAM.
- Isolate machines using multiple networks.
- Securely connect to Google Cloud networks using VPNs or Cloud Interconnect.
- Monitor and audit logs regularly.
- Only allow VMs to be created from **approved imaged**.
    - Use the Trusted Images Policy to enforce which images can be used in your organization
    - Harden custom OS images to help reduce the surface of vulnerability for the instance.
- Keep your deployed Compute Engine instances updated.
- Avoid using the default service account.
- Subscribe to **gce-image-notifications** to receieve notifications about Compute Engine image update releases.
    - `groups.google.com/forum/#!aboutgroup/gce-image-notifications`
