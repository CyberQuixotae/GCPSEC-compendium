### Policy Intelligence
- Tools that help you understand and manage your policies to proactively improve your security configuration

1. Find out what went wrong quickly (Troubleshooting tools)
2. Prevent mistakes from happening (Analysis tools)
3. Make improvements easily (Actionable recommendations)

### Policy Troubleshooter
- Exposes access policies that apply to a particular resources.
- Requires a member email, a resource name, and a permission to check.
- Examines all IAM policies that apply to that resource.
- Reports on whether that member's roles include that permission to that resource.
- Reports on what policies binds that user to those roles.
- Policy Troubleshooter may not always fully explain resource access.
- If you do not have access to a resource policy, it will not be analyzed.
- Maximum effectiveness requires the Security Reviewer (`roles/iam.securityReviewer`) role
- Policy troubleshooter is accessible through the console, the google cloud cli, or the rest api

### Policy Analyzer
- Which principles have what access to which Google Cloud resources?
- Examples:
  - Who can access IAM service account?
  - Who can read data in BigQuery dataset?
  - Who has access to resources in a project?

### Role recommendations (Recommender)
- Identify and remove excess permissions from your principals.
- User ML-based policy insights to analyze principal's permission usage.
- Help enforce principal of least privilege.

#### Recommender evaluations
- Recommender compares project-level role grants with permissions used within last 90 days.
- If a permission has not been used within that time, recommender will suggest revoking it.
- You have to review and apply recommendations; they will not be applied automatically.

#### Recommender evaluation type
- Revoke an existing role.
- Replace an existing role.
- Add permissions to an existing role.

