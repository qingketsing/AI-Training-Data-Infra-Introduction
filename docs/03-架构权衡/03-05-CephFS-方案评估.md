# 3.5 CephFS 方案评估

> Copyright (c) 2026 Qingke. All rights reserved.
> 未经版权所有者事先书面许可，禁止复制、修改、分发、改编或创建衍生作品。详见 [LICENSE](../../LICENSE)。

[返回本章目录](README.md) · [返回总目录](../../README.md)


CephFS 是构建在 RADOS 之上的分布式文件系统。它由 MDS 管理目录和文件元数据，客户端通过 Kernel Client、FUSE 或 CSI 挂载，并直接访问 OSD 中的文件数据。参见 [Ceph 架构文档](https://docs.ceph.com/en/latest/architecture/)。

#### 3.5.1 分布式文件系统能力

```text
训练与数据处理节点
        ↓
CephFS Kernel Client / FUSE / CSI
        │
        ├── MDS：目录与文件元数据
        └── OSD：文件实际数据
```

CephFS 能在通用硬件上提供共享文件系统，并通过增加 OSD、存储节点和 MDS 扩展容量与性能。聚合数据、模型文件和 Checkpoint 可以由多个客户端并行访问，也可以通过 [Ceph CSI](https://github.com/ceph/ceph-csi) 接入 Kubernetes。

#### 3.5.2 小文件与元数据

小文件和目录操作主要受 MDS 缓存、客户端数量和目录分布影响。多活 MDS 能够分担大量客户端在不同目录上的元数据负载，但不会让所有工作负载等比例提升，仍需使用接近生产规模的文件数量验证。参见 [多活 MDS](https://docs.ceph.com/en/latest/cephfs/multimds/) 和 [CephFS 应用最佳实践](https://docs.ceph.com/en/latest/cephfs/app-best-practices/)。

#### 3.5.3 对象复用与多云边界

CephFS 和 Ceph RGW 虽然都使用 RADOS，但采用不同的数据组织与命名空间。已有 OSS、S3 或 RGW 对象不能直接作为 CephFS 中的原生文件使用，通常仍需迁移或同步。

CephFS 可以将目录快照异步镜像到远端 CephFS，适合灾备和区域副本，但目标云需要运行另一套 Ceph 集群，不等同于跨云共享写入的全局文件系统。参见 [CephFS 快照镜像](https://docs.ceph.com/en/latest/cephfs/cephfs-mirroring/)。

#### 3.5.4 建设与运维成本

CephFS 没有 GPFS 类型的软件 License 成本，但需要维护 MON、MGR、MDS、OSD、存储池、故障域和恢复流量。磁盘故障、扩缩容和数据回填会与前台训练争用网络与磁盘，因此硬件规划、监控和故障处理经验会直接影响使用效果。

#### 3.5.5 当前场景下的判断

在自有数据中心、已有 Ceph 集群或共享写入较多的环境中，CephFS 是比自建 NAS 更有扩展性的候选方案。但当前架构更强调已有云对象存储复用、多云训练和模型分发，建设完整 Ceph 数据面会增加迁移与运维成本，因此其综合适配度仍低于 JuiceFS。
