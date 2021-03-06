CPU亲缘性可以理解为让进程尽可能长时间的运行在某个指定的逻辑处理器上，而不会频繁的在各个不同的逻辑处理器上切换。对于我们来说，如果进程能够减少在逻辑处理器上的切换，即意味着进程的消耗可能会更小。
这里先自行回顾和思考下:
1.逻辑CPU和物理CPU有什么区别？
2.进程什么时候一定要让出自己的计算资源呢？
3.进程在CPU间切换，会造成什么消耗呢？

在内核当中，每一个进程都有一个task_struct的数据结构。其中有个affinity的变量，我们可以通过设置cpus_allowed位的掩码来设置进程CPU的亲缘性。其实在内核当中，都会实现进程调度算法，尽可能减少CPU间的任务切换。那我们为什么还需要指定CPU的亲缘性呢？

我们怎么获取和设置CPU亲缘性相关的信息呢？
```
查看进程运行所在的CPU
# ps里面增加-F的选项可以显示进程运行在哪个逻辑CPU上
# CPU编号在 C 列上
ps -F

设置进程绑定CPU运行
# 进程启动时绑定CPU
# 0,5,7,9-11
taskset -c 1 command # 绑定CPU 1运行
taskset -c 0,1 command # 绑定CPU 0,1运行

# 运行中进程绑定CPU
taskset -cp 1 5200 # PID为5200的进程绑定CPU 1运行
```
我们在使用nginx的时候，需要留意 worker_cpu_affinity 这个配置，他可以设置nginx worker进程的亲缘性，可以试下增加这个配置，然后验证下nginx worker使用的cpu有什么变化。设置好了亲缘性之后，可以试下用ab, wrk等工具验证下，究竟给nginx设置亲缘性是好是坏，为什么呢？
