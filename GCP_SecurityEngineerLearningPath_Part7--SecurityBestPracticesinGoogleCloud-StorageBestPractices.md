[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/87/video/450304) <!--Increment the end number by 1 for the duration of each numbered section!-->

# Storage best practices for Cloud Storage and BigQuery Storage

### For Cloud Storage

#### DO NOT USE:
- USER IDs
- EMAIL ADDRESSES
- PROJECT NAMES
- PROJECT NUMBERS
- ANY PERSONALLY IDENTIFIABLE INFORMATION IN BUCKET NAMES
    - BECAUSE ANYONE CAN PROBE FOR THE EXISTENCE OF A BUCKET

Remember, Cloud Storage bucket names must be unique across the entire Cloud Storage namespace, so come up with a naming convention.

- If you need a lot of buckets, use GUIDs or an equivalent for bucket names
    - Put retry logic in your code to handle name collisions
    - Keep a list to cross-reference your buckets

- Use signed URLs to provide access for users with no account.
- Don't allow buckets to be publicly writable.
- Use lifecycle rules to remove sensitive data that is no longer needed.

### BigQuery storage best practices
- Use IAM roles to separate who can create and manage Datasets versus who can process the data.
    - Be careful when giving all authenticated users access to data.
- Use authorized views to restrict access to sensitive data:
    - Principle of least privilege
- Use the expiration settings to remove unneeded tables and partitions.

---

[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/87/video/450305) <!--Increment the end number by 1 for the duration of each numbered section!-->

# Module review
- Cloud Storage buckets can be given access permissions at the Organization, folder, project or bucket levels.
- Administrative operations on buckets is logged automatically.
    - Data operations are not and have to be configured.
- Signed URLs and Signed Policy Documents give limited time permissions to read, write, and upload to users who do not have Google accounts.

- BigQuery datasets can have permissions granted at the dataset, table, row and column level.
- Do not use any personally identifiable information as bucket or object names.Object names and bucket names will appear in URLs!
- Assign lifecycle management rules to a bucket to automatically downgrade or delete data.



