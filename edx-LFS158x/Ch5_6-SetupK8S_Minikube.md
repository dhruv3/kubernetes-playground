# Chapter 5: K8S Setup
## Kubernetes Configuration
4 types of installations:
* All-in-One Single-Node Installation
* Single-Node etcd, Single-Master and Multi-Worker Installation
* Single-Node etcd, Multi-Master and Multi-Worker Installation
* Multi-Node etcd, Multi-Master and Multi-Worker Installation

## Localhost Installation
Options available:
* Minikube - single-node local Kubernetes cluster
* Docker Desktop - single-node local Kubernetes cluster for Windows and Mac
* CDK on LXD - multi-node local cluster with LXD containers.

# Chapter 6: Minikube
## Prerequisites for Minikube
* In order to fully take advantage of all the features Minikube has to offer, a Type-2 Hypervisor should be installed on the local workstation, to run in conjunction with Minikube. 
* This does not mean that we need to create any VMs with guest operating systems with this Hypervisor.
* Minikube builds all its infrastructure as long as the Type-2 Hypervisor is installed on our workstation.
* Minikube invokes the Hypervisor to create a single VM which then hosts a single-node Kubernetes cluster.

## Installing Minikube
1. Install kubectl
```bash
brew install kubernetes-cli
kubectl version
```
2. Install a [Hypervisor](https://www.virtualbox.org/wiki/Downloads)
3. Install minikube
```bash
brew cask install minikube

# test installation
minikube start
# check status
minikube status
# stop minikube
minikube stop
```

