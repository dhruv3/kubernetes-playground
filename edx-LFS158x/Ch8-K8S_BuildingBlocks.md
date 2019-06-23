# Kubernetes Object Model
<img width="1091" alt="Screen Shot 2019-06-23 at 9 58 37 AM" src="https://user-images.githubusercontent.com/13077629/59978011-9133b580-959d-11e9-84fa-c5e8d53a177c.png">

<img width="1096" alt="Screen Shot 2019-06-23 at 9 59 01 AM" src="https://user-images.githubusercontent.com/13077629/59978012-9133b580-959d-11e9-8152-2bbe89f8b2e8.png">

# Pods
A Pod is the smallest and simplest Kubernetes object. It is the unit of deployment in Kubernetes, which represents a 
single instance of the application. A Pod is a logical collection of one or more containers, which:
* Are scheduled together on the same host with the Pod
* Share the same network namespace
* Have access to mount the same external storage (volumes).

<img width="1113" alt="Screen Shot 2019-06-23 at 10 05 02 AM" src="https://user-images.githubusercontent.com/13077629/59978193-73675000-959f-11e9-8256-c8688c1966c5.png">

# Labels
<img width="1098" alt="Screen Shot 2019-06-23 at 10 17 56 AM" src="https://user-images.githubusercontent.com/13077629/59978267-38195100-95a0-11e9-99d5-72775e98eebc.png">

# Label Selectors
* Controllers use Label Selectors to select a subset of objects. Kubernetes supports two types of Selectors:
  * Equality-Based Selectors: **=, ==** (equals, used interchangeably), or **!=** (not equals) operators. For example, with `env==dev` or env=dev.
  * Set-Based Selectors: **in, notin** operators for Label values, and exist/does not exist operator for Label keys. For example, with `env in (dev,qa)` we are selecting objects where the env Label is set to either dev or qa; with `!app` we select objects with no Label key app.

# ReplicaSets
* With the help of the ReplicaSet, we can scale the number of Pods running a specific container application image. 
* Scaling can be accomplished manually or through the use of an autoscaler.
* Deployments are the recommended controllers for the orchestration of Pods. Deployments manage the creation, deletion, and updates of Pods. 
* A Deployment automatically creates a ReplicaSet, which then creates a Pod. There is no need to manage ReplicaSets and Pods separately, the Deployment will manage them on our behalf.

# Deployment
<img width="1079" alt="Screen Shot 2019-06-23 at 10 36 59 AM" src="https://user-images.githubusercontent.com/13077629/59978536-dc9c9280-95a2-11e9-9b7b-76b91fd325c6.png">

<img width="1113" alt="Screen Shot 2019-06-23 at 10 49 41 AM" src="https://user-images.githubusercontent.com/13077629/59978695-a5c77c00-95a4-11e9-9c7d-d31d435da191.png">

# Namespaces
<img width="1092" alt="Screen Shot 2019-06-23 at 10 57 38 AM" src="https://user-images.githubusercontent.com/13077629/59978770-bd533480-95a5-11e9-9db2-a8196672b0bc.png">
