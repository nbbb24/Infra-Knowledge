# 昇腾 NPU 基础知识

面向 NPU、MemFabric 和大模型推理场景的中文学习笔记。重点不是孤立地背缩写，而是先判断一个概念属于
硬件、内存、数据方向、互联协议、网络拓扑还是软件层。

!!! note "阅读范围"

    本站优先解释稳定的通用概念，并用昇腾常见术语举例。AI Core 组成、内存层次、互联能力和端口映射
    会随型号与架构代际变化，硬件相关结论最终应以对应产品手册为准。

## NPU 知识地图

| 层次 | 关键概念 | 要解决的问题 |
| --- | --- | --- |
| 硬件层 | NPU、Die、AI Core、AICPU、HBM | 谁负责计算，数据存在哪里？ |
| 内存层 | Host、Device、NUMA、VA、PA、MR | 内存由谁管理，地址如何访问？ |
| 搬运层 | H2D、D2H、D2D、P2P、DMA | 数据从哪里搬到哪里？ |
| 通信层 | PCIe、HCCS、RoCE、RDMA、URMA | 数据通过什么链路和语义传输？ |
| 网络与软件层 | 参数面、数据面、出框口、HCCL、HCOMM | 网络如何组织，软件怎样管理通信？ |

```mermaid
flowchart LR
    A[硬件与拓扑] --> B[内存与地址]
    B --> C[数据搬运方向]
    C --> D[互联与通信]
    D --> E[性能与故障定位]
```

## 推荐学习顺序

1. [NPU 硬件与层级](npu/mental-model.md)：区分 Die、Package、Card、Device 和 AI Core。
2. [数据搬运与 H2D](npu/data-movement.md)：理解 Host、Device 和片内存储之间的数据流。
3. [网络平面与出框口](npu/network-planes.md)：区分参数面、存储面、控制面和数据面。
4. [互联、协议与通信软件](npu/interconnects.md)：建立 PCIe、HCCS、RDMA、URMA、HCCL 的层次。
5. [内存、NUMA 与地址](npu/memory-addressing.md)：理解数据可达性、映射和注册。
6. [一次端到端数据传输](npu/end-to-end-transfer.md)：把前面的概念放进跨节点 KV Cache 传输过程。
7. [性能分析与常用工具](npu/performance-tools.md)：从带宽、延迟、拓扑和计数器定位瓶颈。

## 学习时始终画两张图

- **物理拓扑图**：CPU、NPU、PCIe Switch、卡间互联、网卡和交换机分别在哪里。
- **数据路径图**：源内存、目标内存、经过的链路、执行搬运的引擎以及同步点是什么。

同一个词在硬件、驱动、通信库和集群网络中可能指向不同层次。遇到“数据很慢”这样的描述，应继续追问：
是 Host DRAM 到 Device HBM 的 H2D 慢，还是跨节点 NPU 通信慢？数据大小、并发和同步方式又是什么？
