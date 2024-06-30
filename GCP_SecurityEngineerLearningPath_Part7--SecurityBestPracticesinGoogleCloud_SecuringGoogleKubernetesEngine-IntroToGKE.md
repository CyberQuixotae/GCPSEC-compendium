[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/87/video/450322)

# Introduction to Kubernetes/GKE

## Kubernetes containers
- K8s is a virtualized environment for running, managing, and scaling applications.
- GKE refers to the Kubernetes offering on Google Cloud.
- Each application runs as one more **containers**

## Pods and workloads
- Containers execute within **pods**
- A pod makes its environment available to containers; for example, its:
    - Network ports
    - IP address
    - Namespace
- The term **workload** is sometimes used for how to deploy a pod.

## Nodes
- Each mode:
    - Is a virtual machine.
    - Has its own instance of the OS.
- Nodes provide services to the pods.

## Clusters
- Clusters are a set of one or more nodes.
- The **control plane** (primary node) controls the other nodes in the cluster.
- GKE manages the control plane.
    - The control plane is not visible in the console.

## Secrets
- Contain sensitive data, such as passwords, OAuth tokens, and SSH keys.
- Can be encrypted.
- Are used by pods to gain access to areas where they need to accomplish tasks.
- Are maintained separately from Google Cloud secrets.

