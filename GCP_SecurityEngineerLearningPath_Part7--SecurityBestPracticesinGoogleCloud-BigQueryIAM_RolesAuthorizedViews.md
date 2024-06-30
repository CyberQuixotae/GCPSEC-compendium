[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/87/video/450301) <!--Increment the end number by 1 for the duration of each numbered section!-->

# BigQuery IAM roles and authorized views

### Permissions are granted to BigQuery datasets

#### BigQuery:
- Uses IAM roles to control access to data.
- Lets you assign roles individually to certain types of resources within datasets.
- Supports access control at column and row security levels.

### BigQuery IAM roles:
BigQuery Admin: Can do everything in BigQuery. Create and read data, run jobs, set IAM policies, etc.
BigQuery Data Owner: Read/write access to data, plus can grant access to other users and groups by setting IAM policies.
BigQuery Data Editor: Read/write access to data.
BigQuery Data Viewer: Read-only access to data.
BigQuery Job User: Can create and run jobs, but no access to data.
BigQuery User: Can run jobs, create datasets, list tables, save queries. But no default access to data.

### Using BigQuery IAM roles
- Assign groups (or users) to BigQuery IAM roles.
    - Generally considered a best practice to manage users in groups.
- Provide groups or users with access to datasets.
    - Can be viewer, editor, or owner.
- The user who created a dataset is the owner.
    - Can add additional users and other owners.

### Authorized views
What if I want admins or super users to see all the data in a table, and others to see only a subset of the data?

- Use views to provide row or column level permissions to datasets.
- Create a second dataset with different permissions from the first.
- Add a view to the second dataset that selects the subset of data you want to expose from the first dataset.
- In the first dataset, you must give the view access to the underlying data.
