# AI 训练数据基础设施设计实践

> Copyright (c) 2026 Qingke. All rights reserved.  
> 未经版权所有者事先书面许可，禁止复制、修改、分发、改编或创建衍生作品。详见 [LICENSE](LICENSE)。

这一篇的主要内容是记录当前AI训练基座的相关内容

## 版权与使用限制

本项目内容版权归 Qingke 所有。除非获得版权所有者事先书面许可，任何人不得复制、修改、分发、改编、再许可、公开发布、用于商业用途或创建衍生作品。完整条款见 [LICENSE](LICENSE) 和 [COPYRIGHT.md](COPYRIGHT.md)。

## 文档结构

本项目已按章节拆分为多个文件夹和 Markdown 文件，便于后续维护、阅读和扩展。

```text
docs/01-数据流设计/
docs/01-数据流设计/README.md
docs/01-数据流设计/01-01-数据流概述.md
docs/01-数据流设计/01-02-数据飞轮系统.md
docs/02-存储架构设计/
docs/02-存储架构设计/README.md
docs/02-存储架构设计/02-01-存储系统分层抽象.md
docs/02-存储架构设计/02-02-远端存储层（Remote-Storage-Layer）.md
docs/02-存储架构设计/02-03-缓存层（Cache-Layer）.md
docs/02-存储架构设计/02-04-文件系统层（Filesystem-Layer）.md
docs/02-存储架构设计/02-04-小结.md
docs/02-存储架构设计/02-05-基于-JuiceFS-的-AI-训练存储基座实践.md
```

## 目录

- [1 数据流设计](docs/01-数据流设计/README.md)
  - [1.1 数据流概述](docs/01-数据流设计/01-01-数据流概述.md)
  - [1.2 数据飞轮系统](docs/01-数据流设计/01-02-数据飞轮系统.md)
- [2 存储架构设计](docs/02-存储架构设计/README.md)
  - [2.1 存储系统分层抽象](docs/02-存储架构设计/02-01-存储系统分层抽象.md)
  - [2.2 远端存储层（Remote Storage Layer）](docs/02-存储架构设计/02-02-远端存储层（Remote-Storage-Layer）.md)
  - [2.3 缓存层（Cache Layer）](docs/02-存储架构设计/02-03-缓存层（Cache-Layer）.md)
  - [2.4 文件系统层（Filesystem Layer）](docs/02-存储架构设计/02-04-文件系统层（Filesystem-Layer）.md)
  - [2.4 小结](docs/02-存储架构设计/02-04-小结.md)
  - [2.5 基于 JuiceFS 的 AI 训练存储基座实践](docs/02-存储架构设计/02-05-基于-JuiceFS-的-AI-训练存储基座实践.md)

## 后续章节占位

- 3 架构权衡（待补充）
- 4 性能评估（待补充）
- 5 后续优化方向（待补充）
