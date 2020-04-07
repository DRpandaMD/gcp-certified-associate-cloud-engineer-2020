# What is Security 

### Helpful Links

* [Information Security - Wikipedia](https://en.wikipedia.org/wiki/Information_security)

* [Google Search: "Public Bucket Breach](https://www.google.com/search?q=public+bucket+breach)

* [Security by Design](https://wiki.owasp.org/index.php/Security_by_Design_Principles)

* [OWASP Top 10 (2017)](https://www.owasp.org/images/7/72/OWASP_Top_10-2017_%28en%29.pdf.pdf)



## Definition


Information security, sometimes shortened to InfoSec, is the practice of preventing unauthorized access, use, disclosure, disruption, modification, inspection, recording or destruction of information....  Its primary focus is the balanced protection of the confidentiality, integrity and availability of data (also know=n as the CIA triad) while maintaining a focus on efficient policy implementation, all without hampering organization productivity. 

-- Wikipedia

* Proper Data Flow

    * You cannot view data you shouldn't

    * You cannot change data you shouldn't

    * You *can* access data you *should*


* Controlling Data Flow

    * Authentication - who are you?

    * Authorization - what are you allowed to do?

    * Accounting - What did you do ?

    * (Resiliency) - Make sure the system keeps running


#### What enables security in GCP?

* Security Products 

* Security Features

* Security Mindset

    * Includes Availability Mindset

#### Principles of Key Security Mindset

* Least privilege

* defense in depth (layer)

* Fail Securely 



#### Key Security Products / Features in GCP -- Authentication 

* Identity

    * Humans in G Suite, Cloud Identity

    * Applications and services use Service Accounts

* Identity hierarchy

    * Google Groups

* Can use Google Cloud Directory Sync (GCDS) to pull from LDAP



#### Key Security Products / Features in GCP -- Authorization

*  Identity hierarchy -- Google Groups

* Resource hierarchy (Organization , Folders, Projects 

* Identity and Access Management (IAM)

    * Permissions 
    
    * Roles

    * Bindings

* GSC ACLS

* Billing Management

* Network structure and restrictions 


#### Key Security Products / Features in GCP -- Accounting 

* Audit / Activity Logs (provided by Stackdriver)

* Billing export

    * Billing Export 

    * BigQuery

    * To file as CSV or JSON in a GCS Bucket

* GCS Object Lifecycle Management 

    