![]()
![image.png](https://img.hacpai.com/file/2019/09/image-32973ad6.png)

下载链接：https://leif.fun/downloads/books/每天5分钟玩转Kubernetes.pdf

百度云：链接:[https://pan.baidu.com/s/1eUJzQVGFMXuMXM3SwGjcFw](https://pan.baidu.com/s/1eUJzQVGFMXuMXM3SwGjcFw) 密码:47bp
# 2019年09月24日
## 第1章 先把Kubernetes跑起来
### 1.2 创建kubernetes集群
查看集群信息

```
kubectl cluster-info
```
![image.png](https://img.hacpai.com/file/2019/09/image-eb97ebc7.png)

### 1.3 部署应用
Deployment:可以理解为**应用**
Pod:是容器的集合，通常会将紧密相关的一组容器放到一个pod中，同一个pod中的所有容器共享IP地址和Port空间，也就是说他们在一个network namespace中。
    是K8S调度的最小单位，同一个pod中的容器始终被一起调度。

查看当前pod
    
```
kubectl get pods
```
![image.png](https://img.hacpai.com/file/2019/09/image-f7d04b23.png)

### 1.4 访问应用
查看应用被映射到节点的哪个端口

```
kubectl get services
```
![image.png](https://img.hacpai.com/file/2019/09/image-205abe4c.png)

service：暂时理解为**端口映射**

### 1.5 scale应用
查看副本数

```
kubectl get deployments
```
![image.png](https://img.hacpai.com/file/2019/09/image-f7b2e880.png)

增加副本数（扩容）

```
kubectl scale deployments/kubernetes-bootcamp --replicas=3
```
![image.png](https://img.hacpai.com/file/2019/09/image-181d23cd.png)

通过`kubectl get pods` 可以看到当前Pod增加到了三个
![image.png](https://img.hacpai.com/file/2019/09/image-d90da8f0.png)

使用`curl`命令访问应用可以看到负载均衡的效果
![image.png](https://img.hacpai.com/file/2019/09/image-34f8ac97.png)

删除一个副本（缩容）

```
kubectl scale deployments/kubernetes-bootcamp --replicas=2
```
![image.png](https://img.hacpai.com/file/2019/09/image-1ec198d1.png)

### 1.6 滚动更新
将v1升级到v2

```
kubectl set image deployments/kubernetes-bootcamp kubernetes-bootcamp=jocatlin/kubernetes-bootcamp:v2
```
![image.png](https://img.hacpai.com/file/2019/09/image-843cd55e.png)

可以看出 v1的pod被诸葛删除，同时启用了新的v2 pod
![image.png](https://img.hacpai.com/file/2019/09/image-1a6e4b46.png)

将v2降级到v1

```
kubectl rollout undo deployments/kubernetes-bootcamp
```
![image.png](https://img.hacpai.com/file/2019/09/image-13ef59e6.png)

![image.png](https://img.hacpai.com/file/2019/09/image-ac81b2ee.png)


# 2019年09月25日
## 第2章 重要概念

1.Cluster: 是计算、存储和网络资源的集合

2.Master: 是Cluster的大脑，主要负责调度，可以运行多个Master来实现高可用

3.Node:职责是运行容器应用。Node由Master管理，Node负责监控并汇报容器的状态，同时根据Master的要求管理容器的生命周期。如果Cluster只有一个主机，那么它既是Master也是Node。

4.Pod:是K8S的最小工作单元。每个Pod包含一个或多个容器。Pod中的容器会作为一个整体被Master调度到一个Node上运行。

5.Controller:K8S通过Controller来管理Pod。Controller中定义了Pod的部署特性，比如有几个副本、在什么样的Node上运行等。K8S提供了多种Controller：

* Deployment：可以管理Pod的多个副本并确保Pod按照期望的状态运行

* ReplicaSet：实现了Pod的多副本管理。使用Deployment会自动创建ReplicaSet，Deployment通过ReplicaSet来管理Pod的多个副本，一般不直接使用ReplicaSet。

* DaemonSet：用于每隔Node最多只运行一个Pod副本的场景。DaemonSet通常用于运行daemon。

* StatefuleSet：能够保证Pod的每个副本在整个生命周期中是不变的，而其他Controller不提供这个功能。当某个Pod发生故障需要删除并重新启动时，Pod的名称会发生变化，同时StatefuleSet会保证副本按照固定顺序启动、更新或者删除。

* Job：用于运行结束就删除的应用，而其他Controller中的Pod通常是长期持续运行。

6.Service：K8S Service定义了外界访问一组特定Pod的方式。Service有自己的IP和端口，Service为Pod提供了负载均衡。K8S运行容器（Pod）与访问容器（Pod）这两个任分别由Controller和Service执行

7.Namespace：可以将物理的Cluster逻辑上划分成多个虚拟Cluster，每个Cluster就是一个Namespace、不同的Namespace里的资源是完全隔离的。K8S默认创建了两个Namespace。

![image.png](https://img.hacpai.com/file/2019/09/image-17bbc4d7.png)

* default：创建资源时如果不指定，将被放到这个Namespace中

* kube-system：K8S自己创建的系统资源将放到这个Namespace中。


