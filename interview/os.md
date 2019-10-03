## 操作系统
### 进程、线程
一个进程就是一个正在执行程序的实例；进程是某种类型的活动，它有程序、输入、输出以及状态

- 运行态（此进程实际占用CPU）
- 就绪态（可运行，但因其他进程正在运行而暂时停止）
- 阻塞态（除非某种外部事件发生，否则进程不能运行）

线程：“轻量级的进程”(lightweight process)：
- 线程与进程一样，也具有三种状态，运行态、就绪态、阻塞态，并且转化关系也一样
- 共享进程内存、线程间不共享
- 有用户级、内核级

区别：
- 调度 ：在引入线程的操作系统中，线程是调度和分配的基本单位 ，进程是资源拥有的基本单位 。
- 并发性 ：在引入线程的操作系统中，不仅进程之间可以并发执行，而且在一个进程中的多个线程之间亦可并发执行
- 拥有资源 ：不论是传统的操作系统，还是设有线程的操作系统，进程都是拥有资源的一个独立 单位，它可以拥有自己的资源。 
- 系统开销： 由于在创建或撤消进程时，系统都要为之分配或回收资源，因此，操作系统所付出的开销将显著地大于在创建或撤消线程时的开销。 

进程通信：
- 管道（Pipe）：管道可用于具有亲缘关系进程间的通信，允许一个进程和另一个与它有共同祖先的进程之间进行通信。
- 命名管道（named pipe）：命名管道克服了管道没有名字的限制，因此，除具有管道所具有的功能外，它还允许无亲缘关系进程间的通信。命名管道在文件系统中有对应的文件名。命名管道通过命令mkfifo或系统调用mkfifo来创建。
- 信号（Signal）：信号是比较复杂的通信方式，用于通知接受进程有某种事件发生
- 消息（Message）队列：消息队列是消息的链接表，包括Posix消息队列system V消息队列。
- 共享内存：使得多个进程可以访问同一块内存空间，是最快的可用IPC形式。
- 内存映射（mapped memory）：内存映射允许任何多个进程间通信，每一个使用该机制的进程通过把一个共享的文件映射到自己的进程地址空间来实现它。
- 信号量（semaphore）：主要作为进程间以及同一进程不同线程之间的同步手段。
- 套接口（Socket）：更为一般的进程间通信机制，可用于不同机器之间的进程间通信


### 内存管理
分页：
- 页式存储管理将内存空间划分成等长的若干物理块，成为物理页面也成为物理块，每个物理块的大小一般取2的整数幂。内存的所有物理块从0开始编号，称作物理页号。
- 页表：与虚拟内存相关。分页系统中，允许将进程的每一页离散地存储在内存的任一物理块中，为了能在内存中找到每个页面对应的物理块，系统为每个进程建立一张页表，用于记录进程逻辑页面与内存物理页面之间的对应关系。页表的作用是实现从页号到物理块号的地址映射，地址空间有多少页，该页表里就登记多少行，且按逻辑页的顺序排列。实际地址：页号+页内地址
- “联想存储器”或“快表”：分页系统中，CPU每次要存取一个数据，都要两次访问内存（访问页表、访问实际物理地址）。为提高地址变换速度，增设一个具有并行查询能力的特殊高速缓冲存储器

分段：
- 页面是主存物理空间中划分出来的等长的固定区域。分页方式的优点是页长固定，因而便于构造页表、易于管理，且不存在外碎片。但分页方式的缺点是页长与程序的逻辑大小不相关。
- 段是按照程序的自然分界划分的长度可以动态改变的区域。通常，程序员把子程序、操作数和常数等不同类型的数据划分到不同的段中，并且每个程序可以有多个相同类型的段。
- 寻址：段号+段内地址


分页对程序员而言是不可见的，而分段通常对程序员而言是可见的，因而分段为组织程序和数据提供了方便。与页式虚拟存储器相比，段式虚拟存储器有许多优点：

段+页即段页式