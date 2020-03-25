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

* 