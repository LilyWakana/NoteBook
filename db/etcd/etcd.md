## command
```
export ETCDCTL_API=3
etcdctl get --prefix=true ""
etcdctl --endpoints=host:port get --prefix=true ""


# 碎片整理
// 显示revision
etcdctl --endpoints=:2379 endpoint status --write-out="json" | egrep -o '"revision":[0-9]*' | egrep -o '[0-9].*'
// 压缩
etcdctl compact your_revision
etcdctl defrag
etcdctl --endpoints=http:// .0.0.1:2379 defrag
```

## http
```
curl http://etcds.y.cn:2379/v3/keys/?recursive=true
```

## 内存使用优化
- 减少日志缓存数量
```
// 查看内存使用
etcdctl endpoint status -w table 
// 启动时设置日志数量
etcd --snapshot-count=1000
// 或者设置环境变量
ETCD_SNAPSHOT_COUNT=5000 etcd
```
etcd会把所有操作都记录到log里面。为防止内存内的log太多，当操作数达到一定值，etcd会把log写入到文件（snapshot），并移除旧的log和snapshot。默认是每1w（默认为1w，可能是因为当前大部分机器的内存都是4G以上？）次操作写一次snapshot。对于etcd v2，创建snapshot的代价是昂贵的。当etcd内存使用量过高，可以考虑减少这个阈值，从而减少缓存数量。当然，如果该值过小，则snapshot则会更为频繁。对于类似baton这种较低频的读写应用，设置为1000的话，snapshot为3分钟一次，每次耗时小于0.1s。

在设置snapshot-count 之后，最好还是整理一下碎片。碎片整理见前文。

<p align="right">
Ref: [Document: ETCD Tuning](https://coreos.com/etcd/docs/latest/tuning.html#snapshots)
</p>

## etcd节点更新
当我们启动一个节点的时候，需要标记该节点是否已经在etcd集群登记过，如果已经登记过，那么启动的时候应该加上：
```
etcd \
other flags \
--initial-cluster-state existing
```
否则如下：
```
etcd \
other flags \
--initial-cluster-state new
```

<p align="right">Ref: [Document: ETCD Clustering](https://coreos.com/etcd/docs/latest/v2/runtime-configuration.html)</p>
