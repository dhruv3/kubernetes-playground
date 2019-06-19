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
* The role of the **kube-scheduler** is to assign new objects, such as pods, to nodes.
* The scheduler obtains from etcd, via the API server, resource usage data for each worker node in the cluster.
* The scheduler also receives from the API server the new object's requirements which are part of its configuration data.

### Controller Managers
* Controllers are watch-loops continuously running and comparing the cluster's desired state with its current state.
* The **kube-controller-manager** runs controllers responsible to act when nodes become unavailable, to ensure pod counts are as expected, to create endpoints, service accounts, and API access tokens.
* The **cloud-controller-manager** runs controllers responsible to interact with the underlying infrastructure of a cloud provider when nodes become unavailable, to manage storage volumes when provided by a cloud service, and to manage load balancing and routing.

### etcd
* **etcd** is used to persist a Kubernetes cluster's state. New data is written to the data store only by appending to it, data is never replaced in the data store.
* Only the API server is able to communicate with the etcd data store.
* etcd is based on the Raft Consensus Algorithm which allows a collection of machines to work as a coherent group that can survive the failures of some of its members. 
* At any given time, one of the nodes in the group will be the master, and the rest of them will be the followers. Any node can be treated as a master.

# Worker Node
<img width="449" alt="Worker_Node" src="https://user-images.githubusercontent.com/13077629/59797121-95fa2000-92a4-11e9-876c-87f1d4406fe3.png">

* A worker node provides a running environment for client applications.
* A Pod is the smallest scheduling unit in Kubernetes. It is a logical collection of one or more containers scheduled together.
* Pods are scheduled on worker nodes, where they find required resources to run.

## Worker Node Components
A worker node has the following components:
* Container runtime
* kubelet
* kube-proxy
* Addons for DNS, Dashboard, cluster-level monitoring and logging.

### Container Runtime
* K8S does not have the capability to directly handle containers.
* In order to run and manage a container's lifecycle, Kubernetes requires a **container runtime** on the node where a Pod and its containers are to be scheduled.
* Example of container runtimes:
  * Docker- although a container platform which uses containerd as a container runtime, it is the most widely used container runtime with Kubernetes.
  * containerd - a simple and portable container runtime providing robustness.
  * rkt - a pod-native container engine, it also runs Docker images
  * rktlet - a Kubernetes Container Runtime Interface (CRI) implementation using rkt.

### kubelet
* The kubelet is an agent running on each node and communicates with the control plane components from the master node. 
* It interacts with the container runtime on the node to run containers associated with the Pod.
* The kubelet connects to the container runtime using Container Runtime Interface (CRI).

![CRI](https://user-images.githubusercontent.com/13077629/59799129-584bc600-92a9-11e9-9b72-e85b8fed3c83.png)

* The kubelet acting as grpc client connects to the CRI shim acting as grpc server to perform container and image operations. CRI implements two services: ImageService and RuntimeService. 

### kubelet - kube-proxy
* The kube-proxy is the network agent which runs on each node responsible for dynamic updates and maintenance of all networking rules on the node. 
* It abstracts the details of Pods networking and forwards connection requests to Pods.

# Networking Challenges
Kubernetes as a containerized microservices orchestrator it needs to address 4 distinct networking challenges:
* Container-to-container communication inside Pods
* Pod-to-Pod communication on the same node and across cluster nodes
* Pod-to-Service communication within the same namespace and across cluster namespaces
* External-to-Service communication for clients to access applications in a cluster.

## Container-to-Container Communication Inside Pods
* Making use of the underlying host operating system's kernel features, a container runtime creates an isolated network space for each container it starts. 
* On Linux, that isolated network space is referred to as a network namespace. A network namespace is shared across containers, or with the host operating system.
* When a Pod is started, a network namespace is created inside the Pod, and all containers running inside the Pod will share that network namespace so that they can talk to each other via localhost.

## Pod-to-Pod Communication Across Nodes
* The Kubernetes network model aims to reduce communication complexity, and it treats Pods as VMs on a network, where each VM receives an IP address - thus each Pod receiving an IP address. 
* This model is called "IP-per-Pod" and ensures Pod-to-Pod communication, just as VMs are able to communicate with each other.
* Containers are integrated with the overall Kubernetes networking model through the use of the Container Network Interface (CNI) supported by CNI plugins. 

## Pod-to-External World Communication
* Kubernetes enables external accessibility through services, complex constructs which encapsulate networking rules definitions on cluster nodes. 
* By exposing services to the external world with kube-proxy, applications become accessible from outside the cluster over a virtual IP.
