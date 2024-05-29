[Link to Lesson](https://www.cloudskillsboost.google/paths/15/course_templates/21/video/449949)

### VPC Service Controls mitigate security risks
- Unauthroized access using stolen credentials.
- Data exfiltration and compromised code.
- Public exposure of private data.
- VPC Service Controls prevent data from being copied to unauthorized resources outside the perimeter using service operations.
- VPC Service Controls provide an additional layer of security defense for Google Cloud services that is independent of IAM.

### VPC Service Controls can be configured with three tools
- Google Cloud console
- gcloud command-line tool
- Access Context Manager APIs

- Note that instead of using a perimeter bridge, we recommend using ingress and egress rules that provide more granular controls.

- VPC Service Controls can be used in a hybrid environment

### How VPC Service Controls help secure your environment
- VPC Service Controls use ingress and egress rules to allow access to and from the resources and clients protected by service perimeters.

### Six stages of a typical VPC service perimeter configuration are:

1. Create an access policy.
2. Secure Google-managed resources with service perimeters.
3. Set up VPC accessible services to add additional restrictions to how services can be used inside your perimeters (which is optional).
4. Set up private connectivity from a VPC network (again, also optional)
5. Allow context-aware access from outside a service perimeter using ingress rules (also optional)
6. Configure secure data exchange using ingress and egress rules. (Also optional)
