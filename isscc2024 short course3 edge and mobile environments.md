分两大块：
ML处理器的能效问题
跨层优化和异构多核的必要性
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/e1a40af3a0d44620b1ace2c2121435f5.png)
边缘设备智能化：边缘系统包括可穿戴设备、植入式设备、智能扬声器、无人机、汽车等，它们需要智能处理能力来处理数据并做出决策。

tinyML挑战：在资源受限的边缘设备上实现机器学习（被称为tinyML）面临诸多挑战，包括有限的内存、实时处理需求（低延迟）、以及低能耗限制。

模型选择：并非所有深度神经网络（DNN）都适用于边缘设备。需要根据任务的复杂性、可用的计算资源和能耗预算来选择合适的模型。
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/ee7461418bb244c6987e2f0f25e909a2.png)

## 1.Efficiency techniques in ML processors
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/20aae1650394494e9e50af1c83e9cfc3.png)

1. **数据重用（Data Reuse）**：
   - **空间重用（SpatialReuse）**：通过在数据路径中重复使用权重（weights）和输入（inputs），减少对片外存储器（如DRAM）的访问次数，从而降低能耗。

   ![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/b3d6487ddeac416c90037e4845b47567.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/ec8dda99eec04b46b1901b21a5f99ca6.png)
   - **时间重用（TemporalReuse）**：在内存层次结构中重复使用数据，以减少数据访问次数和能耗。

![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/66579b230db449e884384576e60c3e8e.png)

2. **降低精度（Reduced Precision）**：
   - 利用神经网络推理过程中对精度的容忍度，使用较低的数值精度（如2-4-8位整数），以减少内存和计算能耗。
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/97bf874507914180a6e76a7243439761.png)

举了一个jssc18的例子
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/307dbd67887d4a269b557a5f2c750a28.png)


3. **稀疏性（Sparsity）**：
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/6bb0a31630cd40be83150e2ba2f0446c.png)

   - 神经网络中存在大量的零值（尤其在ReLU激活函数后），可以通过稀疏性减少计算和存储需求。
   - 通过量化、显式网络剪枝或压缩进一步增加稀疏性。
   - GPU处理稀疏性的方法
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/f505e0b090ab4702aa2344503882799e.png)

4. **融合处理（Fused Processing）**：
   - 将多个操作融合在一起执行，以减少数据移动和提高效率。
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/e6e275a630aa4ae8b591a05e2aa8d41b.png)

5. **跨层优化和异构多核的需求（Cross-layer Optimization and Heterogeneous Multi-core）**：
   - **调度/映射（Scheduling/Mapping）**：在不同层次之间进行优化，以提高资源利用率和性能。
   - 目标：优化整个系统的能耗、延迟和吞吐量，同时考虑到硬件资源的限制和工作负载的特性。
   - 挑战：在边缘和移动设备上，资源受限，因此需要精细地管理和调度计算任务，以最大化效率。
   - 调度策略
   层级调度：在神经网络的不同层之间进行调度，以平衡计算负载和资源使用。
数据流映射：根据数据流的特点，将计算任务映射到最适合执行它们的硬件单元上。
映射策略
 静态映射：在编译时决定计算任务与硬件单元的映射关系，适用于性能预测和优化。
动态映射：运行时根据当前系统状态和资源利用情况动态调整映射关系，可以提高资源的灵活性和利用率。
优化目标
内存带宽：减少对外部存储器（如DRAM）的访问，降低内存带宽需求。
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/845516a414a74bb8bb92a42ae721125b.png)

计算效率：提高处理器的计算效率，减少空闲周期。
能耗：降低整体能耗，特别是在电池供电的移动设备上尤为重要。
软件和硬件的协同设计
编译器优化：编译器在编译时进行代码优化，考虑硬件特性和调度策略。
硬件支持：硬件设计需要支持灵活的调度和映射，如可编程的硬件加速器。
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/fc3ce30c2c4e43dfb0c773788ce3cd22.png)


结论
跨层优化，特别是调度/映射，对于实现边缘和移动设备上的高效机器学习硬件加速至关重要。
需要综合考虑算法、硬件架构和软件管理，以实现最优的性能和能效。


   - **多核探索（Multi-core Exploration）**：研究如何利用多个处理核心来提升性能。
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/fc81aceba2bb42c98292485772c6fe6a.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/70ccbed589544e679d7c80f80604bc03.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/7da854c14bca4843a893adc955c4d523.png)

   - **异构性的需求（The Need for Heterogeneity）**：探讨不同类型核心的组合是否可以提供额外的性能优势。
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/12679d375b5d4e55be8a6ba1a77a9c2b.png)
数字核
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/17cc1a5a325e4753905d2096fb7d023a.png)
模拟核
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/69f3b042d2ab4d968661e9430a11adb0.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/37799e764b9c4998afebcd17cd7420d0.png)



介绍了一个ai soc异构多核的例子
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/a58d113484e34c15a96fec8737defb4c.png)

