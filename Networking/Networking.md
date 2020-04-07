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

## Routing -- Among Resources (VPC)

### Helpful Links

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

  * all firewall ruels are global and apply by Instance-level tags or service account

  * default firewall rules are restrictive inbound and permissive outbound

## VPC - Automode lab

* [subnet ranges](https://cloud.google.com/vpc/docs/vpc#subnet-ranges)