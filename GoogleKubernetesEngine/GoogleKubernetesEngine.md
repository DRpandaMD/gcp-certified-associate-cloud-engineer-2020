# Google Kubernetes Engine

* [Kubernetes Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)

## Helpful links

* [GKE Overview](https://cloud.google.com/kubernetes-engine/docs/concepts/kubernetes-engine-overview)

* [GKE Concepts](https://cloud.google.com/kubernetes-engine/docs/concepts/)

* [Cluster Architecture](https://cloud.google.com/kubernetes-engine/docs/concepts/cluster-architecture)

* [Pods](https://cloud.google.com/kubernetes-engine/docs/concepts/pod)

* [Deployments](https://cloud.google.com/kubernetes-engine/docs/concepts/deployment)

* [StatefulSets](https://cloud.google.com/kubernetes-engine/docs/concepts/statefulset)

* [DaemonSets](https://cloud.google.com/kubernetes-engine/docs/concepts/daemonset)

* [Services and Service Types](https://cloud.google.com/kubernetes-engine/docs/concepts/service)

* [HTTP(s) load balancing with Ingress](https://cloud.google.com/kubernetes-engine/docs/concepts/ingress)

* [GKE Storage](https://cloud.google.com/kubernetes-engine/docs/concepts/storage-overview)

## Introduction

* Learn Kubernetes

## Course Outline

* K8s Big Picture

* K8s App Architecture

* K8s Networking

* K8s Storage

* From code to K8s

* K8s deployments

* scaling K8s Apps

* RBAC and Admision Control

* Other Kubernetes stuff

## Kubernetes Big Picture

### A Kubernetes Primer

* Cloud Native Apps!  [Cloud Native on Wikipedia](https://en.wikipedia.org/wiki/Cloud_native_computing)

### The Kubernetes API

* Everything in K8s is defined here (resources)

* REST

* CRUD

* HTTP Methods (GET POST etc)

* use `kubectl` to post `yaml` to the api server

* Update desired state and current state matches desired state

* API is broken up into parts

  * SIGs look after the API

### Kubernetes Objects

* containers are wrapped up in a **Pod**!

  * Contains one or more containers

  * smallest unit deployable in K8s

  * Atomic unit of scheduling  

  * Object on the cluster

* **Deploy**

  * Object on the cluster

  * defined in **apps/v1** API group

  * scaling

  * rolling updates

### Getting a cluster

* I will be using GCP!

* Just go in to GCP

  * Click on GKE and make a cluster

## App Architecture

### Theory

* Kubernetes objects can spin up cloud resources

* code is wrapped in containers which is wrapped in *deployments*

* Deployment is an object kin Kubernetes

* secrets is an object

* all of this can be managed through the Kubernetes API server

### Sample App

* I forked this from nigelpoulton <https://github.com/DRpandaMD/k8s-sample-apps>

## Kubernetes Networking

### Common Networking Requirements

* big scalable networks

* service discovery! 

* highly dynamic networks are the new normal

* endpoints added and removed from network based on active scaling up and down

  * also covers failure, rolling updates, etc etc.

### Networking in the Sample App

* Take a look at the `k8s-sample-apps/mysql-wordpress-pd/wordpress-deployment.yaml`

* they are in a declarative format. which is great for K8s and Documentation.


### Kubernetes Networking Basics

* All nodes can talk

* All Pods can talk without NAT

* every pod gets its own IP

### Kubernetes Service Fundamentals

* enter Stable network abstraction 

* every service gets a name and IP -- they are stable

* services are auto registered in coreDNS

* use labels for pod traffic routing 

* end point object maps ips from pods and labels


### Service Types

* Cluster Ip is the default:

  * gets own IP

  * own accessible from within the cluster

* NodePort:

  * Gets cluster wide **PORT**

  * Accessible from outside the cluster

* LoadBalancer

  * integrates with public cloud platform (AWS, Azure GCP)


### The Service Network

* Separate from:

    * Node network

    * Pod network

* "kube-proxy"

* IPTABLES Mode:

  * Default since K8s 1.2

  * Doesn't Scale well

  * not really designed for Load Balancing

* IPVS Mode

  * Stable (GA) since Kubernetes 1.11

  * Uses Linux kernel IP Virtual Server

  * native layer-4 load balancer

  * supports more algorithms (than just RoundRobin)

### Networking Demo

* I forked the class lesson here <https://github.com/DRpandaMD/Course_Kubernetes_Deep_Dive_NP/tree/master/lesson-networking>


* `kubectl get nodes` used to list nodes in the cluster

* `kubectl apply -f ./ping-deploy.yml` creates a deployment based on the .yml

* `kubectl get deploy` gets the deployment object here its just pingtest

* `kubectl get pods -o wide` shows the wide landscape of how the pods are set against the nodes

* `kubectl get nodes -o jsonpath='{.items[*].spec.podCIDR}'` shows another output of just the CIDR blocks the nodes are sitting on.

* `kubectl exec -it pingtest-6bcdfcdc5b-8t6zg bash` just like docker this will connect into said pod with bash (these pods will change)

* `