# NPU learning path

Do not begin by memorizing acronyms. Start with three questions: **where is each object, how does data move,
and what controls the work?**

## Suggested order

1. [NPU mental model](npu/mental-model.md): distinguish a die, package, card, Device, and AI Core.
2. [Core glossary](npu/glossary.md): place frequent terms in one consistent hierarchy.
3. [Data movement and H2D](npu/data-movement.md): follow a tensor from CPU memory to a compute unit and back.
4. [Network planes and uplinks](npu/network-planes.md): separate control, data, parameter, storage, and physical links.

## Always draw two diagrams

- A **physical topology** showing CPUs, NPUs, PCIe switches, device interconnects, NICs, and network switches.
- A **data path** showing source and destination memory, buses, copy engines, and synchronization points.

The same word may refer to different layers in hardware, drivers, communication libraries, and cluster networking.
Replace an ambiguous statement such as “data is slow” with “H2D bandwidth from Host DRAM to Device HBM is low.”

## Scope

These pages explain general NPU concepts and use common Ascend terminology as concrete examples. AI Core composition,
memory hierarchies, interconnects, and port mappings vary by product generation. Consult the matching product manual
before applying a hardware-specific statement.
