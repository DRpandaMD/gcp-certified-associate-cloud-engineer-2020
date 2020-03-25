# Identity and Access Management (IAM ) Breakdown


## Resource Hierarchy

* Resource 

    * Something you create in GCP

* Project

    * Container for a set of related resources

* Folder

    * Contains an number of Projects and Subfolders


* Organization

    * Tied to G Suite or Cloud Identity domain.

### Docs

* [Resource hierarchy for access control](https://cloud.google.com/iam/docs/resource-hierarchy-access-control)

* [G Cloud IAM Overview](https://cloud.google.com/iam/docs/resource-hierarchy-access-control)



## IAM Breakdown -- Permissions & Roles

### Helpful Links

* [IAM Overview](https://cloud.google.com/iam/docs/overview)

* [Understanding Roles](https://cloud.google.com/iam/docs/understanding-roles)

* [Understanding IAM custom roles](https://cloud.google.com/iam/docs/understanding-custom-roles)

* [Predefined Roles](https://cloud.google.com/iam/docs/understanding-roles#predefined_roles)

### Permissions 

* A permission allows you to perform  certain action

* Each one follow the form `Service.Resource.Verb`

* Usually correspond to REST API methods

* Examples:

    * `pubsub.subscriptions.consume`

    * `pubsub.topics.publish`


### Roles

* A role is a collection of Permissions to use or manage GCP Resources

* Primitive Roles - Project-level and often too broad

    * viewer is read-only

    * editor can view and change things

    * owner can also control access & billing

* Predefined Roles -  Give granular access to specific GCP resources

    * E.g.: `roles/bigquery.dataEditor, roles/pubsub.subscriber`

    * For the exam read through the list of roles for each product!  --Think about why each exists

* Custom Role - Project or Org-Level Collections you define of granular permissions

#### App Engine - Predefined Role Example


| Role Name | Role Title | Description |
| ---- | ----- | ---- |
| roles/ appengine.AppAdmin | App  Engine Admin | Read/Write/Modify access to all application configuration and settings. |
| roles/ appengine.serviceAdmin | App Engine Service Admin | Read-only access to all application configuration and settings.  Write access to module-level and version-level settings. Cannot deploy a new version. |
| roles/ appengine.deployer | App Engine Deployer | Read-only access to all application configuration and settings.  Write access only to create a new version; cannot modify existing versions other than deleting versions that are not receiving traffic|
| roles/ appengine.appViewer | App Engine Viewer | Read-only access to all application configurations and settings. |
| roles/ appengine.codeViewer | App Engine Code Viewer | Read-only access to all configuration settings, and deployed source code |