# Kubernetes Big Picture

## A Kubernetes Primer

* Cloud Native Apps!  [Cloud Native on Wikipedia](https://en.wikipedia.org/wiki/Cloud_native_computing)

## The Kubernetes API

* Everything in K8s is defined here (resources)

* REST

* CRUD

* HTTP Methods (GET POST etc)

* use `kubectl` to post `yaml` to the api server

* Update desired state and current state matches desired state

* API is broken up into parts

  * SIGs look after the API



## Kubernetes Objects 

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

## Getting a cluster

* I will be using GCP!

* Just go in to GCP

 * Click on GKE and make a cluster
 