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

- `kubectl version` 

```
Client Version: version.Info{Major:"1", Minor:"22", GitVersion:"v1.22.3", GitCommit:"c92036820499fedefec0f847e2054d824aea6cd1", GitTreeState:"clean", BuildDate:"2021-10-27T18:41:28Z", GoVersion:"go1.16.9", Compiler:"gc", Platform:"linux/amd64"}
Server Version: version.Info{Major:"1", Minor:"22", GitVersion:"v1.22.3", GitCommit:"c92036820499fedefec0f847e2054d824aea6cd1", GitTreeState:"clean", BuildDate:"2021-10-27T18:35:25Z", GoVersion:"go1.16.9", Compiler:"gc", Platform:"linux/amd64"}
```

- `kubectl get nodes`

```
NAME       STATUS   ROLES                  AGE   VERSION
minikube   Ready    control-plane,master   27h   v1.22.3
```

- `kubectl get services`

```
NAME             TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)          AGE
hello-minikube   NodePort    10.98.36.71   <none>        8080:31278/TCP   24h
kubernetes       ClusterIP   10.96.0.1     <none>        443/TCP          27h
```

![image-20220109225948867](/home/hjw/.config/Typora/typora-user-images/image-20220109225948867.png)

- `kubectl create deployment nginx-depl --image=nginx`

根据镜像创建deployment

- `kubectl get deployment`

获取deployment

- `kubectl get pod`

获取pod

- `kubectl get replicaset`

<span style=color:red>Replicaset is managing the replicas of Pod</span>

- `kubectl edit deployment nginx-depl`

修改deployment信息，如修改部署服务所用镜像版本信息

- `kubectl get replicaset`

获取副本

```
NAME                        DESIRED   CURRENT   READY   AGE
hello-minikube-6ddfcc9757   1         1         0       24h
nginx-depl-5c8bf76b5b       0         0         0       22m
nginx-depl-7fc44fc5d4       1         1         1       4m51s   
# 由于kubectl edit deployment nginx-depl，修改了镜像版本，所以老容器停止，用新容器nginx-depl-7fc44fc5d4 
```



<span style=color:red>**Debuging Pod**</span>

- `kubectl logs [pod name]`
- `kubectl describe pod [pod name]` 获取pod工作状态信息



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





### MiniKube安装

[官方安装教程](https://minikube.sigs.k8s.io/docs/start/)

问题记录：`[ERROR ImagePull]: failed to pull image k8s.gcr.io/kube-apiserver:v1.22.2: output: Error response from daemon: Get https://k8s.gcr.io/v2/: net/http: request canceled while waiting for connection (Client.Timeout exceeded while awaiting headers)`

解决方法：`minikube start`，修改为：`minikube start --image-mirror-country='cn' --image-repository='registry.cn-hangzhou.aliyuncs.com/google_containers'`

