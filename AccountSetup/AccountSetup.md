# Account Set Up

I already have a paid account.  But the Free Trial Account from GCP is pretty sweet.  Links are below for more information.

* [GCP Free Trial](https://cloud.google.com/free/)

* [Free Trial Restrictions](https://cloud.google.com/free/docs/gcp-free-tier#always-free-usage-limits)

* [GCP Always Free](https://cloud.google.com/free/docs/gcp-free-tier#always-free)

* [GCP Cloud Free Tier](https://cloud.google.com/free/docs/gcp-free-tier)

## Setting up the Account

* You are going to want to create a separate email an google account to set up.
[Trial Account Link](https://console.cloud.google.com/billing/00DD1C-7E0429-3ABCBD)

* You can do this in the browser by using `Incognito Mode`

* Depending on how much data of yourself you have saved into your browser it will be a bit of pain.   Just make sure you add all you details properly

* Also set up some type of 2-Step or Two Factor Verification.

* It might sound weird but you want to ensure that you use least privilege while going about. [Least Privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege) 


## Exploring the GCP Console

* [Link to GCP Console](https://console.cloud.google.com/)

* [Link to Google Cloud Status Dashboard](https://status.cloud.google.com/)

## Setup Billing Export

`Tools for monitoring, analyzing and optimizing cost have become an important part of managing development.  Billing export to BigQuery enables you to export your daily usage and cost estimates automatically throughout the day to a BigQuery dataset you specify.  You can then access your billing data from BigQuery.` -- GCP Docs 

* [Export Cloud Billing data to BigQuery](https://cloud.google.com/billing/docs/how-to/export-data-bigquery)

* Export must be set up per billing account

* Resources should be placed into appropriate projects

* Resources should be tagged with lables

* Billing export is not in real-time

  * Delay is in hours.

## Set up a Billing Alert

* [GCP Docs on Budgets and Billing Alerts](https://cloud.google.com/billing/docs/how-to/budgets)

* To help you with project planning and controlling costs, you can set a budget. Setting a budget lets you track how your spend is growing toward that amount.

* You can apply a budget to either a billing account or a project, and you can set the budget at a specific amount or match it to the pervious month's spend.  You can also create alerts to notify billing administrators when spending exceeds a percentage of your budget.


## Setup Non-Admin User Access 

* [Billing Access Docs](https://cloud.google.com/billing/docs/how-to/billing-access)

* Billing IAM

  * Role: Billing Account User

  * Purpose: Link projects to billing accounts.

  * Level: Organization or Billing Account

  * Use Case: This role has very restricted permissions, so you can grant it broadly, typically in combination with Project Creator.  These two roles allow a user to create new project linked to the billing account on which the role is granted.

  * The point here is to tightly control the access of who manages the billing.

  * Remember to enable 2FA and multi-step auth whenever you are given the option for it.


## Explore Cloud Shell and Editor 

* [Cloud Shell Docs](https://cloud.google.com/shell/)

* [ACloudGuru GCP Cloud Engineer Repo](https://github.com/ACloudGuru/gcp-cloud-engineer)

### What is Google Cloud Shell

`Google Cloud Shell provides you with command-line access to your cloud resources directly from your browser.  You can easily manage your projects and resources without having to install the Google Cloud SDK or other tools on your system.  With Cloud Shell the Cloud SDK gcloud CLI and other utilities you need are always available, up to date and fully authenticated when you need them ` -- GCP Docs

### Highlights

* Web browser access

  * No need for local terminal 

  * Automatic SSH Key management

* 5GB of persistent storage

* Easy access to preinstalled tools like:

  * gcloud, bq, kubectl, docker, npm/node, pip/python, ruby, vim, emacs, bash

* Preauthorized and always up-to-date

* Web Preview of Web app running on local port


### Helpful Cloud Shell Commands

* `dl <filename>`

## Data Flows

### aCloudGuru Lecture Video Links

* [Mental Models](https://acloud.guru/course/aws-certification-preparation/learn/Learning-Effectively/Mental-Models/watch)

* [Mental Model Example](https://acloud.guru/course/aws-certification-preparation/learn/Learning-Effectively/Mental-Model-Example/watch)

* [Zooming In and Out](https://acloud.guru/course/aws-certification-preparation/learn/Learning-Effectively/Zooming-In-and-Out/watch)

IT is all about Data flows.  Try to link up in you mind, a mental model for how this data flows through the cloud system and how you move data in systems that you build on top of the cloud platform

|Cloud Service Type | Data Flow|
|-------------------|----------|
| Network | Moving |
| Compute | Processing |
| Storage | Remembering |

### Mental Models

* A simplified representation of reality, which is ....

* Used by your mind to anticipate events or draw conclusions

* Systems combine

  * Build larger systems out of smaller ones (using abstractions)

  * Zooming and out

## A look at Google Projects

* [GCP Projects](https://cloud.google.com/docs/overview/#projects)