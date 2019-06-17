# Kubernetes Architecture
At a very high level, Kubernetes has the following main components:
* One or more master nodes
* One or more worker nodes
* Distributed key-value store, such as etcd.

# Master Node
<img width="494" alt="Master_Node1" src="https://user-images.githubusercontent.com/13077629/59637147-bb5b2280-911a-11e9-8534-278182899326.png">
* The master node provides a running environment for the control plane responsible for managing the state of a Kubernetes cluster.
* To ensure the control plane's fault tolerance, master node replicas are added to the cluster.
* The control plane components stay in sync across the master node replicas.
* To persist the Kubernetes cluster's state, all cluster configuration data is saved to **etcd**(distributed key-value store).

## Master Node Components
A master node has the following components:
* API server
* Scheduler
* Controller managers
* etcd.

### API Server
* All the administrative tasks are coordinated by the **kube-apiserver**, a central control plane component running on the master node. 
* The API server intercepts RESTful calls from users, operators and external agents, then validates and processes them. 
* During processing the API server reads the Kubernetes cluster's current state from the etcd, and after a call's execution, the resulting state of the Kubernetes cluster is saved in the distributed key-value data store for persistence.

### Scheduler
* 
