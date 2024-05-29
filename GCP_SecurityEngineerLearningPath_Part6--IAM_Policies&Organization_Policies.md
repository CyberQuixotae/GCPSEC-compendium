### A policy is a collection of access statements attached to a resource.

- Each policy contains a set of roles and role members, with resources inheriting policies from their parent.

- You can think of it like this: resource policies are a union of parent and resource, where a less restrictive parent policy will always override a more restrictive resource policy.

- You can grant access to Google Cloud resources by using allow policies, also known as IAM policies, which are attached to resources.

- Another way to express the hierarchy of policies is: "allowed permissions are always inherited down the resource hierarchy unless overridden by a deny policy."

- [Understanding allow policies](https://cloud.google.com/iam/docs/policies)


### Example: Simple Policy

```
{
  "bindings": [
    {
      "members": [
        "user:jie@example.com"
      ],
      "role": "roles/owner"
    }
  ],
  "etag": "BwUjMhCsNvY=",
  "version": 1
}
```

### IAM Conditions
- Specified in the role binding of a resource's IAM policy
- Enforce conditional, attribute-based access control for Google Cloud resources
- Grant resource access to identities (members) only if configured conditions are met
- Condition attributes are either based on the requested resource—for example, its type or name—or on details about the request.
    - For example, its timestamp or destination IP address.


### IAM deny policies
Lets you define deny rules that prevent certain principals from using certain permissions, regardless of the roles they're granted.

Deny policies are made up of deny rules. Each deny rule specifies:
- A set of principals that are denied permissions
- The permissions that the principals are denied, or unable to use
- Optional: the condition that must be true for the permission to be denied


### Example: Deny Policy:

```
{
  "name": "policies/cloudresourcemanager.googleapis.com%2Fprojects%2F253519172624/denypolicies/limit-project-deletion",
  "uid": "06ccd2eb-d2a5-5dd1-a746-eaf4c6g3f816",
  "kind": "DenyPolicy",
  "displayName": "Only project admins can delete projects.",
  "etag": "MTc1MTkzMjY0MjUyMTExODMxMDQ=",
  "createTime": "2021-09-07T23:15:35.258319Z",
  "updateTime": "2021-09-07T23:15:35.258319Z",
  "rules": [
    {
      "denyRule": {
        "deniedPrincipals": [
          "principalSet://goog/public:all"
        ],
        "exceptionPrincipals": [
          "principalSet://goog/group/project-admins@example.com"
        ],
        "deniedPermissions": [
          "cloudresourcemanager.googleapis.com/projects.delete"
        ],
        "denialCondition": {
          "title":  "Only for non-test projects",
          "expression": "!resource.matchTag('12345678/env', 'test')"
        }
      }
    }
  ]
}

```

### Organization policy constraints
- Configured wtih constraints
- Particular type of restriction against either a Google Cloud service or a group of Google Cloud services
- Descendants of the targeted resource hierarchy node inherit the organization policy.
    - [Using Constraints - Resource Manager](https://cloud.google.com/resource-manager/docs/organization-policy/using-constraints)

### Organization policy constraint types
- List constraint type allow or disallow from a list of values.
    - Example: `compute.vmExternalIpAccess`

- Boolean constraint type turn on or turn off policies.
    - Example: `compute.disableSerialPortAccess`

- When you set an organization policy on a resource hierarchy node, all descendants of that resource hierarchy node inherit the organization policy by default.


### Wrapping up of Section
- Organization policies and their constraints are not the same things as IAM policies and bindings.

- Organization Policies focuses on what, and lets the administrator set restrictions on specific resources, services, or groups of services to determine how they can be configured and used.

- IAM policies focus on who, and lets the administrator authorize who can take action on specific resources or services based on permissions.
