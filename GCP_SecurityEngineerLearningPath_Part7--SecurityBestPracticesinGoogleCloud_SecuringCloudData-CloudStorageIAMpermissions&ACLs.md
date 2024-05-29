[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/87/video/450291) <!--Increment the end number by 1 for the duration of each numbered section!-->

# Cloud Storage IAM permissions & ACLs

### Cloud Storage Permissions
- Members can be granted access to Cloud Storage at the organization, folder, project, or bucket levels.
- Permissions flow down from higher levels
- A deny policy can be used to further restrict access

#### Storage role permissions
##### Storage Object Admin
**Description:** Full control of storage objects.
**5** assigned permissions:
- orgpolicy.policy.get
- resourcemanager.projects.get
- resourcemanager.projects.list
- storage.objects.*
- storage.multipartUploads.*

##### Storage Object Creator
**Description:** Access to create objects in storage.
**7** assigned permissions:
- orgpolicy.policy.get
- resourcemanager.projects.get
- resourcemanager.projects.list
- storage.objects.create
- storage.multipartUploads.create
- storage.multipartUploads.abort
- storage.multipartUploads.listParts

##### Storage Object Viewer
**Description:** Read access to storage objects.
**4** assigned permissions:
- resourcemanager.projects.get
- resourcemanager.projects.list
- storage.objects.get
- storage.objects.list

#### Cloud Storage ACLs
- Access control lists (ACLs) can be used to grant access to objects in buckets.

##### Access control
- Uniform: Ensure uniform access to all objects in the bucket by using only bucket-level permissions(IAM). This option becomes permanent after 90 days.
- Fine-grained: Specify access to individual objects by using object-level permissions (ACLs) in addition to your bucket-level permissions(IAM).

##### Making buckets public:
- To make a bucket public, grant `allUsers` the **Storage Object Viewer Role**
- To make an object public, grant `allUsers` **Reader** access

