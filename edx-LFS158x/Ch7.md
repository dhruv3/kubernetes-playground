# Ch7- Accessing Minikube
## Accessing Minikube: Command Line Interface (CLI)
* kubectl is the Kubernetes Command Line Interface (CLI) client to manage cluster resources and applications. 
* It can be used standalone, or part of scripts and automation tools. 
* Once all required credentials and cluster access points have been configured for kubectl it can be used remotely from 
anywhere to access a cluster. 

## Accessing Minikube: Web-based User Interface (Web UI)

## Accessing Minikube: APIs
* We can directly connect to the API server using its API endpoints and send commands to it, as long as we can access the 
master node and have the right credentials.
* HTTP API space of Kubernetes can be divided into three independent groups:
  * Core Group (/api/v1): This group includes objects such as Pods, Services, nodes, namespaces, configmaps, secrets, etc.
  * Named Group: This group includes objects in /apis/$NAME/$VERSION format.
  * System-wide: This group consists of system-wide API endpoints, like /healthz, /logs, /metrics, /ui, etc.

## kubectl Configuration File
* To access the Kubernetes cluster, the kubectl client needs the master node endpoint and appropriate credentials to be 
able to interact with the API server running on the master node.
* The configuration file(present in '.kube' directory of user's home) has all the connection details required by kubectl. 
* By default, the kubectl binary parses this file to find the master node's connection endpoint, along with credentials.
* Kubernetes cluster installed by Minikube the `~/.kube/config` file gets created automatically.
