## Date:2024-04-04
## Tags: #GCP #GoogleCloud
# Google Cloud PCSE Certification Notes

#### Utilize the [Course Resources](https://www.cloudskillsboost.google/paths/15/course_templates/397/documents/455189) for each module. Try not to repeat information that already exists.

---
# Module 2 Review Topics and Links
##### 2.1 - Configuring boundary segmentation

- **Configuring network perimeter controls (firewall rules, hierarchical firewall policies, Identity-Aware Proxy (IAP), load balancers, and Certificate Authority Service)**

- **Differentiating between private and public IP addressing**

- **Configuring web application firewall (Google Cloud Armor)**

```
gcloud compute security-policies rules create priority
	--security-policy sec-policy
	--src-ip-ranges=source-range
	--action=throttle
	--rate-limit-threshold-count=200
	--rate-limit-threshold-interval-sec=3600
	--conform-action=allow
	--exceed-action=deny-429
	--enforce-on-key=HTTP-HEADER
```


- **Deploying Secure Web Proxy**

- **Configuring Cloud DNS security settings**

- **Continually monitoring and restricting configured APIs**

##### Links:
- [VPC Design - Isolate Data](https://cloud.google.com/architecture/best-practices-vpc-design#isolate-data)
- [VPC Design - Isolate VMs Service Accounts](https://cloud.google.com/architecture/best-practices-vpc-design#isolate-vms-service-accounts)
- [Best Practices for securing Service Accounts](https://cloud.google.com/iam/docs/best-practices-for-securing-service-accounts)
- [Cloud Armor - Update Security Policy Rules](https://cloud.google.com/sdk/gcloud/reference/compute/security-policies/rules/update)
- [Cloud Armor - Security Policies for HTTPS](https://cloud.google.com/armor/docs/security-policy-concepts#security_policies_for_https_load_balancing)
- [Set up a classic Application Load Balancer with a managed instance group backend](https://cloud.google.com/load-balancing/docs/https/ext-https-lb-simple)
- [Preventing VMs from being reached from the public internet](https://cloud.google.com/solutions/connecting-securely#preventing_vms_from_being_reached_from_the_public_internet)

- - -
##### 2.2 - Configuring boundary segmentation

- **Configuring security properties of a VPC Network, VPC Peering, Shared VPC, and Firewall Rules**
	- [VPC Networks](https://cloud.google.com/vpc/docs/vpc)
  
- **Configuring network isolation and data encapsulation for N-tier applications**
	![[firewall-service-accounts-example.svg]]
	`Figure 2. - A firewall rule allows traffic from a VM with the service account my-sa-webserver to port 1443 of a VM with the service account my-sa-database.`

- **Configuring VPC Service Controls**

##### Links: 
- [DNS Zones Overview - Peering Zones](https://cloud.google.com/dns/docs/zones/zones-overview#peering_zones)
- [Use VPC Firewall Rules - Cloud NGFW](https://cloud.google.com/vpc/docs/using-firewalls#serviceaccounts)
- [Best practices and reference architectures for VPC design - Isolate sensitive data](https://cloud.google.com/architecture/best-practices-vpc-design#isolate-data)
- [Best practices and reference architectures for VPC design - Isolate VMs using service accounts](https://cloud.google.com/architecture/best-practices-vpc-design#isolate-vms-service-accounts)
- [Best practices for securing service accounts](https://cloud.google.com/iam/docs/best-practices-service-accounts)
- [VPC firewall rules](https://cloud.google.com/firewall/docs/firewalls)
- [Allowing Traffic between service accounts in different subnets](https://cloud.google.com/firewall/docs/using-firewalls#serviceaccounts)


- - - 
##### 2.3 - Establishing private connectivity

- **Designing and configuring private connectivity between VPC networks and Google Cloud Projects (Shared VPC, VPC Peering, and Private Google Access for on-premises hosts)**

- **Designing and configuring private connectivity between data centers and VPC network (HA-VPN, IPsec, MACsec, and Cloud Interconnect)**

- **Establishing private connectivity between VPC and Google APIs (Private Google Access, Private Google Access for on-premises hosts, restricted Google access, Private Service Connect)**

- **Using Cloud NAT to enable outbound traffic***

##### Links: 
- [App Engine - Connecting to a Shared VPC network](https://cloud.google.com/appengine/docs/standard/connecting-shared-vpc)
- [Configure Serverless VPC access connector](https://cloud.google.com/vpc/docs/configure-serverless-vpc-access#create-connector)
- [Overview of VPC Service Controls - Extend perimeter to authorized VPN or Cloud Interconnect](https://cloud.google.com/vpc-service-controls/docs/overview#hybrid_access)
- [Choosing a Network Connectivity product](https://cloud.google.com/network-connectivity/docs/how-to/choose-product)
- [VPC - Private Google Access Supported](https://cloud.google.com/vpc/docs/private-google-access#pga-supported)
- [Cloud DNS - Create Private Zone](https://cloud.google.com/dns/docs/zones#create-private-zone)
- [Private Google Access for on-premises hosts](https://cloud.google.com/vpc/docs/private-google-access-hybrid)
- [Simplifying cloud networking for enterprises](https://cloud.google.com/blog/products/networking/simplifying-cloud-networking-for-enterprises-announcing-cloud-nat-and-more)
- https://cloud.google.com/nat/docs/gke-example
- https://cloud.google.com/nat/docs/overview

---

# Module 3 Review Topics and Links

#### Securing data at Cymbal Bank
- **Protecting sensitive data**
- **Managing encryption at rest**
- **Data Security**
- **Data Loss Prevention**

- **They will be using Sensitive Data Protection to scan data for personally identification information (PII) or other sensitive data types.**
	- **Sensitive Data Protection lets you:**
		- **Select from built-in data patterns for global or country-specific types of sensitive data**
		- **Define new data patterns to scan, detect, and optionally, transform your data**
		- **Work with image and PDF files to perform optical character recognition (OCR)**

- **Ensure least privilege access to data**
	- **Granular access control at organization, folder, project, or lower levels**
		- **Cloud Storage:**
			- **Bucket level or object level access control**
			- **IAM or Access-control lists (ACL)**
		- **BigQuery:**
			- **Dataset, table, or view level access control**
			- **Sub-table access control with row or column level security or authorized views**

- **Protect secret key-value data with Secret Manager**
	- **Using Google Cloud Secret Manager:**
		- **Access control can be granted at the individual secret level.**
		- **Secrets can be independently encrypted, versioned, rotated, and have expiry periods set.**
		- **Changes to secrets can trigger notifications.**

- **All data at rest is encrypted by default in Google Cloud using a multi-level encryption scheme**
	![[Pasted image 20240411120358.png]]

- **Manage your data lifecycle in Cloud Storage**
	- **Retention policies or object holds prevent accidental overwrite or deletion**
	- **Object versioning lets you read or recover past versions of objects**
	- **Lifecycle management rules automatically delete or change the storage class of objects based on age or other factors**
	- ![[Pasted image 20240411120635.png]]

- **Planning for security and privacy in AI**
	- **Understand data classification and access control**
	- **Enable data encryption at rest and in transit**
	- **Implement Data Loss Prevention (DLP) controls**
	- **Leverage Identity and Access Management (IAM)**
	- **Implement access monitoring and auditing**
	- **Conduct regular security assessments**
	- **Embrace zero trust security paradigm**
	- **Integrate security into development and deployment processes**
	- **Stay updated on security threats and vulnerabilities**
	- **Obtain external security assessments**
---
##### 3.1 - Protecting sensitive data and preventing data loss
- **Inspecting and redacting personally identifiable information (PII)**
- **Ensuring continuous discovery of sensitive data (structured and unstructured)**
- **Configuring pseudonymization**
- **Configuring format-preserving encryption**
- **Restricting access to BigQuery, Cloud Storage, and Cloud SQL datastores**
- **Securing secrets with Secrets Manager**
- **Protecting and managing compute instance metadata**

##### Links: 
- [Image inspection and redaction](https://cloud.google.com/sensitive-data-protection/docs/concepts-image-redaction)
- [Redacting sensitive data from images](https://cloud.google.com/dlp/docs/redacting-sensitive-data-images)
- [InfoType detector reference](https://cloud.google.com/sensitive-data-protection/docs/infotypes-reference)
- [Date shifting](https://cloud.google.com/sensitive-data-protection/docs/concepts-date-shifting)
- [InfoTypes and infoType detectors](https://cloud.google.com/sensitive-data-protection/docs/concepts-infotypes)
- [Sensitive Data Protection - Pseudonymization](https://cloud.google.com/sensitive-data-protection/docs/pseudonymization)
- [BigQuery - Authorized views and materialized views](https://cloud.google.com/bigquery/docs/authorized-views)
- [BigQuery - Authorized datasets](https://cloud.google.com/bigquery/docs/authorized-datasets)
- [Secret Manager - Access control with IAM](https://cloud.google.com/secret-manager/docs/access-control)
- [VPC Service Controls - Create a perimeter bridge](https://cloud.google.com/vpc-service-controls/docs/create-perimeter-bridges)
- [Context-aware access with ingress rules](https://cloud.google.com/vpc-service-controls/docs/context-aware-access)
- [IAM Overview - All Users](https://cloud.google.com/iam/docs/overview#all-users)

---
##### 3.2 - Managing encryption at rest, in transit, and in use
- **Identifying use cases for Google default encryption, customer-managed encryption keys (CMEK), Cloud External Key Manager (EKM), and Cloud HSM**
- **Creating and managing encryption keys for CMEK and EKM**
- **Applying Google's encryption approach to use cases**
- **Configuring object lifecycle policies for Cloud Storage**
- **Enabling confidential computing**

##### Links:
- [Cloud Storage - Storage Classes](https://cloud.google.com/storage/docs/storage-classes)
- [Cloud Storage - Object Lifecycle Management](https://cloud.google.com/storage/docs/lifecycle)
- [GKE - Use CMEK-protected node boot disks](https://cloud.google.com/kubernetes-engine/docs/how-to/using-cmek#boot-disks)
- [GKE - Configuring a custom boot disk](https://cloud.google.com/kubernetes-engine/docs/how-to/custom-boot-disks)
- [Cloud KMS Keys - CMEK integrations](https://cloud.google.com/kms/docs/use-keys-google-cloud#cmek_integrations)
- [Compute Engine - Confidential VM overview](https://cloud.google.com/confidential-computing/confidential-vm/docs/confidential-vm-overview)
- [Cloud KMS - Rotate a key](https://cloud.google.com/kms/docs/rotating-keys)

---
##### 3.3 - Planning for security and privacy in AI
- **Implementing security controls for AI/ML systems (e.g., protecting against unintentional exploitation of data or models)**
- **Determining security requirements for IaaS-hosted and PaaS-hosted training models**
##### Links:
- [Security & Identity Blog - How Sensitive Data Protection can help secure generative AI workloads](https://cloud.google.com/blog/products/identity-security/how-sensitive-data-protection-can-help-secure-generative-ai-workloads)
- [PaaS vs IaaS vs SaaS vs CaaS: How are they different?](https://cloud.google.com/learn/paas-vs-iaas-vs-saas)

---
# Module 4 Review Topics and Links

### Cymbal Bank's security operations
##### Managing security operations at Cymbal Bank
- **Building and deploying secure infrastructure and applications**
- **Configuring logging, monitoring, and detection**

##### Automated security operations in CI/CD pipelines

![[Pasted image 20240411150753.png]]

- **Confirming that most recent and secure versions of third-party software and dependencies are used;**
- **Scanning code for security vulnerabilities;**
- **Ensuring only software that passes checks and tests and is built by approved CI/CD pipelines can be deployed into production systems; and,** 
- **Detecting errors in production deployments and rolling back to the last stable build**
##### Infrastructure as code (IaC) for infrastructure creation and updates in CI/CD
- **Terraform** can be used to **create immutable infrastructure** which can be modified or deleted and **recreated quickly** in an automated response to incidents or attacks

- **Packer** can be used to **create baked images** so software and configurations of virtual machines can remain fixed, reducing chance of insecure configuration.
##### Binary authorization to enforce secure container image deployment
- ![[Pasted image 20240411151622.png]]
- When an image is built by **Cloud Build** an “attestor” verifies that it was from a **trusted repository**, built by a **specific pipeline**, **passed tests**, and was **scanned for vulnerabilities**
	- These attestations will automatically allow or block container images from being deployed into production systems.

- **Artifact Registry** includes a vulnerability scanner that scans containers and results can be used to apply attestations allowing or blocking deployment

##### Shielded Virtual Machines
- Google Cloud Shielded VMs ensure integrity of the VM
- Secure boot prevents loading of malicious code during bootup
- Measured b oot checks for modified components during bootup

##### Security monitoring and incident response process
- ![[Pasted image 20240411152158.png]]
#### Cloud Audit Logs to detect invalid administrative activity
- **Audit logs provide a complete capture of administrative activity and should be periodically audited to ensure compliance**
	- **Optionally enable data access logs to capture reads and writes to managed data storage**
	- **Optionally export logs for long-term storage or analysis**
![[Pasted image 20240411152536.png]]
##### Security Command Center
- Some of the features provided include:
	- **Asset discovery and inventory**
	- **Sensitive data discovery**
	- **Web application vulnerability detection**
	- **Access control monitoring**
	- **Real time notifications**
	- **Audit logs**
	- **Assessment of misconfigurations**

---
#### 4.1 - Automating infrastructure and application security
- **Automating security scanning for Common Vulnerabilities and**
**Exposures (CVEs) through a continuous integration and delivery CI/CD pipeline**
- **Configuring Binary Authorization to secure GKE clusters or Cloud Run**
- **Automating virtual machine image creation, hardening, maintenance, and patch management**
- **Automating container image creation, verification, hardening, maintenance, and patch management**
- **Managing policy and drift detection at scale (custom organization policies and custom modules for Security Health Analytics)**

#### Links
- [Use On-Demand Scanning in your Cloud Build pipeline](https://cloud.google.com/artifact-analysis/docs/ods-cloudbuild)
- [Container scanning overview](https://cloud.google.com/artifact-analysis/docs/container-scanning-overview#severity_levels_for_vulnerabilities)
- [Shielded VM - Integrity Monitoring](https://cloud.google.com/compute/shielded-vm/docs/shielded-vm#integrity-monitoring)
- [Shielded VM - Monitoring integrity on Shielded VMs](https://cloud.google.com/compute/shielded-vm/docs/integrity-monitoring)
- [Creating custom shielded images](https://cloud.google.com/compute/shielded-vm/docs/creating-shielded-images)
- [Compute Engine - Enable guest operating system features on custom images](https://cloud.google.com/compute/docs/images/create-custom#guest-os-features)
- [Compute Engine - Share images within organization](https://cloud.google.com/compute/docs/images/managing-access-custom-images#share-images-within-organization)
- [Image management best practices](https://cloud.google.com/compute/docs/images/image-management-best-practices)
- [Automating deployments](https://cloud.google.com/build/docs/deploying-builds/deploy-gke#automating_deployments)
- [Build an image using a build config file](https://cloud.google.com/build/docs/build-push-docker-image#build_an_image_using_a_build_config_file)
- [GKE - Modern CI/CD with GKE: A software delivery framework](https://cloud.google.com/kubernetes-engine/docs/tutorials/modern-cicd-gke-user-guide)

---
#### 4.2 - Configuring logging, monitoring, and detection
- **Configuring and analyzing network logs (Firewall Rules Logging, VPC flow logs, Packet Mirroring, Cloud Intrusion Detection System (Cloud IDS), Log Analytics)**
- **Designing an effective logging strategy**
- **Logging, monitoring, responding to, and remediating security incidents**
- **Designing secure access to logs**
- **Exporting logs to external security systems**
- **Configuring and analyzing Google Cloud audit logs and data access logs**
- **Configuring log exports (log sinks and aggregated sinks)**
- **Configuring and monitoring Security Command Center**

#### Links
- [GKE - Audit logging](https://cloud.google.com/kubernetes-engine/docs/concepts/security-overview)
- [Cloud Audit Logs overview](https://cloud.google.com/logging/docs/audit)
- [Cloud Audit Logs with Cloud Storage](https://cloud.google.com/storage/docs/audit-logging)
- [Enable Data Access audit logs](https://cloud.google.com/logging/docs/audit/configure-data-access)
- [Scenarios for exporting Cloud Logging: Compliance requirements](https://cloud.google.com/architecture/exporting-stackdriver-logging-for-compliance-requirements)
- [Security Command Center - Anomaly Detection](https://cloud.google.com/security-command-center/docs/concepts-security-sources#anomaly_detection)
- [Configuring Security Command Center](https://cloud.google.com/security-command-center/docs/how-to-configure-security-command-center)
- [Security Command Center - Enabling real-time email and chat notifications](https://cloud.google.com/security-command-center/docs/how-to-enable-real-time-notifications)
## Module 5  - Supporting Compliance Requirements - Review Topics and Links

### Cymbal Bank's security regulatory compliance
#### Ensuring security regulatory compliance at Cymbal Bank
- **Determining regulatory requirements for the cloud**
- **Can include such standards as HIPAA, PCI-DSS, The ISO 27000 Series, The NIST cybersecurity framework, CIS critical security controls, FedRAMP, SOC1 and SOC2, and many others**
- **Requirements related to:**
	- **How authentication, authorization, and access control can be performed;**
	- **How data is encrypted and otherwise secured;**
	- **How key management is performed; and,**
	- **How networks, computing, and storage resources are monitored, secured, and maintained

- #### **Google Cloud meets many third-party and government compliance standards worldwide**
	- **Google Cloud has been certified as secure, but that does not mean that applications built on Google Cloud are automatically certified.**
	- **Cymbal Bank does not need to worry about getting Google Cloud tools and services certified, only those services you build on top of Google Cloud.**
#### Cymbal Bank collaborates with Google Cloud to ensure security compliance
- **Google is responsible for managing its**
**infrastructure security**
- **You are responsible for securing your virtual**
**infrastructure, workloads and data**
- **Google helps you with best practices, templates,**
**products, and solutions**
![[Pasted image 20240411162506.png]]

#### Encryption in the context of security compliance
- **Default at rest encryption provided by Google Cloud**
- **Options for encryption at rest with varying degrees of control over keys and key storage**
- **Optional hardened hardware-based key storage with Cloud HSM**
- **Default encryption in motion when data is transferred across physical boundaries controlled by Google Cloud**
- **Optional application layer encryption in motion for auditable end-to-end encryption**
#### Sensitive Data Protection and granular access control for data security compliance
- **Use Sensitive Data Protection to scan, classify, and label data with metadata indicating sensitivity**
- **Transform sensitive data to allow processing while preventing exposure**
- **Apply granular access control to data to ensure correct access based on sensitivity**
- ![[Pasted image 20240411164102.png]]

#### VPC service controls for data residency and location-based access requirements
- **Coupled with isolated VPC networks, services and data can be locked down to be accessible only from fixed hardened endpoints**
- **VPCs can be configured with subnets in only certain regions which when combined with VPC service controls can constrain access to data from only those locations**
- ![[Pasted image 20240411164333.png]]

#### Network isolation to support regulatory compliance
- **Separate isolated VPCs can:**
	- **Guarantee better workload isolation.**
	- **Help satisfy compliance requirements that depend on workload isolation.**
	- **Facilitate meeting location-based requirements when combined with VPC service controls.**
	- ![[Pasted image 20240411164635.png]]

#### Setting policy to ensure compliance
- **Organization policy constraints can be applied to the**
**organization or any folder or project and restrict how Google Cloud can be used**
- **Compliance may require auditable least privilege and separation of duties in access control policies**
- ![[Pasted image 20240411164903.png]]

---

#### 5.1 - Determining regulatory requirements for the cloud
- **Determining concerns relative to compute, data, network, and storage**
- **Evaluating the shared responsibility model**
- **Configuring security controls within cloud environments to support compliance requirements (regionalization of data and services)**
- **Restricting compute and data for regulatory compliance (Assured Workloads, organizational policies, Access Transparency, Access Approval)**
- **Determining the Google Cloud environment in scope for regulatory compliance**
##### Links
- [Cloud Storage - Upload an object by using CSEK](https://cloud.google.com/storage/docs/samples/storage-upload-encrypted-file#storage_upload_encrypted_file-python)
- [Cloud KMS - Customer-managed encryptioon keys (CMEK)](https://cloud.google.com/kms/docs/cmek)
- [Cloud Storage - Customer-supplied encryption keys](https://cloud.google.com/storage/docs/encryption/customer-supplied-keys)
- [Cloud Storage - Data encryption options](https://cloud.google.com/storage/docs/encryption)
- [Compliance - ISO/IEC 27018](https://cloud.google.com/security/compliance/iso-27018)
- [Sensitive Data Protection Overview](https://cloud.google.com/security/compliance/iso-27018)
- [Automating the classification of data uploaded to Cloud Storage](https://cloud.google.com/sensitive-data-protection/docs/automating-classification-of-data-uploaded-to-cloud-storage)
- [Sensitive Data Protection client libraries](https://cloud.google.com/sensitive-data-protection/docs/libraries)
- [Sensitive Data Protection Demo](https://cloud.google.com/dlp/demo/#!/)
- [Compliance resource center](https://cloud.google.com/compliance?hl=en)
- [Health & Life Sciences Blog - Getting to know the Google Cloud Healthcare API: Part 1](https://cloud.google.com/blog/topics/healthcare-life-sciences/getting-to-know-the-google-cloud-healthcare-api-part-1)
- [Sharing and Collaboration](https://cloud.google.com/storage/docs/collaboration#top_of_page)
- [GCP HIPAA overview guide](https://cloud.google.com/files/gcp-hipaa-overview-guide.pdf)
- [PCI DSS Compliance in GCP - Cloud Storage](https://cloud.google.com/architecture/pci-dss-compliance-in-gcp#cloud_storage)
## Related Ideas: [[]]

