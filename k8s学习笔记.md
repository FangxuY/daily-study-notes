# k8s学习笔记

***



Docker是应用最为广泛的容器技术，通过打包镜像，启动容器来创建一个服务。但是随着应用越来越复杂，容器的数量也越来越多，由此衍生了管理运维容器的重大问题，而且随着云计算的发展，云端最大的挑战，容器在漂移。

从架构设计层面，我们关注的可用性，伸缩性都可以结合k8s得到很好的解决，如果你想使用微服务架构，搭配k8s，真的是完美，再从部署运维层面，服务部署，服务监控，应用扩容和故障处理，k8s都提供了很好的解决方案。

具体来说，主要包括以下几点：

1. 服务发现与调度
2. 负载均衡
3. 服务自愈
4. 服务弹性扩容
5. 横向扩容
6. 存储卷挂载

## k8s集群的组成

![preview](https://pic2.zhimg.com/v2-499cc023903440be0fee5cf63b689c89_r.jpg)

k8s集群由Master节点和Node节点组成

### **Master节点**

Master节点指的是集群控制节点，管理和控制整个集群，基本上k8s的所有控制命令都发给它，它负责具体的执行过程。在Master上主要运行着：

1. Kubernetes Controller Manager（kube-controller-manager）：k8s中所有资源对象的自动化控制中心，维护管理集群的状态，比如故障检测，自动扩展，滚动更新等。
2. Kubernetes Scheduler（kube-scheduler）： 负责资源调度，按照预定的调度策略将Pod调度到相应的机器上。
3. etcd：保存整个集群的状态。

### **Node节点**

除了master以外的节点被称为Node或者Worker节点，可以在master中使用命令 `kubectl get nodes`查看集群中的node节点。每个Node都会被Master分配一些工作负载（Docker容器），当某个Node宕机时，该节点上的工作负载就会被Master自动转移到其它节点上。在Node上主要运行着：

1. kubelet：负责Pod对应的容器的创建、启停等任务，同时与Master密切协作，实现集群管理的基本功能
2. kube-proxy：实现service的通信与负载均衡
3. docker（Docker Engine）：Docker引擎，负责本机的容器创建和管理
