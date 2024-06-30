[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/99/video/432489)

# Monitoring multiple projects
- Each project creates a metrics scope for itself and hosts monitoring configuration for itself.
    - This happens for every project you create.
        - Example: Project `svc1` will create its own metric scope to be viewed by default
- But what if you want to centralize how that data is stored and how it's accessed?
    - The answer is up to you and your org, but here are a few scope ideas.

## Every project is monitored locally, in that project.
**Advantages**
- The advantages for this approach include: Clear and obvious separation for each project.
- If the project contains development-related resources, it's easy to provide access to the dev personnel.
- Project resources and monitoring resources all in the same place.
- It is easy to automate, since monitoring becomes a standard part of the initial project setup.

**Disadvantages**
- If the application is larger than a single project, you will have limited visibility into application performance.

## Optionally, create monitoring projects for a wider perspective
- You can add multiple projects to an existing scope.
- Monitoring data for all projects in that scope will be visible.
- This will let you create dashboards, showing resources from all projects in the scope, or alerting policies that apply to resources in multiple projects.
- The recommended approach for production deployments is to create a dedicated project to host monitoring configuration data and use its metrics scope to set up monitoring for projects that have actual resources in them.

**Advantages**
- Provides a single pane of glass that offers visibility into the entire group of related resources or projects.
- It also helps compare non-prod and prod environments easily.
**Disadvantages**
- Anyone with IAM permissions to access Cloud Monitoring will be able to see metrics for all environments.
- Monitoring in prod is typically divided among different teams.
