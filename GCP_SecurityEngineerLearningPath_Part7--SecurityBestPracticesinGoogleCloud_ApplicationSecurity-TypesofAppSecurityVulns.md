[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/87/video/450308) <!--Increment the end number by 1 for the duration of each numbered section!-->

# Types of application security vulnerabilities
- Developers are frequently given a requirements document that defines the desired features and functional requirements for the application.
    - Security is often neglected
        - Often undefined and remains untested
- Deadline pressures also promote the release of vulnerable code; Attackers also know this and will attack applications more often than any other target - more often than networks, more often than infrastructure.

### Common application vulnerabilities

#### Injection
- Injection flaws occur when some form of malicious content can be “injected” into an application from an attacker and the application will then accept and interpret that content.
    - SQL injection
    - LDAP injection
    - HTML injection

#### Cross-site scripting (XSS)
- Cross-site scripting is actually a form of injection where the attacker is able to inject javascript into an application, and the code injection originates from a different site.
    - Cross-site scripting allows attackers to execute scripts in the victim's browser which can then hijack user sessions, deface web sites, or redirect the user to other malicious sites.

#### Weak authentication and access control
- When insufficient control over authentication and access is exercised, this vulnerability allows attackers to compromise passwords, keys, or session tokens, or to exploit other implementation flaws to assume other users' identities.

#### Sensitive data exposure
- Attackers may steal or modify weakly-protected data to facilitate credit card fraud, identity theft, or other data and identity crimes.
    - Sensitive data risks being compromised any time it is transferred without extra protection. Secure data transfer requires encryption at rest or in transit, and special precautions when exchanged with the browser.

#### Security misconfiguration
- Security misconfiguration is commonly a result of insecure default configurations, incomplete or ad hoc configurations, open cloud storage, misconfigured HTTP headers, and verbose error messages containing sensitive information.

#### Using components with known vulnerabilities
- Components, such as libraries, frameworks, and other software modules generally run with the same privileges as the main application itself.


