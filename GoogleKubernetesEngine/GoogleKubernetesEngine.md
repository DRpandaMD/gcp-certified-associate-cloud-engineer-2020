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