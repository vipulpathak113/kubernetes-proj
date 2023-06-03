# Kubernetes Introduction

1. **Why do we need containers?**

   So that all services we need should be in isolated environments and it can be shipped and installed with the same config as developed.

2. **What are containers?**

   Containers are **completely isolated** environments.They have their own processes, own network interfaces and their own mount like VM. But they share the **same OS kernel**.

3. **What is container orchestration?**

   Process of **deploying and managing containers** is called container orchestartion.
   It monitors if container is up/down and also help in automatically scale up/down based on the load.

4. **Advantage of container orchestration?**

- Application is highly available as hardware failure will _not bring down the application_ as there are **multiple instances of application running on different nodes**.
- User traffic is load balances across various containers.
- When demand increases, deploy more instances of applications within seconds.
- Also can be done at service level when run out of hardware resources and scale the underlying nodes up/down without taking down the application.
- All these can be done with the help of set of declerative config file which is know as **kubernetes**.

1. **What is kubernetes?**

   It is an orchestration technology used to orchestrate deployment and management of hundred or thousands of container in clustered environment.

2. **What are nodes?**

   It is a machine, physical or virtual on which kubernetes is installed. It is a worker machine where containers will be launched by kubernetes.

3. **What are clusters?**

   It is a set of nodes grouped together.This way if one node fails your application will be still accessible from other nodes. Having multiple nodes helps in sharing the load as well.

4. **What are Master Node?**

   It is another node with kubernetes installed and is configured as Master.
   The master watches over the nodes in cluster and is responsible for actual orchesteration of containers on the worker nodes.

5. **What components we get after installing kubernetes on the system?**

   An API Server, etcd service, a kubelet service, a Container Runtime, Controllers and Schedulers.

6. **What is an API Server?**

   It acts as the frontend for kubernetes. The users, management devices, command line interfaces all talk to API server to interact with kubernetes cluster.

7. **What is an etcd key store?**

   It is a distrbuted reliable key value store by Kubernetes to store all data used to manage the cluster. When you have multiple nodes and multiple Masters in your cluster, etcd stores all that information is a distributed manner.
   It is also responsible for implementing locks within cluster to ensure that there are no conflicts between the masters.

8. **What are schedulers?**

   It is responsible for distributing work or containers. It looks for newly created containers and assign them to nodes.

9. **What are controllers?**

   They are brain behind orchesteration. The are reponsible for noticing and responding when nodes,container or end points goes down. It makes decisions to bring up new containers in such cases.

10. **What is Container Runtime?**

    They are underlying software used to run containers. Ex. Docker.

11. **Whate is kubelet?**

    It is an agent that runs on each node in the cluster. It is responsible for making sure containers are running on the nodes as expected.

12. **Whate is kubectl?**

    It is a command line tool which is used to deploy and manage applications on a kubernetes cluster. To get the cluster information, to get the status of other nodes in the cluster.

    kubectl run command is used to deploy an application on the cluster.

    `kubectl run hello-minikube `

13. **Steps to setup Kubernetes:**

    - Install kubectl
    - Intall minikube and start it

14. **What are pods?**

    A Pod is the smallest deployable unit in Kubernetes, representing a single instance of an application.

    Containers are not directly deloyed on the worker node by kubernetes. It is encapsulated with an object call pods. Pods is the smallest object in the kubernetes.

    Each pod gets an internal IP of its own within kubernetes cluster

15. **What should we do when more resources are added?**

    - [ ] Create a new container instance within same pod
    - [x] Create a new pod with new container instance of the same application
          <br/><br>

      **Pods usually have one to one relationship with containers running your application.**

    We can create multiple container in a single pod if both are of different kind.(Example helper container)

    For scaling purpose we should always create new pod with new instance of container of same application.

16. **Command to create pod using kubectl :**

    `kubectl run nginx --image=nginx `

    This command will create a new pod with name nginx using docker image named nginx(from docker hub)

17. **What is a Deployment in Kubernetes?**

    A Deployment in Kubernetes is a higher-level abstraction that manages the deployment of multiple Pods. It ensures that a specified number of replica Pods are running at any given time and allows for rolling updates and rollbacks. Deployments provide a declarative way to manage the state of applications and ensure consistency across environments.

18. **What is a Service in Kubernetes?**

    Services enable communication between different parts of an application and provide load balancing and service discovery. They ensure that Pods are discoverable and accessible from other parts of the application, even if they are running on different nodes or have dynamic IP addresses.

19. **What is a Kubernetes namespace?**

    It provides a way to partition and isolates resources within a cluster, allowing multiple teams or applications to share the same physical infrastructure. Namespaces provide a way to organize and manage resources based on their logical grouping and enable role-based access control and resource quotas.

20. **What is a Kubernetes controller?**

    A Kubernetes controller is a core component of Kubernetes that manages the state of a cluster. It monitors resources in the cluster and ensures that the desired state is maintained, reconciling any discrepancies that arise. Controllers provide a declarative way to manage resources and ensure consistency across the cluster. Examples of controllers include Deployments, ReplicaSets, StatefulSets, and Jobs.

21. **What is a StatefulSet in Kubernetes?**

    It ensures that each instance has a stable and unique hostname, persistent storage, and ordered deployment and scaling. StatefulSets provide a way to manage stateful applications in a declarative and consistent manner, enabling applications to be scaled up or down dynamically.

22. **What is a ConfigMap in Kubernetes?**

    It provides a way to store key-value pairs, files, or command-line arguments that your application needs to run. ConfigMaps are typically used to store configuration data that is likely to change, such as database connection strings or environment variables. They enable you to manage configuration data separately from the application code, making it easier to update and maintain.

23. **What is a Secret in Kubernetes?**

    It provides a secure way to store and distribute sensitive data to your application without exposing it to other parts of the system. Secrets are typically used to store credentials, TLS certificates, or other sensitive information that your application needs to function. They are encrypted at rest and can be mounted as files or environment variables in your application containers.

24. **What is the difference between a DaemonSet and a Deployment in Kubernetes?**

    A DaemonSet in Kubernetes ensures that a Pod is running on all nodes in a cluster, while a Deployment manages the deployment of multiple Pods and ensures a specified number of replica Pods are running at any given time.

    ***

**PODS with YAML:**

_It has 4 root level mandatory properties:_

- **apiVersion** > Version of Kubernetes API using to create the objects. Ex: v1,apps/v1
- **kind** > Refers type of object. Ex: Pod,Service, ReplicaSet, Deployment
- **metadata** > Data about the objects. Ex: name,labels. Metadata does not accept any key-value pair, it should be some specific values
- **spec** > Additional information regarding object to be created

Example for pod YAML file:

```yml
// test.yml

apiVersion: v1
kind: Pod
metadata:
   name: myapp-pod
   labels:
      app: myapp
      type: front-end
spec:
 containers:
   - name: nginx-container
     image: nginx

```

- To create pod using yaml file we use command:

  `kubectl apply -f test.yml `

- To get information about pods:

  `kubectl get pods`

- To get information of specific pod:

  `kubectl describe pod myapp-pod `

---

**REPLICATION CONTROLLER AND REPLICA SET**

**Replication Controller:** It helps in running muliple instances of a single pod in kubernetes cluster, _thus providing high availibilty_. It make sure that that number of pods always exists.

- It also helps in creating multiple pods to share the load across them.

- If no. of users increases then we will deploy additional pod to balance the load across the two pods.
- If further demand increases and we run out of resources on the first node we could deploy additional ports on other nodes in the cluster.

**Replica Set:**

- Replicaset is interlinked with image version, if image version is changed then new replicaset will be created and old will be not deleted but its pod will be deleted
- **Only 1 replicaset will be active per deploymen**t
- ReplicaSet manages pods , if one pods goes down then it will create new pods
