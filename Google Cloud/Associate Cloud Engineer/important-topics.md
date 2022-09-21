# Topics
> Below are the most important topics to learn about in preparation for the exam. All of these topics have questions on the exam in one form or another

## Table of Contents
* [Resources Used for Preparation](#resources-used-for-preparation)
* [Most Import Topics to Know](#most-important-topics-to-know)
  * [Kubernetes](#kubernetes)
  * [Compute Engine](#compute-engine)
  * [App Engine](#app-engine)
  * [Cloud Storage](#cloud-storage)
  * [Databases](#databases)
  * [Virtual Private Cloud (VPC)](#virtual-private-cloud-vpc)
  * [Cloud Logging](#cloud-logging)
  * [Cloud Monitoring](#cloud-monitoring)
  * [Cloud IAM](#cloud-iam)
  * [Cloud Billing](#cloud-billing)


## Resources Used for Preparation

- [Google Cloud - Cloud Engineer Learning Path](https://cloud.google.com/training/cloud-infrastructure/#cloud-engineer-learning-path)
- [Udemy Practice Tests](https://www.udemy.com/course/google-certified-associate-cloud-engineer-practice-exams-gcp/)
- [Medium Article](https://medium.com/google-developer-experts/yes-you-can-pass-the-google-cloud-associate-engineer-exam-e4468a7bcf7d)

---

## Most Important Topics to Know

*Note: I grabbed this list from [Tutorials Dojo](https://tutorialsdojo.com/gcp-associate-cloud-engineer-exam-study-guide/). There’s more information about the exam available on the linked page.*

### Kubernetes

- **Features**
    - Can be configured to automatically scale node pool and clusters across multiple node pools based on changing workload requirements.
    - Auto-repair can be enabled to do health checks on node.
    - Can enable Cloud Logging and Cloud Monitoring via simple checkbox configurations.
    - Kubernetes version can be enabled to auto-upgrade with the latest release patch.
    - Supports Docker container format.
    - Integrates with Google Container Registry so you can easily access your private Docker images.
- **kubectl**
    - The main CLI tool for running commands and managing Kubernetes clusters
- **Cluster**
    - All of the Kubernetes objects that represent your containerized applications run on top of a cluster.
- **Node**
    - Nodes are the worker machines that run your containerized applications and other workloads.
    - A cluster typically has one or more *nodes.*
    - Kubernetes runs your workload by placing containers into pods to run on nodes.
- **Node Pool**
    - A node pool is a set of nodes within a cluster that have similar configurations.
- **Cluster Autoscaler**
    - Cluster Autoscaler automatically resizes the number of nodes in a given node pool, based on the demands of your workloads.
- **Kubernetes API Objects**
    - Pods
        - Are the smallest deployable units of computing that you can create and manage in Kubernetes.
        - Every pod has its own IP address.
    - Deployment
        - You described the desired state in a *deployment*, and the Deployment Controller changes the actual state to the desired state at a controlled rate.
    - Service
        - Serves as a load balancer to balance traffic across a set of pods.
        - You are allowed to specify which type of service you would like to use:
            - ClusterIP: exposes the service on a cluster-internalIP.
            - NodePort: exposes the service on each node’s IP at a static port (the NodePort)
            - Load Balancer: exposes the service externally using a cloud provider’s load balancer.
- **Workload Resources**
    - [ReplicaSet](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)
        - A ReplicaSet’s purpose is to maintain a stable set of replica pods running at any given time. As such, it is often used to guarantee the availability of a specified number of identical pods
    - [StatefulSets](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)
        - A StatefulSet is the workload API object used to manage stateful applications.
        - Manages the deployment and scaling of a set of pods, *and provides guarantees about the ordering and uniqueness of these pods.*
        - Like a deployment, a StatefulSet manages pods that are based on an identical container spec.
        - Unlike a deployment, a StatefulSet maintains a sticky identity for each of their pods. These pods are created from the same spec, but are not interchangeable: each has a persistent identifier that it maintains across any rescheduling.
    - [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)
        - A DaemonSet ensures that all (or some) nodes run a copy of a pod. As nodes are added to the cluster, pods are added to them. As nodes are removed from the cluster, those pods are garbage collected. Deleting a DaemonSet will clean up the pods it created.
    - ConfigMaps
        - ConfigMaps enable you to separate your configurations from your pods and components, which helps keep your workloads portable.
- **GKE Sandbox**
    - Provides a second layer of security between containerized workloads on GKE.
    - GKE Sandbox uses gVisor.
    - You cannot enable GKE Sandbox on a default node pool.
    - When using Sandbox, you must have at least 2 node pools.
    - It’s not possible to use accelerations such as GPUs or TPUs.

---

### Compute Engine

- **Instance Groups**
    - An instance group is a set of virtual machine instances that you can collectively manage as a single entity.
        - Managed Instance Groups
            - Lets you operate apps on multiple identical VMs.
            - MIG is scalable and highly available.
            - It supports autoscaling, auto-healing, regional deployment, and automatic updating.
            - MIG can be set to perform auto-healing to keep your instances running at all times.
                - Activating this triggers health check to determine the status of instances and will try to recreate them when an instance is unhealthy.
- **Preemptible Instances**
    - A preemptible VM is an instance that you can provision at a much lower price point than normal instances.
    - Compute Engine might stop preemptible instances at any time due to system events.
    - This is perfect for fault-tolerant applications that can withstand possible instance preemption.
- Sole-tenant Nodes
    - A physical Compute Engine server dedicated exclusively for your use.

---

### App Engine

- **Standard and Flexible environment**
    - Standard
        - Based on container instances running on Google’s infrastructure.
    - Flexible
        - Enables you to manage the underlying compute infrastructure.
- **Scaling**
    - Basic
        - Creates instances when your application receives requests.
        - Each instance will be shut down when the application becomes idle.
    - Automatic Scaling
        - Creates instance based on request rate, response latencies, or application metrics that you specify.
    - Manual Scaling
        - Allows you to manually specify the number of instances that continuously run regardless of the load level.
- Deploying an App Engine service with CLI.

---

### Cloud Storage

- [https://cloud.google.com/storage/docs/storage-classes](https://cloud.google.com/storage/docs/storage-classes)
- **Bucket Configurations**
    - Life Cycle Management
        - You can define conditions that trigger data deletion, or transition to a cheaper storage class with object class with object life cycle management.
    - Versioning
        - Continue to store old copies of objects you store when they are deleted or overwritten.
    - Retention Policies
        - Define minimum retention periods that objects must be stored.
    - Object Holds
        - Place an object on hold to prevent deletion
    - Encryption Keys
        - Customer-managed
        - Customer-supplied
    - Access Permissions
        - Access Control list
        - Uniform bucket level access
        - Object and Bucket Level Permissions
- **Storage Classes:**
- **[Uploading Objects to Google Cloud Storage](https://cloud.google.com/storage/docs/uploads-downloads)**
    - Simple Upload
        - Utilize this if the file is small enough to upload again if the connection fails, and if there is **no** object metadata to send as part of the upload request.
    - Multipart Upload
        - Utilize this if the file is small enough to upload again if the connection fails, and you **need** to include object metadata as part of the upload request.
    - Resumable Upload
        - Utilize this for a more reliable transfer, which is especially important with large files.
    - [Parallel Composite Upload](https://cloud.google.com/storage/docs/parallel-composite-uploads)
        - Utilize if network and disk speed are not limiting factors. When doing parallel composite upload, a file is divided into up to 32 chunks and uploaded in parallel to temporary objects. The final object is recreated using the temporary objects, and the temporary objects are deleted.
    - Alternatively, for uploading large volumes of data (from hundreds of terabytes up to 1 petabyte), you can utilize **Transfer Appliance**. It is a hardware appliance you can use to securely migrate to Google Cloud Platform without disrupting business operations.

---

### Databases

- [https://cloud.google.com/blog/topics/developers-practitioners/your-google-cloud-database-options-explained](https://cloud.google.com/blog/topics/developers-practitioners/your-google-cloud-database-options-explained)
- **Relational**
    - Cloud SQL
        - Managed MySQL, PostgreSQL, SQL Server.
        - Good for general purpose SQL database.
        - Point-in-time recovery (PITR) uses binary logs.
    - Cloud Spanner
        - Cloud-native with large scale, consistency, horizontal scaling.
        - Good for RDBMS+ scale, HA, HTAP.
    - Bare Metal
        - Lift and shift Oracle workloads to Google Cloud.
- **Non-Relational (NoSQL)**
    - Firestore
        - Cloud native, serverless, NoSQL document database, backend-as-a-service.
        - Good for large scale, complex hierarchical data.
    - Cloud BigTable
        - Cloud native NoSQL wide-column store for large scale, low-latency workloads.
        - Good for heavy read + write events.
- **In Memory**
    - Memory Store
        - Fully managed Redis and Memcached for sub-millisecond data access.
        - Good for in-memory and key-value store.

---

### Virtual Private Cloud (VPC)

- [**Shared VPC**](https://cloud.google.com/vpc/docs/shared-vpc)
    - Allows an organization to connection resources from multiple projects to a common VPC network, so that they can communicate with other securely and effciently using internal IPs from that network.
- **[VPC Network Peering](https://cloud.google.com/vpc/docs/vpc-peering)**
    - Allows connectivity between two VPC networks regardless if they are in different projects or organizations.
- **[Load Balancers](https://cloud.google.com/load-balancing/docs/choosing-load-balancer)**
    - A load balancer distributes users traffic across multiple instances of your applications. By spreading the load, load balacing reduces the risk that your applications experience performance issues.
- **Cloud VPN vs. Cloud Interconnect**
    - Cloud Interconnect offers [low-latency and high availability to transfer data between on-premise and VPC networks](https://cloud.google.com/network-connectivity/docs/interconnect/concepts/overview).
        - *Dedicated Interconnect* provides a direct physical connection between your on-premises network and Google's network.
        - *Partner Interconnect* provides connectivity between your on-premises and VPC networks through a supported service provider.
    - Consider using Cloud VPN if you [don’t require low-latency and high availability](https://cloud.google.com/network-connectivity/docs/interconnect/concepts/overview#cloud-vpn-considerations) to set up IPSec VPN tunnels between your networks. IPSec VPN tunnels encrypts data.
        - A Cloud VPN tunnel doesn't require the overhead or costs associated with a direct, private connection. Cloud VPN only requires a VPN device in your on-premises network.

---

### Cloud Logging

- **Features**
    - Write any custom log, from any source, into Cloud Logging using the public write APIs.
    - Integrates with Cloud Monitoring to set alerts on the logs events and logs-based metrics you have defined.
    - You can export data in real-time to BigQuery to perform advanced analytics and SQL-like query tasks.
    - Cloud Logging helps you see the problems with your data using Error Reporting. It helps you automatically analyze your logs for exceptions and intelligently aggregate them into meaningful error groups.
- **Cloud Audit Logs**
    - Admin Activity admin logs
        - Contains log entries for API calls or other administrative actions that modify the configuration or metadata or resources.
        - You must have the IAM role logging/logs.viewer or project/viewer to view these logs.
        - Admin Activity logs are always written and you can’t configure or disable them in any way.
    - Data Access audit logs
        - Contains API calls that read the configuration or metadata of resources, including user-driven API calls that create, modify, or read user-provided resource data.
        - You must have logging/private.logs.viewer or project/owner to view these logs.
        - You must explicitly enable Data Access audit logs to be written. They are disabled by default because they are large.
    - System Event audit logs
        - Contains log entries for administrative actions taken by Google Cloud that modify the configuration of resources.
        - You must have the IAM role logging/logs.viewer or project/viewer to view these logs.
        - System Event audit logs are always written so you can’t configure or disable them.
        - There is no additional charge for your System Event audit logs.
    - Exporting Audit Logs
        - Log entries received by Logging can be exported to Cloud Storage buckets, BigQuery datasets. and Pub/Sub topics.
        - To export audit log entries outside of logging:
            - Create a logs sink.
            - Give the sink a query that specifies the audit log types you want to export.
        - If you want to export audit log entries for a Google Cloud organization, folder, or billing account, review Aggregated sinks.

### Cloud Monitoring

- **Workspaces**
    - A Workspace can manage the monitoring of data for a single Google Cloud project, or it can manage the data for multiple Google Cloud projects and AWS accounts.
        - A Google Cloud project or an AWS account can only be associated with one Workspace at a time.
    - You must have the following IAM role name for the Google Cloud project to create a Workspace:
        - Monitoring Editor
        - Monitoring Admin
        - Project Owner
- **Cloud Monitoring Agent**
    - The Cloud Monitoring agent is a `collectd` based daemon that collects application and system metrics from virtual machine instances.
    - The Monitoring agent collects disk, network, CPU, and process metrics by default.
    - You can configure the Monitoring agent to monitor third-party applications.

---

### Cloud IAM

- **Features**
    - Lets you authorize who can take specific actions on resources to give you full control and visibility on your Google Cloud services centrally.
    - Permissions are represented in the forms of *service.resource.verb.*
- **Roles**
    - A role contains a set of permissions that allows you to perform specific actions on Google Cloud resources.
    - You don’t directly grant users permissions in IAM. Instead, you grant them roles, which bundle one or more permissions.
    - Types of roles:
        - Basic roles
            - Owner, Editor, and Viewer.
        - Predefined Roles
            - Provides granular access for a specific service and is managed and defined by Google Cloud.
        - Custom Roles
            - Provides granular access according to a user-defined list of permissions.
            - You can create a custom IAM role with one or more permissions and then grant that custom role to users or groups.
- **Service Accounts**
    - Used by an application or a virtual machine instance, not a person.
    - Applications use service accounts to make authorized API calls.
    - A service account is associated with two sets of public/private RSA key pairs used to authenticate to Google.
    - Types of service accounts
        - User-managed service accounts
        - Default service accounts
            - Google creates a user-managed service account when you use Google Cloud services. These accounts are called default service accounts.
            - In addition to being an identity, **a service account is also a resource** with IAM policies attached to it, which means you can define who can use the account and who can perform specific actions on the service account.
- **Best** **Practices**
    - Enforce least privilege at all times.
    - Mirror your Google Cloud resource hierarchy structure to your organization structure.
    - Set policies at the organization level and at the project level rather than at the resource level.
    - It’s easier and better to manage members in a Google group than to update an IAM policy.
    - Rotate your service account keys using the IAM service account API.
    - For production workloads, it’s best practice to user user-managed service accounts instead of the default service accounts.
---

### Cloud Billing

- **Cloud Billing Account**
    - Access control to Cloud Billing account is established by IAM roles.
- **Google Payments Profile**
    - Stores information about who is responsible for the profile
    - Serves as a document center where you can view invoices and payment history.
- **Cloud Billing Reports**
    - The Cloud Billing Reports page allows you to view your Google Cloud usage costs at a glance and discover and analyze trends.
    - You can also forecast future costs using the Cloud Billing Reports to check out how much you are projected to spend, up to 12 months in the future.
- **Cloud Billing Budgets**
    - You can define the scope of the budget to apply:
        - Entire Cloud Billing account.
        - One or more projects.
        - One or more products.
        - Other budget filters applicable to your Cloud Billing account.
    - You can specify the budget amount to your requirement, or base the budget amount on the previous month’s spend.
    - Moreover, you can also specify email alerts and declare the recipients in the following ways:
        - Using the role-based option, where you can send email alerts to billing admins and users on the Cloud Billing account.
        - Using Cloud Monitoring, where you can enlist other people in your organization to receive budget alert emails.
        - You can also use Pub/Sub for a more programmatic notification approach.
- **Overview of Cloud Billing Roles in IAM**
    - Billing Account Creator (roles/billing.creator)
        - Create new self-service billing accounts.
        - Assigned at the organization level.
        - Use this role for initial billing setup or to allow the creation of additional billings. Users must have this role to sign up for Google Cloud with a credit card using their corporate identity.
    - Billing Account Administrator (roles/billing.admin)
        - Manage billing accounts (but not create them).
        - Can be assigned at the organization level or billing account.
        - This role is an owner role for a billing account. Use it to manage payment instruments, configure billing exports, view cost information, link and unlink projects, and manage other user riles on the billing account.
    - Billing Account User (roles/billing.user)
        - Link projects to billing accounts.
        - Can be assigned at the organization level or billing account.
        - This role has very restricted permissions, so you can grant it broadly, typically in combination with Project Creator. These two roles allow a user to create new projects linked to the billing account on which the role is granted.
    - Billing Account Viewer
        - View billing account cost information and transactions.
        - Can be assigned at the organization level or billing account.
        - Billing Account Viewer access would usually be granted to finance teams. It provides access to spend information but does not confer the right to link or unlink projects or otherwise manage the properties of the billing account.
    - Project Billing Manager (roles/billing.projectManager)
        - Link/unlink the project to/from a billing account.
        - Can be assigned at the organization level or billing account.
        - This role allows a user to attach the project to the billing account, but does not grant any rights over resources. Project Owners can use this role to allow someone else to manage the billing for the project without granting them resource access.
