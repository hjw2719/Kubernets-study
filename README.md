# Kubernets-study

## Intro to K8s

### What is Kubernetes?

**Official definition of Kubernetes**

- Open source container orchestration tool
- Developed by Google
- Help you manage containerized applications in different deployment environments

**What problems does Kubernetes Solve ?**





**What are the tasks of an orchestration tool ?**





### K8s Architecture

- Api Server
- Scheduler
- Controller manager
- etcd

![image-20220103215001354](/home/hjw/.config/Typora/typora-user-images/image-20220103215001354.png)



#### node process

Worker machine in K8s cluster

1) each Node has multiple Pods on it
2) **3 processes (container runtime、kubelet、Kube proxy)**must be installed on every Node
3) Worker Nodes do the actual work

- Kubelet **interacts with both** -container and node

- Kubelet **starts the pod** with a container inside

3 process:

1. container runtime
2. Kubelet
3. Kube proxy, forwards the requests 







![image-20220105230615619](/home/hjw/.config/Typora/typora-user-images/image-20220105230615619.png)

**answer :	Managing processes are done by Master Nodes**



4 processes run on every master node!

1. **Api Server, 容器管理统一entry_point，具有最高权限**
   - cluster gateway
   - acts as a gatekeeper for authentication



![image-20220105231506726](/home/hjw/.config/Typora/typora-user-images/image-20220105231506726.png)

2. **Scheduler**

![image-20220105231754390](/home/hjw/.config/Typora/typora-user-images/image-20220105231754390.png)

3. **Controller manager**

![image-20220105232032710](/home/hjw/.config/Typora/typora-user-images/image-20220105232032710.png)

4. **etcd(Cluster brain), Key Value Store** 

for example, 

​        	- Is the cluster healthy

​             What resources are availiable ?

​             Did the cluster state change

​             这些问题都能在etcd存储数据找到答案

![image-20220105232758565](/home/hjw/.config/Typora/typora-user-images/image-20220105232758565.png)











### Main K8s Components

- Pod
- Service
- Ingress
- ConfigMap
- Secretes
- Volumes
- Deployment and Stateful Set

![image-20220103210258290](/home/hjw/.config/Typora/typora-user-images/image-20220103210258290.png)





**Pod and Ingress**

Ingress可以理解为给外界提供服务的入口，提供域名供公网访问。

![image-20220103210552406](/home/hjw/.config/Typora/typora-user-images/image-20220103210552406.png)



**ConfigMap and Secret**（不要将密钥放入ConfigMap，Secret中可放密钥）

ConfigMap 配置数据库url等参数，否则如果数据库名字变更，内网访问时需要先修改my-app里数据库url，接着重启DB容器，然后重启my-app容器，此时数据库改名才生效，如果使用ConfigMap，直接修改其内容中数据库url就可生效。

![image-20220103211232768](/home/hjw/.config/Typora/typora-user-images/image-20220103211232768.png)

![image-20220103211629012](/home/hjw/.config/Typora/typora-user-images/image-20220103211629012.png)

**Volumes**

![image-20220103212211126](/home/hjw/.config/Typora/typora-user-images/image-20220103212211126.png)

**Deployment and Stateful Set**

![image-20220103212609269](/home/hjw/.config/Typora/typora-user-images/image-20220103212609269.png)

Deployment and Stateful Set

DB are often hosted outside of K8s cluster

Stateful Set通常给数据库设置，因为数据库切换时需要数据同步

![image-20220103213227179](/home/hjw/.config/Typora/typora-user-images/image-20220103213227179.png)





### Minikube and Kubectl - Local Setup（实战）

- What is minikube ?
- what is kubectl ?
- Set-up Minikube cluster 



![image-20220106224605966](/home/hjw/.config/Typora/typora-user-images/image-20220106224605966.png)



![image-20220106230618356](/home/hjw/.config/Typora/typora-user-images/image-20220106230618356.png)







### Main Kubectl Commands - K8s CLI

### K8s YAML Configuration File

### Hands-On Demo







## Advanced Concepts

### K8s Namespaces - Organize your Components

### K8s Ingress 

### Helm - Package Manager

### Volumes - Persisting Data in K8s

### K8s StatefulSet - Deploying Stateful Apps

### K8s Serivces
