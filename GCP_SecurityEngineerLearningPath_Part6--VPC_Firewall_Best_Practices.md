### Best Practices
1. Use the model of least privilege
2. Minimize direct exposure to/from the internet.
    - To do this avoid having “allow” firewall rules defined with the source or destination range set to 0.0.0.0/0.
3. Prevent ports and protocols from being exposed unnecessarily.
4. Develop a standard naming convention for firewall rules.
    - `{direction}-{allow/deny}-{service}-{to-from-location}`
    - `Ingress-allow-ssh-from-onprem`
    - `egress-allow-all-to-gcevms`
5. Consider service account firewall rules instead of tag-based rules.

### Hierarchical firewall policies
- Let you create and enforce a consistent firewall policy across your organization.
- You can assign hierarchical firewall policies to the organization as a whole or to individual folders.
- Similar to hierarchical firewall policies, these network firewall policy structures act as a container for firewall rules.

### Firewall Insights
- Produces data about how your firewall data is being used in order to make better decisions about optimizing your firewall rules.
- Recommender tool that generate Insights for individual Google products regarding your firewall rules.
