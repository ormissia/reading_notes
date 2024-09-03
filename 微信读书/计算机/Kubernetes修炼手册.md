---
doc_type: weread-highlights-reviews
bookId: "38153670"
reviewCount: 2
noteCount: 65
author: 奈吉尔·波尔顿
cover: https://cdn.weread.qq.com/weread/cover/5/YueWen_38153670/t7_YueWen_38153670.jpg
readingStatus: 读完
progress: 100%
totalReadDay: 2
readingTime: 1小时37分钟
readingDate: 2024-02-11
finishedDate: 2024-02-14
isbn: 9787115561091
category: 计算机 计算机综合
title: Kubernetes修炼手册
rating: 74%
readProgress: 100
readingTimestamp: 5842
lastReadTimestamp: 1707921403
tags: 读书笔记 计算机 计算机综合 读完
totalWords: 153396

---

# Kubernetes修炼手册

# 元数据
> [!abstract] Kubernetes修炼手册
> - ![ Kubernetes修炼手册|200](https://cdn.weread.qq.com/weread/cover/5/YueWen_38153670/t7_YueWen_38153670.jpg)
> - 书名： Kubernetes修炼手册
> - 作者： 奈吉尔·波尔顿
> - 简介： 本书是一本Kubernetes入门图书，共分为12章，涵盖了Kubernetes的基础知识，并附带了大量的配置案例。此外，还介绍了Kubernetes架构、构建Kubernetes集群、在Kubernetes上部署和管理应用程序、Kubernetes安全，以及云本地、微服务、容器化等术语的含义。本书在内容上不断进行充实和完善，可以帮助读者快速入门Kubernetes。本书适合系统管理员、开发人员，以及对Kubernetes感兴趣的初学者阅读。
> - 出版时间 2021-05-01 00:00:00
> - ISBN： 9787115561091
> - 分类： 计算机-计算机综合
> - 出版社： 人民邮电出版社



---


# 高亮划线


### 2.1 Kubernetes概览


> 📌 Deployment）提供可扩展性和滚动更新，DaemonSet在集群的每个工作节点中都运行相应服务的实例，有状态应用部署于StatefulSet，同时那些需要不定期运行的临时任务则由定时任务（CronJob）来管理。

---

### 2.2 主节点与工作节点


> 📌 一个Kubernetes集群由主节点（master）与工作节点（node）组成。

> 📌 Kubernetes的主节点（master）是组成集群的控制平面的系统服务的集合。

> 📌 API Server（API服务）是Kubernetes的中央车站。所有组件之间的通信，都需要通过API Server来完成。

> 📌 API Server对外通过HTTPS的方式提供了RESTful风格的API接口，读者上传YAML配置文件也是通过这种接口实现的。

> 📌 etcd认为一致性比可用性更加重要。这意味着etcd在出现脑裂的情况时，会停止为集群提供更新能力，来保证存储数据的一致性。

> 📌 就算etcd不可用，应用仍然可以在集群性持续运行，只不过无法更新任何内容而已。

> 📌 etcd使用业界流行的RAFT一致性算法来解决这个问题。

> 📌 controller管理器实现了全部的后台控制循环，完成对集群的监控并对事件作出响应。

> 📌 （1）获取期望状态。
   （2）观察当前状态。
   （3）判断两者间的差异。
   （4）变更当前状态来消除差异点。

> 📌 每个组件都专注做好一件事，复杂系统是通过多个专一职责的组件组合而构成的。

> 📌 从整体上来看，调度器的职责就是通过监听API Server来启动新的工作任务，并将其分配到适合的且处于正常运行状态的节点中。

> 📌 调度器并不负责执行任务，只是为当前任务选择一个合适的节点运行。

> 📌 1.监听API Server分派的新任务。
   2.执行新分派的任务。
   3.向控制平面回复任务执行的结果（通过API Server）。

> 📌 Kubelet是每个工作节点上的核心部分，是Kubernetes中重要的代理端，并且在集群中的每个工作节点上都有部署。实际上，通常工作节点与Kubelet这两个术语基本上是等价的。

> 📌 Kubelet的一个重要职责就是负责监听API Server新分配的任务。每当其监听到一个任务时，Kubelet就会负责执行该任务，并维护与控制平面之间的一个通信频道，准备将执行结果反馈回去。

> 📌 CRI屏蔽了Kubernetes内部运行机制，并向第三方容器运行时提供了文档化接口来接入。

> 📌 kube-proxy运行在集群中的每个工作节点，负责本地集群网络。

---

### 2.3 Kubernetes DNS


> 📌 集群DNS服务有一个静态IP地址，并且这个IP地址集群总每个Pod上都是硬编码的，这意味着每个容器以及Pod都能找到DNS服务。每个新服务都会自动注册到集群DNS服务上，这样所有集群中的组件都能根据名称找到相应的服务。

> 📌 集群DNS是基于CoreDNS来实现的。

---

### 2.5 声明式模型与期望状态


> 📌 kubectl会将manifest文件通过HTTP POST请求发送到控制平面，通常HTTP服务使用的端口是443。

> 📌 调度工作包括拉取镜像、启动容器、构建网络以及启动应用进程。

> 📌 命令式模式是指用户需要指定一大串针对特定平台的命令来解决相应的问题。

---

### 2.6 Pod


> 📌 Pod就是为用户在宿主机操作系统中划出有限的一部分特定区域，构建一个网络栈，创建一组内核命名空间，并且在其中运行一个或者多个容器，这就是Pod。


> 划线评论

> 📌 因为Kubernetes会启动一个新的Pod来取代有问题的Pod。
>> 💭 *2024-02-11 16:01:30* 发表想法：**如果没有controller是不会自动创建新pod的，不过，生产环境通常没有这种情况**


---

### 2.7 Deployment


> 📌 上层的控制器包括Deployment、DaemonSet以及StatefulSet。

---

### 2.8 服务与稳定的网络


> 📌 Service为一组Pod提供了可靠且稳定的网络。

> 📌 这就是Service的职责：一个稳定的网络终端，提供了基组动态Pod集合的TCP以及UDP负载均衡能力。

---

### 4.1 Pod原理


> 📌 一般来说，在微服务的设计模式中应当分离需求点，意思就是一个容器实现一个需求点。

> 📌 Pod中的所有容器都共享主机名、IP地址、内存地址空间以及卷。

> 📌 每个Pod会创建其自己的网络命名空间。其中包括一个IP地址、一组TCP和UDP端口范围，以及一个路由表。

> 📌 同一个Pod中的两个容器可以有不同的CGroup限额。

> 📌 典型的Pod生命周期是这样的：用户定义一个YAML格式的清单文件，并将其POST到API Server。一旦发送成功，清单文件中的内容就被作为一条意图记录（a record of intent）——即“期望状态”（desired state）——持久化记录在集群存储中，然后Pod被调度到一个健康的、有充足资源的节点上。一旦完成调度，就会进入等待状态（pending state），此时节点会下载镜像并启动容器。在所有资源就绪前，Pod的状态都保持在等待状态。一切就绪后，Pod进入运行状态（running state）。在完成所有任务后，会停止并进入成功状态（succeeded state）。

---

### 4.2 Pod实战


> 📌 Kubelet进程是Kubernetes在节点上的代理（agent）程序。

---

### 5.1 Deployment原理


> 📌 Deployment在底层利用了另一种名为ReplicaSet的对象。

> 📌 Deployment使用ReplicaSet来提供自愈和扩缩容能力。

> 📌 可以理解为Deployment管理ReplicaSet，ReplicaSet管理Pod。

> 📌 Kubernetes支持两种模型，不过更加青睐于声明式模型。

> 📌 期望状态能够实现的基础是底层调谐循环（reconciliation loop，也称作control loop）的概念。

> 📌 Deployment在更新前创建的ReplicaSet位于左侧，更新后创建了右侧的ReplicaSet。可以看到，更新前创建的ReplicaSet已经暂停，并不包含任何Pod。更新后的ReplicaSet已经启动了所有Pod。

> 📌 回滚与滚动升级的过程正好相反：启用旧的ReplicaSet，停用当前的ReplicaSet。

---

### 5.2 如何创建一个Deployment


> 📌 ReplicaSet的名称其实是Deployment的名称与一个hash值的拼接。

---

### 5.3 执行滚动升级


> 📌 更新的过程可以通过执行kubectl rollout status来查看。

---

### 6.1 要点前瞻


> 📌 每一个Service都拥有固定的IP地址、固定的DNS名称，以及固定的端口。

> 📌 Service利用Label来动态选择将流量转发至哪些Pod。

---

### 6.2 原理


> 📌 Service与Pod之间是通过Label和Label筛选器（selector）松耦合在一起的。

> 📌 每一个Service在被创建的时候，都会得到一个关联的Endpoint对象。整个Endpoint对象其实就是一个动态的列表，其中包含集群中所有的匹配Service Label筛选器的健康Pod。

> 📌 ClusterIP Service拥有固定的IP地址和端口号，并且仅能够从集群内部访问得到。

> 📌 NodePort Service在此基础上增加了另一个端口，这个用来从集群外部访问到Service的端口叫作NodePort。

> 📌 LoadBalancer Service能够与诸如AWS、Azure、DO、IBM云和GCP等云服务商提供的负载均衡服务集成。

> 📌 ●运行DNS服务的控制层Pod。
   ●一个面向所有Pod的名为kube-dns的服务。
   ●Kubelet为每一个容器都注入了该DNS（通过/etc/resolv.conf）。

> 📌 DNS插件会持续监测API Server中新Service的动向，并且自动注册到DNS中。因此，每一个Service都有一个可以在整个集群范围内都能解析的DNS名称。

> 📌 Service的核心作用就是为Pod提供稳定的网络连接。除此之外，还提供负载均衡和从集群外部访问Pod的途径。

---

### 7.2 服务注册


> 📌 每一个节点上都运行着一个kube-proxy，它能够为新的Service和Endpoint创建IPVS规则，从而到达Service的ClusterIP的流量会被转发至匹配Label筛选器的某一个Pod上。

---

### 7.3 服务发现


> 📌 kube-proxy是一个基于Pod的Kubernetes原生应用，它实现了一个能够监视API Server上新创建的Service和Endpoint的控制器。当它有新发现时，就回创建一条本地的IPVS规则，该规则告诉主机节点拦截发往Service的ClusterIP的流量，并发送至具体的Pod。

> 📌 在Kubernetes 1.11之后替换为IPVS

---

### 7.4 服务发现与命名空间


> 📌 FQDN的格式是<object-name>.<namespace>.svc.cluster.local。

> 📌 同一命名空间内部的对象名称必须是唯一的，不过不同命名空间之间的对象可以重名。

---

### 7.5 服务发现问题排查


> 📌 所有与集群DNS相关的对象都有K8s-app=kube-dns的Label。

---

### 11.1 安全模型


> 📌 STRIDE定义了6种潜在威胁。
   ●伪装（Spoofing）。
   ●篡改（Tampering）。
   ●抵赖（Repudiation）
   ●信息泄露（Information Disclosure）。
   ●拒绝服务（Denial of Service）。
   ●提升权限（Elevation of Privilege）。

---

### 11.2 伪装


> 📌 Kubernetes所实现的安全模型，要求组件使用mutual TSL（mTLS）认证。这就要求通信双方（发送方和接收方）必须通过加密的签名证书来相互认证。

> 📌 可以利用Kubernetes Secret将证书挂载到Pod，来对Pod进行安全认证。

> 📌 Kubernetes在具体实现时，会自动将一个服务账号令牌（Service account token）作为Secret挂载到每一个Pod中。

---

### 12.2 基础设施与网络


> 📌 Kubernetes的命名空间，并不能保证某一个命名空间中的Pod不会影响到另一个命名空间中的Pod。

> 📌 唯一能够确保真正的隔离的方式是将其置于一个独立的集群中运行。

> 📌 Kubernetes命名空间还是有用的，而且我们应当使用它——只是不要将其作为安全边界来使用。

---

