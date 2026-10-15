# Core glossary

## Hardware and identities

| Term | Short explanation | Ask during diagnosis |
| --- | --- | --- |
| Die | Silicon cut from a wafer; a package may hold several dies | Physical Die ID or logical ID? |
| Package | Installable component containing one or more dies | How many dies are present? |
| NPU | Processor optimized for neural-network and tensor work | Which vendor, model, and generation? |
| Device | An accelerator object enumerated and managed by a runtime | How does Device ID map to physical location? |
| Rank | Logical participant in a communication domain | How does it map to node, Device, and port? |
| AI Core | A compute resource inside an NPU | Is this a matrix core, vector core, or coupled design? |

## Memory and movement

| Term | Expansion | Direction or role |
| --- | --- | --- |
| Host Memory | Host memory | DRAM directly accessible by the CPU |
| Device Memory / GM | Device Global Memory | Large NPU-side memory, commonly implemented with HBM or DDR |
| Local Memory | On-chip local storage | Small, fast storage near an AI Core, such as UB, L1, or L0 |
| H2D | Host to Device | Host Memory → Device Memory |
| D2H | Device to Host | Device Memory → Host Memory |
| D2D | Device to Device | A copy within or between devices; inspect the context |
| P2P | Peer to Peer | Direct access or copies between devices without Host staging |
| DMA | Direct Memory Access | A dedicated engine moves data without CPU byte-by-byte work |
| MTE | Memory Transfer Engine | Ascend terminology for engines moving data through AI Core memory levels |

## Interconnect and communication

| Term | Short explanation |
| --- | --- |
| PCIe | A common I/O bus connecting CPUs, NPUs, and NICs; H2D/D2H often traverse it |
| PCIe Switch | A device that expands and aggregates PCIe links, affecting reachability and shared bandwidth |
| Scale-up | High-bandwidth, low-latency expansion inside a node or tightly coupled system |
| Scale-out | Expansion across servers or racks through a network fabric |
| Collective | A multi-Rank operation such as AllReduce, AllGather, or Broadcast |
| RDMA | Remote access to registered memory with reduced CPU involvement and copying |
| RoCE | A family of protocols that carries RDMA over Ethernet and requires suitable congestion configuration |
| HCCL | Ascend's collective communication library for multi-NPU communication |
| HCCS | Ascend terminology for a high-speed coherent system interconnect; capabilities vary by product |

## Terms ending in “plane”

| Term | Common meaning |
| --- | --- |
| Control plane | Discovery, configuration, connection setup, resource management, and state maintenance |
| Data plane | The frequent path that carries actual tensor or message payloads |
| Parameter plane | A cluster network carrying gradients, weights, and other model-parameter synchronization traffic |
| Storage / sample plane | A network carrying datasets, models, checkpoints, results, and logs |
| Service / management plane | Job submission, cluster management, monitoring, and normal service access |

!!! warning "Confirm the context"

    “Data plane” describes a functional role, while “parameter plane” often describes a cluster network by workload.
    They are not necessarily peer categories. A communication library's data plane may carry parameter synchronization;
    a network designer may use “data network” to mean sample or service traffic.
