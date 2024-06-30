[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/87/video/450324)

# Hardening your clusters.

## GKE hardening guidelines for robust cluster security
- Upgrade your GKE infrastructure in a timely fashion
- Monitor cluster configurations
- Restrict direct access to control planes and nodes
    - **Public endpoint access disabled**
    - **Public endpoint access enabled, control plane authorized netowrks disabled**
- Consider using Group Authentication
    - which removes the need to update your Role Based Access Control configuration whenever anyone is added or removed from the group.
- Use "least privileged" Google service accounts.
    - You should create and use a minimally privileged service account to run your GKE cluster instead of using this Compute Engine default service account.
- Restrict access to cluster resources.
- Use Shielded GKE nodes.
- Restrict traffic between pods.
- Choose a hardened node image with the container runtime.
- Use secret management.
- Restrict cluster discovery permissions.

## GKE automatically creates firewall rules
- GKE cluster firewall rules
- GKE Service firewall rules
- GKE Ingress firewall rules
- **DO NOT MODIFY OR DELETE FIREWALL RULES CREATED BY GKE**
