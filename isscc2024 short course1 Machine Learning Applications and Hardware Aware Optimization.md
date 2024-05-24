# Cource 1：Introduction to Machine Learning Applications and Hardware Aware Optimizations
这个course分四个部分进行讲解：
1. 介绍了机器学习和深度神经网络
2. 机器学习中硬件设计的趋势和挑战
3. 单芯片性能扩展方法
4. 多芯片集成方法


## 1.Introduction to machine learning and deep neural networks
这部分没有好说的，基础知识普及，从机器学习的定义到深度神经网络的分类，诸如CNN，卷积，激活函数等，介绍了常用的几种CNN，attention等
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/192a55305d224b289912860978ec7386.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/e26bbe376966482494d18460e6afc172.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/56cdc7613bbd405db64e79c6f54ee736.png)

## 2.Trends and challenges in hardware design
1） 应用的多样性快速增长
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/e106eca050e546d4b902bee63ccebf75.png)
2）模型大小的增加以及可扩展性的要求
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/c8d206c35cc84c338538c4cc281dcce0.png)

3）硬件性能和功耗的挑战
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/755f2ea5f00c488ea7c23636c14cdc20.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/5643e9404c2b4bc28149f03789b671db.png)
## 3.Approaches to scaling single chip performance
 重点讨论了如何在单个芯片层面上提升机器学习硬件的性能，主要聚焦于两个关键技术手段：量化（Quantization）和稀疏性（Sparsity）。

1）. **量化（Quantization）**：
   - 量化技术利用了深度学习模型内在的容错性，通过降低数值表示的精度来减少计算和存储需求。传统的浮点运算会被转换成使用较少比特数的整数或定点运算，例如FP32转换为INT8或更低精度的格式（如FP16, FP8）。
   - ![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/beab22af281249cdacf8fe90271ed7ad.png)

   - 量化的好处包括：
     - **加速数学运算**：利用更高吞吐量的数学运算流水线加速计算过程。
     - ![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/839d0a4d18a64fad8e558e8b665db2f0.png)

     - **减少内存流量**：因每个数值占用的位数减少，降低了内存读写需求。
     - ![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/399f2009b33148f6a343b02162bea33c.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/41622ee717cd4d60a126f758eafdbb61.png)

     - **减小存储需求**：需要更少的硬件资源来存储模型参数。
     - **节能**：减少了数据移动的能耗。
   - 然而，量化也带来了效率与准确度之间的权衡，因为精度的降低可能会导致模型准确度的损失。

2）. **稀疏性（Sparsity）**：
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/526bcefa52bc414ab10f013e0c20082d.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/36f57ae00f01490db9ec721beb574142.png)
   - 神经网络中存在大量的权重和激活值为零或接近零的现象，利用这种自然稀疏性可以避免无效的计算，从而提高效率。
   - **未结构化稀疏性**：处理任意位置的零值，例如SCNN（Sparse CNN）通过只计算非零元素的乘积来减少计算量，同时对传统的滑动卷积操作提出质疑，因为大部分元素为零时，常规操作显得低效。
   - **结构化稀疏性**：如在特定模式或块中的零值，某些加速器能更好地利用这类稀疏性，例如在NVIDIA的Ampere A100和Hopper H100中，结构化稀疏性能提升可达两倍。
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/408cf562b1c84d0a9f718d0ca267010c.png)

综上，通过量化和利用稀疏性，硬件设计者能够在单个芯片上显著提升机器学习算法的执行效率，同时控制成本和功耗。这些技术的实施需要细致的硬件优化和软件算法的协同设计，以确保在不牺牲模型准确度的前提下实现性能的最大化。
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/60c6abd4285b402987bbe1f5e723957a.png)


## 4.Scaling beyond single chip with package level integration
### 优势
超越单芯片性能：包级集成可以突破单个芯片的物理尺寸限制（如光罩限制），允许在一个封装内集成多个同类或异类芯片。这样可以有效地提升系统的计算能力和存储容量​​。
异质集成：能够集成具有不同功能的专用芯片（如计算、存储和I/O芯片），从而形成一个综合性能更高的系统。此外，还可以混合不同的工艺技术，以优化每个芯片的性能和功耗​​。
可扩展性：根据不同的产品需求，可以灵活调整集成的芯片数量，以满足不同的性能目标。例如，通过增加更多的计算芯片，可以提升整体的计算能力；通过增加存储芯片，可以提升存储容量​​。
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/7c450de847a64e3593eee6286f4033ac.png)

### 挑战
数据移动和通信：包级集成需要高效的芯片间通信架构，以确保各芯片之间的数据传输能够快速且能耗低。为此，采用高效的通信协议和低功耗的信号传输技术是必要的​​。
并行计算：为了实现大规模并行计算，系统需要在多个芯片上有效地分配计算任务。需要优化算法和硬件设计，以充分利用各个芯片的计算能力​​。
### 具体技术
片上网络（NoC）和封装网络（NoP）：通过层次化的网络架构，可以减少通信中的跳数和拥塞，提升整体通信效率​​。
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/e5877841409c4eccb5f9b27c65948a97.png)

芯片间链接：采用如地参考信号（GRS）等高效通信技术，实现高速度（11-25 Gbps每个引脚）和高能效（0.82-1.75 pJ/bit）的芯片间通信​
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/8d8c9ac21eb24575b19551358de6b427.png)
## summary
深度学习是未来硬件设计的关键驱动力

多样化的应用：卷积神经网络（CNNs）、大语言模型（LLMs）等
计算和内存需求继续快速增长
定制硬件加速器能够提升单芯片性能
硬件软件协同设计技术非常有前景
量化和稀疏性提供了有趣的机会
包级集成使扩展超越单芯片成为可能
克服光刻机限制
高效的通信架构和利用并行性是实现可扩展性的关键






