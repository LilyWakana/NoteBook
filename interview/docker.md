

## Docker
### 虚拟化
虚拟化允许您在相同的硬件上运行两个完全不同的操作系统。每个客户操作系统都经历了引导，加载内核等所有过程。您可以拥有非常严格的安全性，例如，客户操作系统无法完全访问主机操作系统或其他客户端并搞砸了。
- 仿真
- 半虚拟化
- 基于容器的虚拟化

### 什么是docker
Docker是一个容器化平台，它以容器的形式将您的应用程序及其所有依赖项打包在一起，以确保您的应用程序在开发，测试或生产的任何环境中无缝运行。


### 与虚拟机的区别
Docker不是虚拟化方法。它依赖于实际实现基于容器的虚拟化或操作系统级虚拟化的其他工具。为此，Docker最初使用LXC驱动程序，然后移动到libcontainer现在重命名为runc。Docker主要专注于在应用程序容器内自动部署应用程序。应用程序容器旨在打包和运行单个服务，而系统容器则设计为运行多个进程，如虚拟机。因此，Docker被视为容器化系统上的容器管理或应用程序部署工具。

- 与虚拟机不同，容器不需要引导操作系统内核，因此可以在不到一秒的时间内创建容器。此功能使基于容器的虚拟化比其他虚拟化方法更加独特和可取。
- 由于基于容器的虚拟化为主机增加了很少或没有开销，因此基于容器的虚拟化具有接近本机的性能
- 对于基于容器的虚拟化，与其他虚拟化不同，不需要其他软件。
- 主机上的所有容器共享主机的调度程序，从而节省了额外资源的需求。
- 与虚拟机映像相比，容器状态（Docker或LXC映像）的大小很小，因此容器映像很容易分发。
- 容器中的资源管理是通过cgroup实现的。Cgroups不允许容器消耗比分配给它们更多的资源。虽然主机的所有资源都在虚拟机中可见，但无法使用。这可以通过在容器和主机上同时运行top或htop来实现。所有环境的输出看起来都很相似。

### Docker镜像和层有什么区别？
- 镜像：Docker镜像是由一系列只读层构建的
- 层：每个层代表镜像Dockerfile中的一条指令。

### 什么是Docker Swarm？
Docker Swarm是Docker的本机群集。它将Docker主机池转变为单个虚拟Docker主机。Docker Swarm提供标准的Docker API，任何已经与Docker守护进程通信的工具都可以使用Swarm透明地扩展到多个主机。


### 为什么Docker Compose不会等待容器准备就绪，然后继续以依赖顺序启动下一个服务？
Compose按照依赖顺服启动和停止容器，决定依赖关系语句有 depends_on, links, volumes_from, 和network_mode: "service:...".

但是，对于启动，Compose不会等到容器“准备好它运行“。这里有一个很好的理由：
- 等待数据库（例如）准备就绪的问题实际上只是分布式系统更大问题的一个子集。在生产中，您的数据库可能随时变得不可用或移动主机。您的应用程序需要能够适应这些类型的故障。
- 要处理此问题，请将应用程序设计为在发生故障后尝试重新建立与数据库的连接。如果应用程序重试连接，它最终可以连接到数据库。
- 最佳解决方案是在启动时以及出于任何原因丢失连接时，在应用程序代码中执行此检查。

