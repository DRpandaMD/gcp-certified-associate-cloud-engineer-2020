# Networking in GCP

## Routing Overview

* About Software Defined Networking

* More general than the OSI 7 Layer Model

* Not about any particular routing scheme

* Sets the stage for routing tables and routes

* Routing here is about the *data flow*

### Helpful Links

* [OSI Model of Networking - Webopedia](https://www.webopedia.com/quick_ref/OSI_Layers.asp)

* [Routing - Wikipedia](https://en.wikipedia.org/wiki/Routing)

## Routing - To Google's Networking (Premium Routing Tier)

### Links

* [Premium Routing Tier Blog Post](https://cloud.google.com/blog/products/gcp/introducing-network-service-tiers-your-cloud-network-your-way)

* [Hot potato / cold potato routing](https://en.wikipedia.org/wiki/Hot-potato_and_cold-potato_routing)

### Getting data to Google's Network

* Take a look at this gif to get an idea:

![Google Network](/Networking/images/google_network.gif)

## Routing - To the Right Resource

* [GCP Cloud Load Balancing Overview](https://cloud.google.com/load-balancing/docs/load-balancing-overview)

* Latency Reduction -- solved with **Cross Region Load Balancing** with Global Anycast IPs

  * Use servers physically close to client

* Load Balancing -- solved by using **Cloud Load Balancer**

  * separate from auto-scaling

* System Design -- Solved by using **HTTP(S) Load Balancer** (with URL Map)

  * Different servers may handle different parts of the system

  * Especially when using microservices (instead of a monolith)

### Unicast vs Anycast

* Unicast: there is only one **uni**que device in the world that can handle this; send it there

* Anycast: there are multiple devices that could handle this; send it to **any** one; but ideally the closest

### Layer 4 vs Layer 7

* TCP is usually called Layer 4
  * it works solely with IP addresses

* HTTP and HTTPS works at layer 7
  * these know about URLs and paths

* Each layer is built on the one below it

* Therefore:
  * To route based on URL paths routing needs to understand Layer 7
  * Layer 4 cannot rout based on the URL paths defined in Layer 7

### So what about DNS?

* Name resolution with DNS can be the first step in routing

* But, that comes with a number of problems:

  * Layer 4! -- Cannot route L4 based on L7 URL Paths

  * Chunky -- DNS queries often cached and reused for huge client sets

  * sticky -- DNS lookups "lock on" and refreshing per request has a high cost

    * Extra latency because each request includes another round-trip!

    * More money for additional DNS request processing
  
  * Not robust -- relies on the client always doing the right thing

    * spoiler alert they don't!

  * Premium tier "cold potato" routing with global anycast IPs avoid these problems.

## Routing -- Among Resources (VPC)

### Helpful Links Part 2

* [AcloudGuru -- Primer on Subnets and CIDRs](https://acloud.guru/series/acg-fundamentals/view/62f923ef-8f30-2f51-8681-5ab5de29b45d)

* [Classless inter-domain routing CIDR Blocks on Wikipedia](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing)

* [Private Network on Wikipedia](https://en.wikipedia.org/wiki/Private_network)

### Getting data from one resource another

* VPC (global) is a Virtual Private Cloud -- Your private SDN space in GCP

  * Not just resource to resource -- also manges the doors to outside & peers

* subnets (regional) create logical spaces to contain resources 

  * all subnets can reach all others -- globally without any need for VPNs

* Routes (global) define "next hop" for traffic based on destination IP

  * routes are global and apply by Instance level tags, not by subnet

  * no route to the  internet gateway means no such data can flow

* firewall rules (global) further filter data flow that would otherwise route

  * all firewall rule are global and apply by Instance-level tags or service account

  * default firewall rules are restrictive inbound and permissive outbound

## VPC - Automode Lab

* [subnet ranges](https://cloud.google.com/vpc/docs/vpc#subnet-ranges)

## VPC - Custom Mode Lab

### Part 1

* [VPC Documentation](https://cloud.google.com/vpc/docs/vpc)

### Part 2

* [Understanding Iam Custom Roles](https://cloud.google.com/iam/docs/understanding-custom-roles)

* [Creating and Managing Custom Roles](https://cloud.google.com/iam/docs/creating-custom-roles)

* [Service Accounts Overview](https://cloud.google.com/compute/docs/access/service-accounts)

* [Creating and enabling service accounts](https://cloud.google.com/compute/docs/access/create-enable-service-accounts-for-instances)

### Part 3

* [Firewall Rules Overview](https://cloud.google.com/vpc/docs/firewalls)

* [Configuring Network Tags](https://cloud.google.com/vpc/docs/add-remove-network-tags)

* [Filtering by Service Account vs. Network Tag](https://cloud.google.com/vpc/docs/firewalls#service-accounts-vs-tags)

* [Updating manged Instance Groups (e.g. Rolling update)](https://cloud.google.com/compute/docs/instance-groups/rolling-out-updates-to-managed-instance-groups)

* [acloudguru: Thead for editing instance in the web console](https://acloud.guru/forums/gcp-certified-associate-cloud-engineer/discussion/-LX_K01iaNGvgD6ICp_p/cannot_edit_instance_in_group)

Add tag to VM via `gcloud`

```bash
gcloud compute instances add-tags frontend-instance-group-knf1 --zone=us-west1-c --tags=open-ssh-tag
```

### Challenge Lab

* A Lab Challenge built on the previous step

#### Desired Result -- SETUP

* Two-tier setup: frontend and back, each auto scaled across 2+ zones

* Use ICMP (ping) to represent allowed traffic

* Frontend:

  * accepts incoming traffic from internet

  * can connect outbound to backend and internet

* Backend:

  * only accepts incoming from frontend or other backend

  * no outbound expect other backend

#### Desire Result -- Validation

* From Cloud shell or your computer:

  * can ping frontend instances

  * cannot ping backend instances

* when SSHed to a frontend instances

  * can ping the backend

  * can ping google.com

* When SSHed to a backend instance

  * cannot ping the frontend

  * cannot ping google.com

  * can ping other backend instances

#### My Solution

* Start with 2 sets of managed instance groups like in the first lab

* create a `open-ssh` firewall rule with `500` priority and `0.0.0.0/0`

* **THIS WILL NOT WORK AS SHOWN IN THE VIDEO**

* delete the firewall rule

* open the gcloud terminal 

* set your gcloud config  : `gcloud config set project <project-id>`

* **I Will come back to this at a later date to finish**

## Networking Exam Tips

* Practice CIDR Blocks

  * /16, /24, /28, etc

  * use <https://cidr.xyz/>

  * CIDR /16 is the same as 255.255.0.0

  * CIDR /24 is the same as 255.255.255.0

  * CIDR /32 is the same as 255.255.255.255

* Practice / Learn common ports

  * **HTTP == 80**

  * **HTTPS == 443**

  * **SSH == 22**

  * ICMP == NO PORT

  * RDP == 3389

  * SQL == 1443

  * MySQL == 3306

  * Postgres == 5432

### Subnet CIDR Ranges

* In GCP you *can* edit a subnet to increase its CIDR range

* No need to recreate subnet or instances

* New range must contain old range (i.e. old range must be a subset)

### Shared VPC

* [Shared VPC](https://cloud.google.com/vpc/docs/shared-vpc)

* In an Organization, you can share VPCs among Multiple projects

  * **Host project:** One project owns the shared VPC

  * **Service project:** other projects granted Access to use all/part of Shared VPC

* Lets multiple projects coexist on same local network (private IP space)

* This would let a centralized team manage network security
