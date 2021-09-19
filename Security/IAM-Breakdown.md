# Identity and Access Management (IAM) Breakdown

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

### Members and Groups

* [IAM Overview Docs - Members and Groups](https://cloud.google.com/iam/docs/overview)

#### Members

* A member is some Google-Known identity

* Each member is identified by a unique email address

* Can be:
  * user: Specific Google Account:  `{G Suit, Cloud Identity, Gmail or validated email}`
  * `serviceAccount`: Service account for apps/services
  * `group` : Google group of users and service accounts
  * `domain`: whole domain managed by GSuite or Cloud Identity
  * `allAuthenticatedUsers --  *ANY* Google account or service account

#### Groups

* " A Google Group is a named collection of google accounts and service accounts".

* "Every group has unique email address that is associated with the group."

* You can never act *as* the group
  * But membership in a group can grant capabilities to individuals

* Use them for everything!

* Can be used for owner when within an organization

* *Can* nest groups in an organization
  * Example: one group for each department, all those in group for all staff

### IAM Breakdown - Policies

* [IAM Overview Docs - Policies](https://cloud.google.com/iam/docs/overview)

* [Granting, Changing and Revoking Access to Resources](https://cloud.google.com/iam/docs/granting-changing-revoking-access)

* ["gcloud add-iam-policy-binding"](https://www.google.com/search?q=gcloud+add-iam-policy-binding+site%3Acloud.google.com)

#### Policies

* A Policy binds Members to Roles for some scope of Resources

* Answers: Who can do what to which things?

* Attached to some level in the Resource Hierarchy
  * Organization, Folder, Project, Resource

* Roles and Members listed in policy, but Resource identified by attachment

* Always additive ("Allow") and never subtractive (no "Deny")
  * "Child policies cannot restrict access granted at a higher level

* Use groups!

##### Managing Policy Bindings

* Can use `get-iam-policy`, edit the JSON/YAML file, and `set-iam-policy` back

* But you should use:

* `gcloud [GROUP] add-iam-policy-binding [RESOURCE-NAME] --role [ROLE-ID-TO-GRANT] --member user: [USER-EMAIL]`

* `gcloud [GROUP] remove-iam-policy-binding [RESOURCE-NAME] --role [ROLE-ID-TO-REVOKE] --member user: [USER-EMAIL]`

* Atomic operations are better because changes:

  * are simpler, less work, and less error-prone (than editing the yaml or json)

  * *Avoids race conditions, so changes cna happen simultaneously*

  * Example `gcloud beta compute instances add-iam-policy-binding myhappyvm --role roles/compute.instanceAdmin -- member user:me@example.com`

### IAM Breakdown -- Wrap Up

* [IAM Overview Documentation](https://cloud.google.com/iam/docs/overview)

* [IAM FAQ](https://cloud.google.com/iam/docs/faq)

* [IAM Best Practices](https://cloud.google.com/iam/docs/using-iam-securely)
