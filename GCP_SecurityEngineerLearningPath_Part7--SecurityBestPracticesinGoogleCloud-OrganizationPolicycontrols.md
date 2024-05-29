[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/87/video/450282) <!--Increment this by 1!-->

[Setting up trusted image policies](https://cloud.google.com/compute/docs/images/restricting-image-access)
# Organization Policy Service
- Allows you to set constraints that apply to all resources in your organization's hierarchy.
- All descendents inherit the policy constraints

# Trusted Images Policy
- The compute.trustedImageProjects constraint has an interesting use case.
- Use the Trusted Images Policy to enforce which images can be used in your organization. This allows you to host organization-approved, hardened images in your Google Cloud environment.

# Trusted Images Policy example
1. Get the existing policy settings for your project by using the `resource-manager org-policies describe command.`
```bash
gcloud resource-manager org-policies describe \
   compute.trustedImageProjects --project=PROJECT_ID \
   --effective > policy.yaml
```

2. Open the policy.yaml file in a text editor and modify the compute.trustedImageProjects constraint.
```bash
constraint: constraints/compute.trustedImageProjects
listPolicy:
 allowedValues:
    - projects/debian-cloud
    - projects/cos-cloud
 deniedValues:
    - projects/IMAGE_PROJECT
```
3. Apply the policy.yaml file to your project
```bash
gcloud resource-manager org-policies set-policy \
   policy.yaml --project=PROJECT_ID
```
