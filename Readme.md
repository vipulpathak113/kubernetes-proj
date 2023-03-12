# Kubernetes Introduction

1. **Why do we need containers?**

    So that all services we need should be in isolated environments and it can be shipped and installed with the same config as developed.

2. **What are containers?**

    Containers are **completely isolated** environments.They have their own processes, own network interfaces and their own mount like VM. But they share the **same OS kernel**.

3. **What is container orchestration?**

    Process of **deploying and managing containers** is called container orchestartion.
    It monitors if container is up/down and also help in automatically scale up/down based on the load.

4. **Advantage of container orchestration?**
- Application is highly available as hardware failure will *not bring down the application* as there are **multiple instances of application running on different nodes**.
- User traffic is load balances across various containers.
- When demand increases, deploy more instances of applications within seconds.
- Also can be done at service level when run out of hardware resources and scale the underlying nodes up/down without taking down the application.
- All these can be done with the help of set of declerative config file which is know as **kubernetes**. 

5. **What is kubernetes?**

    It is an orchestration technology used to orchestrate deployment and management of hundred or thousands of container in clustered environment. 


6. **What are nodes?**

    It is a machine, physical or virtual on which kubernetes is installed. It is a worker machine where containers will be launched by kubernetes.

7. **What are clusters?**

    It is a set of nodes grouped together.This way if one node fails your application will be still accessible from other nodes. Having multiple nodes helps in sharing the load as well.

8. **What are Master Node?**

    It is another node with kubernetes installed and is configured as Master.
    The master watches over the nodes in cluster and is responsible for actual orchesteration of containers on the worker nodes.

9. **What components we get after installing kubernetes on the system?**

    An API Server, etcd service, a kubelet service, a Container Runtime, Controllers and Schedulers.

9. **What is an API Server?**

    It acts as the frontend for kubernetes. The users, management devices, command line interfaces all talk to API server to interact with kubernetes cluster.
    
9. **What is an etcd key store?**

    It is a distrbuted reliable key value store by Kubernetes to store all data used to manage the cluster.         
