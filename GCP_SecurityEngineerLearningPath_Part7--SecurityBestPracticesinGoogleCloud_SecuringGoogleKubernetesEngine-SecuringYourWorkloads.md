[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/87/video/450325)

# Securing your workloads with Workload Identity

## Securing workloads with pod container process privileges
**Limit pod container process privileges**
- Critical to securing workloads and clusters.
- Set security-related options via Security Context on both pods and containers.
    - Allow you to change the security settings of your workload processes.
- Change settings at the cluster level requires implementation of `PodSecurityPolicy` or `PodSecurity` admission controllers.

## Securing workloads with Workload Identity
**Challenges:**
- Applications typically use and rely on a variety of services.
- Applications running on GKE must authenticate to use Google Cloud APIs.
    - Authentication has been a challenge, requiring workarounds and suboptimal solutions.

*Solution?* **Workload Identity!**
    - Configure a Kubernetes service account to act as a Google service account.
    - Permit your workloads to automatically access other Google Cloud services.
- Enables you to assign fine-grained identity and authorization for applications in your cluster.

**Benefits**
- Recommended way to access Google Cloud services from applications running within GKE.
    - Improves security properties and manageability.
- Easy to assign identity and prove it to external identity solutions
- Strong Security guarantees
- Enforces principle of least privilege
- Preserves Kubernetes abstraction layer

## Securing workloads with Binary Authorization
- Binary authorization allows you to enforce deploying only trusted containers into GKE.
- Enable Binary Authorization on your GKE cluster.
- Add a policy that requires signed images.
- When an image is built by Cloud Build an "attestor" verifies that it was from a trusted repository (Source Repositories, for example).
- Container Registry includes a vulnerability scanner that scans containers.

