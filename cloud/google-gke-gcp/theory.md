# Theory

## <mark style="color:yellow;">Kubernetes</mark>

<mark style="color:red;">**Kubernetes**</mark>**&#x20;is an orchestration framework for software containers. Kubernetes provides the tools you need to run containerized applications in production and at scale.&#x20;**<mark style="color:red;">**Google Kubernetes Engine (GKE)**</mark>**&#x20;is a managed service for Kubernetes.**

## <mark style="color:yellow;">Cloud Computing</mark>

Principles of Cloud Computing:

* Customers get computing resources that are on-demand and self-service
* Customers get access to those resources over the internet, from anywhere.
* The provider of those resources allocates them to users out of that pool
* Resources are elastic - which means they're flexible, so customers can be
* Customers pay only for what they use, or reserve as they go

## <mark style="color:yellow;">GKE Structure</mark>

<figure><img src="../../.gitbook/assets/gke-architecture.png" alt=""><figcaption></figcaption></figure>

1. <mark style="color:yellow;">**Cluster**</mark>: A Kubernetes cluster is a set of nodes (machines) that run containerized applications managed by Kubernetes. It includes a control plane and nodes.
2. <mark style="color:yellow;">**Pod**</mark>: The smallest and simplest Kubernetes object. A pod represents a single instance of a running process in a cluster and can contain one or more containers.
3. <mark style="color:yellow;">**Node**</mark>: A machine (virtual or physical) in a Kubernetes cluster that runs pods. Nodes are managed by the control plane.
4. <mark style="color:yellow;">**Control Plane**</mark>: The collection of processes that manage the Kubernetes cluster. This includes the API server, scheduler, controller manager, and etcd database. It is responsible for maintaining the desired state of the cluster.
5. <mark style="color:yellow;">**kubelet**</mark>: An agent that runs on each node in the cluster. It ensures containers are running in a pod by communicating with the control plane.
6. <mark style="color:yellow;">**kubectl**</mark>: A command-line tool for interacting with the Kubernetes API server. It allows you to deploy and manage applications on a Kubernetes cluster.

#### Google Computing Services List

<mark style="color:yellow;">**Compute Engine**</mark>**,&#x20;**<mark style="color:yellow;">**GKE**</mark>**,&#x20;**<mark style="color:yellow;">**App Engine**</mark>**,&#x20;**<mark style="color:yellow;">**Cloud Functions**</mark>**, and&#x20;**<mark style="color:yellow;">**Cloud Run**</mark>

## <mark style="color:yellow;">Batch Job</mark>

In the simplest terms, a **batch job** is a scheduled program that is assigned to run on a computer without further user interaction. Batch jobs are often queued up during working hours, then executed during the **evening** or **weekend** when the computer is idle

## <mark style="color:yellow;">Service Accounts</mark>

Service accounts are identities that are intended for use by applications instead of people. In GKE, you interact with _**Kubernetes service accounts**_ and with _**Identity and Access Management service accounts**_.

### <mark style="color:yellow;">Account Impersonation</mark>

**GKE Service Account Impersonation** allows one Google Cloud service account to act on behalf of another service account. This is useful for granting temporary permissions and enhancing security.
