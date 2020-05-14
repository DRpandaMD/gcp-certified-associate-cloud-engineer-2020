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

* run `apt-get install iputils-ping curl dnsutils iproute2 -y` to install some utilities that the base container image does not come with and will needed to run some tests

  * you will have to run `apt-get update` FIRST!!

* inside the pod you can `ping` the other pods it will work

* exit the pod

* `kubectl apply -f ./simple-web.yml` deploys the new service

* `kubectl get svc` will list the service 

* jump back into the pod you had the ip tests 

  * if you don't remember (Like I did) just install the tools again on the new pod

* `curl hello-svc:8080` which is the format of `<SERVICE_NAME: Pod_Port>` 

  * this will dump out the HTML text of the pod

* `curl <Any_Node_IP>:30001` which is the format of `<NODE_IP: NODE_PORT>`

  * This will ALSO dump out the html text of the pod

* Now to set up the public load balancer 

* `kubectl apply --f lb.yml` to deploy the new lb service

* `kubectl get svc --watch` to watch the lb-svc and get an external IP

* copy and paste the external IP and put it into a browser and the web page should render

  * "Hello Cloud Gurus"

## Kubernetes Storage

### Kubernetes Storage Big Picture

* Kubernetes Volumes abstract the data from the pods -- decoupling storage from Pods

* File and Block are First Class citizens in Kubernetes 

  * Standards based

  * pluggable backend

  * Rich API 

* What are your storage requirements

  * Speed?

  * Replication?

  * Resiliency 

  * ...etc

* This all gets handled by the storage backend

* Containers Storage Interface puts the storage into the hands of the Persistent Volume Subsystem.

  * Persistent Volume (PV) -- storage

  * Persistent Volume Claim (PVC) -- ticket to use the PV

  * Storage Class (SC) -- makes it dynamic

### The Container Storage Interface (CSI)

* maintained at <https://github.com/container-storage-interface/spec>

* decouples storage from the main code base of K8s

### The kubernetes PersistentVolume Subsystem

* GCP Persistent Disks

  * Standard

  * SSD

* GCEPersistentDisk PlugIn

* to use a PV  needs to PV Claim  


### Dynamic Provisioning with StorageClasses

* using storage classes allow for the dynamic creation of PV and binding


### Storage Classes Demo

* code used <https://github.com/ACloudGuru-Resources/Course_Kubernetes_Deep_Dive_NP/blob/master/sample-app/mysql-wordpress-pd/mysql-deployment.yaml>

* it is important to note that by default Kubernetes (GKE) will make a `default` storage class 

* you can find it by `kubectl get sc`

  * It will list the storage class

* you will need a secret for the database

  * `kubectl create secret generic mysql-pass --from-literal=password=<PASSWORD>`

* run `kubectl apply -f ./mysql-deployment.yaml`

* use `kubectl describe pv` && `kubectl describe pvc` to get details about the Persistent Volume and the Persistent Volume Claim


* clean up by: 

  * `kubectl delete deployment <delpoyment_name>`

  * `kubectl delete pvc <pvc_name>`

  * `kubectl delete pv <pv_name>`

  * check the deployment, pods, pvc, and pv and it should all be cleaned up

## From Code to Kubernetes

* apps start with code

* put it into a container image

* put the image in to a registry

* then use kubernetes to create an object that kubernetes can uses

  * deployments!!

* *coding* then *docker* then *kubernetes*

### Demo

* Using this code <https://github.com/ACloudGuru-Resources/Course_Kubernetes_Deep_Dive_NP/tree/master/code-k8s> or the fork that I have provided

* examine the directory code and dockerfile 

* `docker image build -t drpandamd/node-app:0.1 .`

* `docker image push drpandamd/node-app:0.1`

* I went ahead and made some changes to his code and made it my own and deployed the deployment and the web-service

* for clean up you will want to make sure you kill the deployment and services made in kubernetes

## Kubernetes Deployments

* deployments wrap up your pods

* make your changes in the deployment post it against the API server then stick it back into git

* with replicas set to 3:

  * rolling updates :

    * maxSurge: 1  -- will have one extra pod than the desired state during the update

    * maxUnavailable: 0 -- will ensure we never go below 3 
  
  * This will roll out new pods with the new version and kill off the old pods one by one until all pods in the desired state of 3 have the new version.  -- This will keep your app up while rolling the update

* minReadySeconds: 300 will give 5 minutes between each new pod -- this helps give time to ensure the pods stand up 

### Deployment Demo

* `kubectl get nodes`

* `kubectl version -o yaml`

* `kubectl apply -f deploy.yml`

* `kubectl get deployment test --watch`

* `kubectl describe deployment test`

* `kubectl get rs` -- rs here means replica set

* `kubectl rollout history deployment test`

* `kubectl apply -f deploy.yml --record`

* `kubectl rollout undo deploy test`



## Scaling Applications Automatically 

* Increasing load (cpu memory / connections messages in the queue )

* increase in pods to trigger more nodes

* Horizontal Pod AutoScaler 

* Cluster AutoScaler


### Horizontal Pod AutoScaler 

* will scale pods automatically horizontally across nodes

### HPA Demo

* to match up what Nigel has, i set my cluster to autoscale min 3 nodes max 6 nodes

* `kubectl get pods --namespace acg-ns` to check the pods made


* to run the load generator

```bash
kubectl run -i --tty loader --image=busybox /bin/sh

while true; do wget -q -O- http://acg-lb.acg-ns.svc.cluster.local; done
```

* `kubectl get hpa --namespace acg-ns` to watch the HPA do its thing

* `kubectl get pods --namespace acg-ns` to list the pods out in the name space

* `kubectl get deploy --namespace acg-ns -o yaml` to see the yaml of the deployment and how the deployment was changed based on information provided by the HPA

* make sure to clean up after you are done


### Cluster Autoscaler 

* make sure you have your pods listed in the yaml with resource requests!

* dont mess with the pools via the CLI or Console

* check your specific cloud for support (luckily GCP is on top of it)

* test for performance on BIG clusters

## RBAC and Admission Control

* we want to control who access to the API server

  * actions are REST based

  * and CRUD (Create, Read, Update, Delete )

* via HTTPS 

* AuthN -- prove your ID

* AuthZ -- is the user allowed to perform action

* Addition Control -- Mutate and validation 

* Schema validation 

* RBAC 

  * Enabled since 1.6

  * GA since 1.8

  * Deny-by-default

### Authentication

* Kubernetes does not do users 

  * manage users externally 

* Service Accounts

  * do happen in Kubernetes

  * for system components

  * managed  by kubernetes

  * you should be using these and should manage them.

### Authorization

* Basically : **who** can perform which **actions** on which **resources**

  * can *sam* execute a *create* on a *deployment*

  * can *bob* execute a *delete* on a *pods*

* out of the box K8s has Default Users -- its how you been doing everything in the cluster as it stands

  * it is too powerful for production

* You will need to create some **Roles & RoleBindings** for least privilege 

* new roles and bindings are -- DENY ALL by default

  * so you will have to open up individual roles

* You can bind by *Role* or by *ClusterRole*

  * *role* is namespaced

  * *ClusterRole* is for the whole cluster

  * what you can do is create *ClusterRoles* then in the *RoleBinding* you can add namespaces to them.

  * That way you can make a few *ClusterRoles* but get granular in the *RoleBinding*

  * This prevents you from doing extra work with roles and assigning them


### Admission Control - not yet GA

* webhooks with external admissions controllers

* mutating 

* validating


### RBAC Demo

* [Github Code](https://github.com/ACloudGuru-Resources/Course_Kubernetes_Deep_Dive_NP/tree/master/lesson-rbac)

* he is using kops on AWS 

### RBAC Recap

Here is an overview I snipped from the mad lads over at acloudguru

![RBAC Overview](/GoogleKubernetesEngine/Images/RBAC_AdmissionControl_Overview.PNG)

## Other Kubernetes Stuff -- Stuff Nigel thinks is important

* DaemonSets - pod one runs every node

* StatefulSet - 

* Job - specified number of pods to complete a specific task

* CronJob - scheduled Job

* PodSecurityPolicy 

* Pod resource requests and limits

* ResourceQuotas - set limits against namespaces

* CustomResourceDefinition - adds some extensibility to Kubernetes 

## What is Next 

* The Kubernetes Book

* Docker Dive Book

* Community KubeCon

* the podctl podcast

* kubernetes podcast from google

* kubernetes certfied administrator

* serverless Knative and openfaas

* serverice meshes

* prometheus

* API 