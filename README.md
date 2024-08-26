
# DeepSwarm——一种新型边缘群体智能感知-计算耦合框架（通过数据采集和计算的双向优化实现群体深度学习）

**Organization:** Northwestern Polytechnical University

**Author:** Sicong Liu, Bin Guo, Ziqi Wang, Lehao Wang, Zimu Zhou, Xiaochen Li, Zhiwen Yu

To appear at **FCS 2024**
[`Paper`](https://journal.hep.com.cn/fcs/EN/10.1007/s11704-024-40465-z)

### Please help me with the citation, citation format：
Sicong LIU, Bin GUO, Ziqi WANG, Lehao WANG, Zimu ZHOU, Xiaochen LI, Zhiwen YU. DeepSwarm: Towards Swarm Deep Learning with Bidirectional Optimization of Data Acquisition and Processing. Front. Comput. Sci., https://doi.org/10.1007/s11704-024-40465-z

## 摘要

在**资源受限**的移动设备（mobile device）和嵌入式设备（embedded device）中，**设备端深度学习 （on-device deep learning）** 的兴起激发了各种应用。然而，现有的设备上深度学习主要依赖于**预定义**的处理模式来对**特定**的输入数据做出**响应**，从而导致**准确性**和**资源效率**瓶颈。在这项工作中，作者主张向 **Swarm Deep Learning** 的范式转变，其灵感来自在群体中观察到的集体智慧，其中个体的主动行动实现了更好的全局性能。利用物联网场景中物理相邻的移动和嵌入式设备形成的集群的潜力，作者提出 DeepSwarm，这是一个旨在突破 on-device DL 性能边界的闭环系统框架。特别是，*DeepSwarm* 将主动数据采集和处理与**双向优化**相结合，以最大限度地减少冗余并提高资源效率。它通过深度学习反馈及时解决数据限制和冗余问题，利用数据的互补性和异步性进行可扩展的处理。最后，作者讨论了提高 *DeepSwarm* 性能的研究挑战和机遇，并展示了两个初始实例（群体深度学习自适应、群体联邦学习），以展示其优势。

## 问题

### 概述

*DeepSwarm* 主要解决了移动和嵌入式物联网设备上**设备端深度学习**（on-device DL）的**系统精度**和**资源效率**之间实现完美的权衡的问题。传统的设备端DL系统依赖于**预定义的处理模式**，这导致在处理数据冗余和缺乏数据采集与处理阶段之间的实时反馈，从而导致**准确性**和**资源效率**瓶颈。

### 详情

嵌入式深度学习(Embedded deep learning, Embedded DL)系统将深度学习部署在资源受限的边缘设备上，这在智能物联网 (Artificial Intelligence of Things，AIoT) 中发挥着关键作用。直接在智能物联网终端设备上执行先进深度学习模型，使其能够收集、处理和解释本地传感器数据，不仅提高了**数据隐私安全和终端设备响应能力**，还节省了**网络带宽**。然而，使深度学习模型适应动态变化的**可用存算资源**和**多源异构传感器数据**并非易事，尤其是在**资源有限**的智能物联网边端设备上，努力满足智能物联网应用程序的实时性和成本效益需求非常困难。为此，资源高效的嵌入式深度学习为各种智能物联网应用领域开辟了新的可能性，包括医疗保健、智能家居、自动驾驶、工业自动化等领域。

尽管研究者们之前已经做了一些工作，但智能物联网系统仍存在**两大主要问题**，使得在**系统精度**和**资源效率**之间实现完美的权衡仍然具有挑战性：

 - 由于智能物联网终端设备**资源限制**，为提高资源利用效率而压缩的深度学习模型在进行推理任务时**面临精度受限的问题**。
 - 虽然采集**丰富感知数据**的传感器数量和类型（例如摄像头、激光雷达和高光谱成像仪等）激增，但来自单个终端设备的实时感知数据通常有限，导致在低分辨率、小尺寸和运动模糊等具有挑战性的**高质量数据需求的场景**中，存在感知和推理精度显著下降等问题。

## 动机

### 概述

*DeepSwarm* 的动机是利用物联网设备中的群体智能，旨在从被动系统转向主动系统，通过双向优化实现更好的数据采集与处理。这种方法旨在最大限度地减少数据冗余，提高资源效率，从而解决当前设备端DL系统的局限性。

### 嵌入式深度学习到感知-计算耦合集群系统（Swarm Deep Learning）的范式转变

为了进一步增强深度学习和智能物联网系统之间的协同作用，以提高**单个**终端设备以外集群的**整体**性能，作者创新性提出了一种从嵌入式深度学习到**感知-计算耦合集群系统**的范式转变，称为**集群深度学习 (swarm deep learning, swarm DL)系统**。swarm DL系统将嵌入式深度学习，即单个智能物联网终端设备上资源高效的模型扩展到具有群体智能概念的**协作**环境中。swarm DL系统以嵌入式数据挖掘为基础，通过对传感器**数据采集和处理**之间的**相互反馈**的集成与优化，提高智能物联网系统应对复杂环境和集群自适应协同能力。

特别地，在**传统物联网系统**中（如图所示），嵌入式深度学习在单个设备上一般依据**预定义**的感知资源与计算资源的方式高效处理本地传感器数据，存在**模式固化、适应能力不足**等问题，难以实现高动态场景中**感知与计算的有效联动**。与传统的物联网系统不同，*swarm DL*系统在**水平方向**上与多个分布式设备高效协作，在**垂直方向**上采用传感器数据采集和传感器数据处理模块的协同设计的方式，可以实现高动态场景中感知与计算的有效联动，充分利用单一设备**局部感知能力和有限计算资源**，增强系统**协作感知与计算能力**，提高智能物联网系统的适用性与鲁棒性。同时，*swarm DL*系统致力于构建一个**多智能体网络**，主动收集来自多个数据源的传感器数据，实现全面和精确的目标或情境感知，以优化系统运行效率，并使整个系统适应复杂动态协作环境中**设备内和设备间**的动态相互作用。这种感知-计算耦合范式不仅提高了单个设备的性能，而且为**分散**和**弹性可伸缩**的智能物联网系统铺平了道路。
![将单个设备上的资源高效型 DL 引入网络系统，采用感知-计算耦合方法](https://i-blog.csdnimg.cn/direct/8ce9eaf7b85f40cc867a5089d2a82b5c.png#pic_center)

### 系统需求

*Swarm DL*以设备上的深度学习为基础，主动**扩展**数据采集和处理，并为用户提供**双向优化反馈**，形成闭环。这种范式旨在最大限度地提高隐式互补性，并最大限度地减少群体内数据采集和处理的冗余，从而促进更高效和可扩展的物联网系统。具体而言，*Swarm DL*通过利用配备先进传感器和深度学习计算能力的物联网设备作为**proactive agents**来实现群体智能，体现了以下愿景：

 - *Proactive Data Acquisition for DL*：与传统的传感器数据采集先于**固定的数据处理完成**范式不同，*Swarm DL*使每个物联网设备都能**利用基于DL的数据处理的运行时反馈，尽快解决数据采集过程中数据缺失和冗余的问题。**每个设备都主动地在本地运行，利用全球数据分布的本地代理和有限的资源，以自组织的方式提高协作性能，并促进更准确和高效的数据采集。
 - *Proactive Data Processing by DL*：为了利用采集数据的互补性和异步性，即系统问题，*Swarm DL* **主动扩大/缩小**设备上的 DL 模型子结构和底层系统配置。这种本地适应优化了**全局**性能（例如，准确性、延迟、能源成本、内存使用），同时了解群体上的动态资源可用性。此外，与单独执行设备上的深度学习不同，**主动**群体设备对**非静止移动环境具有更大的适应性**，这些环境通过主动学习实现数据漂移。
   ![*DeepSwarm* 将群体智能集成到设备上的深度学习 （DL） 中，以便在资源稀缺的代理处实现主动数据采集和处理，同时满足系统应用程序需求。](https://i-blog.csdnimg.cn/direct/a0f98907f5fd4f8d926d7bec357ae064.png#pic_center)

### 系统独特性

在目前的研究中，有很多相关概念容易引起与*Swarm DL*的混淆，如*群体智能（Swarm Intelligence）*、*设备上深度学习（On-device DL）*、*分布式深度学习卸载（Distributed DL offloading）*、*联邦学习（Federated Learning）*、*群体感知（Crowd Sensing）*等。但是，*Swarm DL* 在本质上与这些概念有很大不同。如图所示，将 Swarm DL 与其他概念进行比较，突出了其独特的特性：

 - Swarm DL vs. Swarm Intelligence。Swarm DL 系统代表了群体智能概念的具体实例化。特别地，群体智能指定了swarm DL中所需的特征，包括：自组织，自适应和自主演化。Swarm DL 系统使用深度学习赋能的智能物联网设备作为群体中的智能体来实现群体智能在很大程度上尚未探索。同时，联合优化分布式边缘设备感知配置、深度学习模型、硬件资源等，以增强群体智能系统的性能、可扩展性和鲁棒性方面存在独特的挑战。
 - *Swarm DL vs. On-device DL*：在传统的设备端深度学习系统中，推理是主要功能，设备上的适应性很小或可以忽略不计，特别是当嵌入式设备是为特定的推理任务定制时。例如，有研究者提出了一个系统，该系统可以在256kb的内存限制下运行DL模型。然而，模型的这种压缩和修改被设备被动接受。相比之下，Swarm DL 中的每个智能体都表现出更高的主动性，参与设备上的 DL 推理和适应，其中专门用于适应的比例更高。因此，在这种新背景下，平衡深度学习推理和适应的资源分配成为一个新的挑战。
 - *Swarm DL vs. Distributed DL offloading*： 分布式深度学习卸载主要涉及自上而下的任务分区和卸载到多个设备，正如现有文献所强调的。Swarm DL强调设备之间集体行为的自下而上的出现。换言之，在Swarm DL中，每个智能体通过主动启动本地操作和调整，而不是集中分析来进行数据采集和处理，从而实现全局系统性能和资源效率的动态优化。
 - *Swarm DL vs. Federated Learning*：联邦学习（Federal Learning，FL）是一种数据处理范式。在给定输入数据的情况下，嵌入式设备上的联邦学习可以提高数据驱动的深度学习训练/适应效率。Swarm DL 专注于跨越数据采集和处理的联合优化。
 - *Swarm DL vs. Crowd Sensing*：群智感知将任务分配给众多用户，并使用它们贡献的数据来融合有关特定环境或情境的信息[8]。但是，它们没有从数据融合到任务分配阶段的进行及时反馈。此外，Swarm DL系统强调设备协作进行数据采集和处理，而群智感知仅依靠用户生成的数据进行集群数据采集。
 - *Swarm DL vs. Distributed multi-modal data fusion*： 分布式多模态数据融合主要是将来自不同感知源的数据进行融合，提高融合数据的整体质量，是一种多对一的单向数据融合模式。而swarm DL系统则主要关注每个设备的数据生成和融合的需求，采用多对多交互的双向聚合方案。

 ![Swarm DL 和相关概念的比较。](https://i-blog.csdnimg.cn/direct/f7e15634732349428570a0efa740df06.png#pic_center)

### 关键挑战

尽管先前工作对设备上的深度学习推理和自适应进行了广泛的研究，但将其扩展到包含数据采集和处理的**群体双向优化**仍存在两个**复杂性的挑战**：

 - 从数据采集和处理的**独立优化到双向优化**。它要求在对每个设备准确执行数据处理之前，对模态和样本中的数据重要性进行在线分析。它涉及在群体中动态整合实时数据。具体而言，现有的设备端数据重要性评估方法仅通过分布或熵比较来评估**显性影响**。它们无法处理**隐含的互补性**，受到分布式和动态因素的影响，如数据异步性、跨模态互信息可传递性以及相关的融合延迟成本。
 - 从被动数据处理到**主动数据采集和处理**。尽管之前在数据反应式设备端 DL 算法-系统协同设计方面做出了努力，但主动集群设备的优化范围需要改进。分散的约束，例如从部分信息和分布式资源进行处理，加剧了 *swarm DL* 的优化难度。此外，单个 IoT 设备之间的协作为 *swarm DL* 中的数据采集关联和计算优化带来了新的挑战。在分布式设置中，**数据采集**（生产者）和**数据处理**（消费者）的最佳匹配使优化范围进一步复杂化。

## 系统设计

### 系统概述

为了实现 *swarm DL* 的愿景，作者提出了一个通用的系统框架，名为 *DeepSwarm*（如图所示）。它与**异构 AIoT 硬件**（例如，CPU、GPU 或配备 MCU 的嵌入式设备）一起运行，适应**动态**应用环境（即，数据分布漂移和运行时资源可用性），并推广到各种 AIoT 应用（例如，移动健康、智能家居、自动驾驶汽车、工业自动化）。

*DeepSwarm* 采用模块化设计，将 *swarm DL* 的需求分解为两个功能模块：用于 DL 的主动集群数据采集和基于 DL 的主动 Swarm 数据处理。这两个模块与双向反馈协同工作，以优化**系统性能**（例如，准确性、延迟）和**资源效率**（能源效率、内存碎片）。下面我们简要说明两个模块的范围和特点：

 - *Proactive data acquisition module*：利用丰富传感器、资源受限的AIoT设备作为**智能体**，形成**自组织**集群，实现高效的数据采集，显著提升感知性能，并减少连接智能体之间的冗余信息。*DeepSwarm* 中的数据采集应自主选择和关联AIoT设备和传感器模式，并配置传感参数。例如，根据数据处理反馈，采样率以最小的开销（例如通信和能源成本）最大限度地提高融合数据质量。
 - *Proactive data processing module*：以深度学习任务的形式高效处理获取的数据，包括推理、训练和适应（微调、演化），以实现**自适应**和**自演化**的群体系统。*DeepSwarm* 中的数据处理预计将按需、实时地扩展，并具有高资源效率。
![DeepSwarm 图示，这是一个通用系统框架，用于实现 Swarm DL 的生物定向优化。](https://i-blog.csdnimg.cn/direct/34f60a3173c94bb9bfa187dd88eff2e4.png#pic_center)

### 模块功能

#### Proactive Swarm Data Acquisition Module

该模块从群体智能中汲取灵感，协调分布式设备和传感器的自组织。每个智能体通过分析从跨模态、跨任务和跨时钟传感器数据中提取的信息，积极参与数据重采样、感知参数调整以及与其他智能体的关联，旨在最大限度地提高数据融合质量并减少智能体数据冗余。此外，它旨在实现早期的**互补增强**，解决模态信息丢失、时钟异步和异构数据移位等挑战。前期是指数据生成、预处理、流出和处理的初始阶段。这样可以尽早降低后续的资源成本（例如，采样、计算、传输带宽）。

具体来说，我们强调同时评估数据在运行时对后续数据处理任务性能的**显性和隐性重要性**。

 - *Explicit data importance*： 可以使用数据/特征级信息比较和历史拟合等技术来实现分析。
 - *Implicit data importance* ：分析依赖于其在整个群体系统中数据采集阶段的互补性以及后续处理任务的特性。这包括异步特征解缠、生成和组合、慢数据重用、异构数据分布聚类以及时空数据重用。
 - 显性数据重要性估计是**数据驱动**的，已有丰富的研究成果。虽然隐含的数据互补性分析是**系统驱动**的，而且是不平凡的，需要全面考虑动态系统因素。我们指定了实现这种群体数据采集所必需的**三个主要要求**：

  1. **Automated Association of Heterogeneous, Asynchronous, and Asymmetric  Sensing Sources（异构、异步和不对称传感源的自动关联）**
     低功耗、数据丰富的传感器（如摄像机、麦克风、激光雷达和射频成像仪）的**分布式协作**，跨越不同的感知设备，促进了在复杂环境中的感知精度，如在角落、穿过墙壁、在微光下和树叶下的监测。为了优化资源受限的智能物联网感知设备的整体感知灵敏度和覆盖范围，采用**最小化数据信息冗余**的思想，并利用跨传感器不同模态间数据和设备的**早期关联性**，实现跨设备高效协同感知。
  2. **Context-adaptive Data Sampling（上下文自适应数据采样）**
     在众多智能体中，根据传感任务的动态性和多样性调整选定传感器的**采样策略**对于在没有数据冗余的情况下捕获必要信息至关重要。观察结果表明，只有**少数类别**对处理部分缺失的数据敏感。例如，在优化深度学习模型适应任务时，用于后向传播的主动样本识别策略应考虑**两个标准**：（1）识别可靠的适应样本和（2）确保非冗余，特别是跨模态和多任务。对于深度学习推理，分布式群传感器的占空比采样通过从长程依赖性角度预测全局信息融合后的潜在相关性来延长电池寿命。这涉及到本地执行的采样，然后在空闲期间关闭传感器，或者根据互补性和环境复杂性降低采样率。
  3. **Feedback-aware Data Acquisition（反馈感知数据采集）**
     自适应感知源关联和采样应根据数据处理的实时反馈，在不依赖全局数据知识或精确处理结果的情况下利用局部信息。这些配置必须快速调整以适应不断变化的传感器数据流和应用环境。实时性能估计反馈是优化数据采集流水线的关键。然而，在没有精确执行的情况下，验证这些策略对后续处理任务的适用性具有挑战性。一种方法，如在测试时自适应调整，涉及一个附加的“**再向前**”模块，它跟随向前和向后传递。其核心挑战在于准确、及时地预测数据采集性能，而无需**重新执行**整个数据处理阶段。

#### Proactive Swarm Data Processing Module

该模块包含数据处理任务，包括DL推理和自适应。传统的设备上深度学习系统主要专注于推理，很少有设备上的适配，特别是在为特定任务定制的嵌入式设备中。相比之下，*Swarm DL*智能体表现出**更高的主动性**，参与**推理**和**自适应**，甚至更强调自适应。因此，平衡深度学习推理和自适应的资源分配在这种背景下提出了一个新的挑战。具体来说，*swarm DL*的主要目标是以**自适应**和**自进化**的方式执行数据处理任务，类似于一般的群体智能。与专注于优化深度学习算法的方法不同，*DeepSwarm*还解决了资源竞争中的系统异步问题，代理之间不同的资源可用性，管理峰值内存使用，以及优化系统延迟和准确性之间的权衡。我们强调此模块的以下关键需求：

1.  **Self-adaptive DL Inference**
    为了在低资源预算和动态资源预算下实时处理传感器数据，必须自适应地**压缩**和**划分**深度学习推理工作负载，平衡精度和资源效率。需要创新地集成模型压缩、分区和卸载技术，以在算子、通道、分支和层级别上精细地向上/向下扩展深度学习推理工作负载。尽管深度学习模型的压缩或分割在算法上有了进步，但它们很难解决现实世界部署的动态性。识别和适应这些变化是至关重要的，因为不同的性能需求会受到时变的资源可用性、推理频率和来自其他应用程序的资源争用的影响。自适应深度学习推理过程必须操作免再训练和跨层跨越的深度学习模型、计算图、算子和内存分配，以匹配动态上下文。
2.  **Self-evolutionary DL Adaptation**
    在真实的AIoT应用中，**实时数据漂移**通常会挑战预训练深度学习模型建立的精度-资源效率的平衡。积极地从新数据中学习，并使用来自本地和边缘设备的有限本地计算资源自适应部署的深度学习模型的参数是至关重要的。为了最大化高精度深度学习推理时间在所有智能体整个生命周期（包括推理和适应时间）中的比例，需要一种高效的机制来支持资源有限的智能体处理深度学习适应任务。为了实现这一点，智能体必须在没有真实标签的情况下准确和快速地估计局部深度学习模型的精度下降，以控制再训练数据的大小并决定何时触发模型演化。同时，*DeepSwarm*还需要平衡设备之间有限的计算和内存资源，并以分散的方式解决不同设备发起的异步任务之间的竞争。此外，解决特定嵌入式SoC上的深度学习训练的算子支持问题也是至关重要的。

## 提高 DeepSwarm 性能的研究挑战和机遇

*DeepSwarm* 依赖于高度自动化和闭环的双向优化，强调环境、异构系统组件和设计堆栈之间的交互。如图所示，与专注于数据采集和处理单独优化的传统研究不同，这些组件的双向优化克服了性能限制，平衡了准确性和资源效率。通过共同优化群体数据采集和处理，可以准确收集和处理数据，最大限度地提高系统性能，同时最小化冗余和资源成本。在物联网场景中，每个智能体既是**主动数据生产者，又是消费者**，导致它们之间产生错综复杂的动态匹配关系。新的数据处理任务层出不穷，争夺集群设备的计算/内存资源，需要不断进行数据再分配，并调整深度学习模型结构和资源分配，以满足精度、时延、资源效率等多样化的应用需求。秉承这一**协同设计原则**，作者确定了以下挑战和机遇：
![DeepSwarm 中 swarm 数据采集和处理之间的生物定向优化循环图示。](https://i-blog.csdnimg.cn/direct/769b5f50f4ca478eb525c96be06189fd.png#pic_center)

### 自适应非阻塞深度学习推理

为了在推理精度和效率之间取得平衡，在数据采集和处理中增强互补性并最大限度地减少冗余至关重要。

#### 识别非冗余数据关联

为了确定最低限度的数据要求和非冗余的数据相关性，**常用的方法**涉及**统计分析**或距离度量，例如相关性、互信息、方差和相对重要性，以评估每种模态与目标变量之间的关系。然而，旨在确保预测精度的现有方法通常非常**耗时**，或者**依赖于完整的全局数据分布分析**。对于具有多个分布式设备的实时和去中心化物联网场景，进一步调整这些方法至关重要。在分布式 AIoT 场景中，不同的设备可能会带来异构数据进行非阻塞模型推理，此外，物联网场景中感知任务的动态性质增加了复杂性。具体而言，确定最低限度的数据要求需要考虑基于具体任务的不同模式的不同相关性。自适应方法对于动态调整任务依赖性是必要的。

针对这些挑战，作者提供了一些**见解**：

- 并非每个传感器数据样本都对后续模型处理精度有统一的贡献，对数据贡献进行细粒度的任务感知估计至关重要。
- 在深度学习训练任务中，错误处理不可靠的数据样本会对准确性产生负面影响。
- 在瞬息万变的感知环境中，数据传输中的滞后问题也会对计算精度造成干扰。具体来说，在异步分布式深度学习中，这种增加的数据过时性会导致深度学习模型更新期间出现更严重的参数错误。
- 排除不可靠的数据样本会留下潜在的冗余，建立一个旨在识别可靠和非冗余样本的主动样本选择标准是必要的，但也具有挑战性。
![使用异构数据进行自适应非阻塞 DL 推理的图示。](https://i-blog.csdnimg.cn/direct/b116ca1630454061bddb71132928b3ff.png#pic_center)

#### 运行时采样率适配

根据不同设备的**贡献**和**数据处理效率**调整每个传感器的采样率和开或关是一项艰巨的任务。这一挑战的出现是由于任务的动态性质以及传感器与不同活动的不同相关性，而每个传感器的贡献可能会根据本地的各种系统因素而波动，这一事实使其难度更加复杂。这进一步使得预先确定 **1-for-all** 采样率和用法变得令人望而却步，因此需要一种**实时自适应**方法 。然而，挑战在于目前的研究无法准确评估每个传感器的贡献，并根据不断变化的环境需求做出明智的运行时适应决策，确保**最佳**的平衡。不同场景和任务下的数据准确性与处理效率之间的关系。传感器噪声、异常值或意外事件等因素可能会给算法设计带来复杂性，因此需要在多样化和动态场景中表现良好的稳健解决方案。

此外，在涉及多个智能体和不同传感器的场景中，尽管进行了一些初步研究工作，但挑战在于实现**实时采样率适应的协调和协作**。目前的研究总是在探索数据自适应抽样与单一设备模型自适应之间的关系，缺乏一个**统一的框架**来指导它跨越协作的群体设备和多样化的任务。

#### 对不完整的数据流进行高效的深度学习推理

分布式多模态数据流的实时和精确处理对于各种 AIoT 应用至关重要。为了实现这一目标，研究能够使用来自不同设备的部分、延迟、不完整或缺失的数据流执行深度学习推理的**高效推理框架**至关重要。虽然分布式多模态传感数据有可能通过**立体多视角视图**提高感知准确性和覆盖范围，如在车辆网络和无人机集群中观察到的那样，它们协同感知小型、遮挡或弱光目标，但这些挑战在实际应用中很常见。这需要对以下几项关键技术进行探索：

- 估计和插补实时数据流的缺失值和不确定性，例如采用**生成模型**或插值技术，使模型能够在没有完整信息的情况下做出明智的预测。这使模型能够根据可用数据生成**推测性推断**，即使只有部分信息，也能做出准确的预测。然而，确定插补缺失的数据点是否能够保持底层模式的准确性，尤其是在没有标签的情况下，这是一个挑战。
- 将不确定性估计（例如概率模型或贝叶斯模型）集成到深度学习模型中，以**量化**与在不完整数据上做出的预测相关的不确定性。采用**自适应特征选择机制**，从完整数据中优先考虑和利用最有用的特征，优化融合过程。
- 开发用于准确同步和对齐多模态数据流的**预处理技术**对于准确融合和深度学习推理至关重要。然而，由于不同传感器或数据源之间的数据到达率、延迟和时钟同步不同，上述技术将面临挑战。此外，传感环境是动态的，数据流的特性可能会随着时间的推移而变化。构建能够持续适应动态条件的**自适应模型**对于异步数据流中推测推理的鲁棒性至关重要。
- 执行上述复杂计算，特别是在生成和预测模型的**轻量化**和**加速**实现中，对于具有资源受限移动设备的实时系统至关重要。

#### 动态弹性深度学习模型结构

*Swarm DL* 模型的**上下文感知规范**考虑了输入传感器数据、所需的应用程序性能结果以及可用硬件资源的约束。它对特定任务具有双重适应性，并且经过精心设计，对硬件资源友好。具体来说，推理、训练和适应任务中的情境感知 DL 模型应该是动态**可扩展的**、**可分割的**和**可组合的**。

- 深度学习模型（包括结构和参数大小）必须以不同的压缩程度进行**放大或缩小**，以满足动态资源约束（内存、计算和电池）和指定的性能要求（精度、延迟、能源成本）。设计不佳的深度学习模型可能会导致精度波动。
- 当前的**算法-系统协同设计**方法，它们缺乏基于运行时资源可用性的获取数据感知深度学习模型计算和系统部署的**协同优化**。去中心化的计算约束，特别是从部分信息进行计算，使协同设计的群体深度学习系统中的优化挑战进一步复杂化。此外，将运行时硬件资源可用性和系统执行反馈传播到数据处理算法设计仍然是一个具有挑战性的方面。 

### 测试时自我进化深度学习适应

为了在满足数据采集和处理资源限制的同时保持深度学习对非平稳数据漂移的准确性，有必要探索协同学习和自适应聚合以实现群体中的深度学习适应。具体问题包括：
![测试时 swarm DL 适应的图示](https://i-blog.csdnimg.cn/direct/f0a13322ee5446e3a48959e3b6a80cb8.png#pic_center)

#### 基于异构数据的*Swarm DL*自适应

为了实现高效且有效的群体深度学习适应，必须从数据和设备资源的角度考虑智能体的异构性。具体来说，对于每个需要聚合多源数据的设备，由于模态、大小和传输带宽的差异，传感器数据表现出异步性，从而引入了**异步数据流**。分布式多模态数据流的**异步特性**带来了挑战，导致系统延迟（如果等待慢速设备）或由于数据模态不足或缺失（如果不等待慢速数据）而导致准确性降低。此外，当每个智能体协作处理此类数据时，计算资源的多样性会导致快速和慢速设备之间的差异。**双系统异步**使精度和延迟之间的平衡变得复杂（等待慢速设备/数据会导致延迟，而丢弃慢速设备/数据可能会导致精度降低），因此需要对数据采集和数据处理进行协调优化。此外，传感器数据在不同智能体之间的分布异质性和不平衡性，包括非独立和同分布式（Non-IID），对实现群体深度学习系统的精度-时延平衡提出了更多挑战。为了应对这些挑战，一些有价值的系统性考虑因素为传统的深度学习推理、训练和自适应算法带来了特殊的挑战和创新机会。

利用深度学习适应中不同模态的互补性，特别是在面对异步实时传感器数据时，是一个很有前途的方向。具体而言，高质量传感器数据的**稀缺性**给单一传感器之间的互信息带来了瓶颈。多模态数据提供了更全面的对象表示，从而提高了模型的准确性和鲁棒性。因此，挖掘数据特征与目标任务之间的关联性，共享与模型下游任务最相关的数据，实现数据的互补和增强至关重要。此外，还需要研究细粒度的**融合策略**，这些策略可以有效地利用每种模式中存在的**独特信息**，而不仅仅是简单的串联或早期/晚期融合。

#### 知识增强的多任务协同自适应

作者探索了考虑不同任务和数据特征的协作群体深度学习自适应。集成**多任务深度学习框架**以在有限的本地数据和资源下提高系统性能是一个令人兴奋的方向。在不同的任务中，深度学习模型在训练过程中会产生各种**可转移的知识**，其中一部分可以增强其他模型对其目标任务的理解。这种可迁移的知识学习增强了模型的特征表示和语义理解，从而实现了高精度的深度学习模型训练。但是，这种优势仅限于与任务相关的方案。在任务差异明显的情况下，多任务学习将遭受**负迁移**和**跷跷板现象**的影响，使得准确性增益低于预期。因此，希望捕获任务依赖性、相似性和层次结构，以便在异步系统中实现有效的知识转移和任务之间的表示共享，而不是在固定的方案中。
![知识增强的多任务协同适应图示。](https://i-blog.csdnimg.cn/direct/6feabc8ba254454d83a15425440b05d0.png#pic_center)

#### 自适应系统资源调度

在模型自适应系统部署中，最大化运行时硬件能力不仅仅是算法。**中间结果重用和消除存储碎片**等做法对于提高性能限制至关重要。即使使用广泛使用的深度学习模型配置，将模型层/算子以不同的顺序映射到不同的底层资源也会导致不同的延迟和资源开销。因此，对计算图、算子并行性/融合性以及处理器之间的内存分配进行战略性优化，可以提高深度学习执行的运行时资源可用性。此外，群体系统中的**算法-系统协同设计**应有助于在算法层面迭代探索更灵活的深度学习模型设计空间，突破精度-资源权衡的界限，如图所示。

然而，尽管之前在针对单个嵌入式设备的算法-系统协同设计方面做出了努力，但网络化群体深度学习系统的优化范围仍需要重新定义。可能进一步研究的领域包括：

- 根据数据处理任务的特性（如张量/算子生命周期和依赖关系）定制系统调度，可以增强计算并行度，提高数据重用率，并减少群体数据处理过程中的内存碎片。我们注意到，与为不可预测的任务分配资源的传统操作系统不同，深度学习模型表现出相对**固定的**计算模式。在**计算依赖性**和**生命周期**方面，这种更强的可预测性使得细粒度优化更加可行。
- 虽然各个智能体可能会做出单独的资源池调度决策，但**全局性能评估**至关重要。
  此外，为了解决智能体之间的异构性，自动化框架对于自适应和自适应的群体深度学习系统至关重要。此框架涉及细粒度搜索空间、执行前性能**预测器**和**调度器**。然而，这些研究主要侧重于通过预测深度学习模型的部署成本来卸载计算任务，而没有考虑如何适应群体系统中的**动态上下文**变化。此外，由于缺乏统一的框架来部署和评估跨各种设备、异构 CPU/GPU/NPU/DSP 处理器和 DL 框架的 DL 模型的部署成本，这在比较和测量可选技术性能方面带来了挑战。需要对跨代理框架有更多的见解和努力。

在紧密联系和资源受限的群体中寻找合适的设备是必要的，但具有挑战性。我们观察到，数据处理任务只有在获得足够的内存资源时才能执行，并且随着计算资源的增加，其执行时间会减少。具体来说，可以从几个方面进行研究：

- 使用异构后端监控动态资源**可用性**并预测数据采集和深度学习任务的资源需求是棘手的。特别是，提供准确、及时的深度学习推理**性能估计**具有挑战性。
- 当多个任务同时运行时，设备之间将存在对**共享资源的竞争**。每个设备都可以通过确定何时为不同任务分配足够的内存资源来控制不同任务的调度时间。它需要根据任务的**紧迫性**、计算成本和培训时间进行合理的规划，为了最大限度地提高资源利用率，这需要对分配的资源与各种任务的延迟之间的关系进行全面分析。
- 用于多目标优化的运行时**优化器**，例如动态规划、强化学习或图形搜索，是一个基本的**NP难**问题，用于调整所有系统层（例如，算子顺序、内存分配）以实现最优的资源供需匹配。
- 精心设计的搜索空间对于解决多种数据处理需求之间的属性差异，提升**调度的搜索速度**至关重要。自适应地调度具有不同资源需求的所有异步任务，以使它们适应具有动态资源可用性的服务器并最大限度地提高整体性能也是 NP 困难的。选择任务组合可以有效减少搜索次数，从而提高速度。
  ![自适应系统资源调度的问题图示。](https://i-blog.csdnimg.cn/direct/8b33b1fea1c24b2fbd79003b924bdae3.png#pic_center)

### 异步和灵活的通信

在去中心化群体中，智能体之间的有效沟通在信息共享、协同感知、交换模型更新和协作决策中起着至关重要的作用。然而，分布式数据采集和去中心化数据处理环境在可扩展性和效率方面提出了挑战。特别是，在数据融合中，不同智能体之间的智能体间时间间隔将导致合并不准确，并影响后续感知任务的性能。我们将数据到达时间间隔定义为数据生产者生成到消费者到达消费者之间的时间。这段时间涉及传感器数据的预处理、传输和后处理，延迟了后续任务。因此，关键的机遇和挑战是调整这三个系统组件，以在**动态数据复杂性、本地资源可用性和通信带宽**下平衡计算成本和中间数据大小，以最小化整体时间差距。此外，有必要考虑异步和同步通信的灵活性，以平衡即时协调和准确性。

## 系统适用性分析

该论文通过两项初步研究展示了**移动端群体深度学习**的优势，包括：**群体深度学习自适应**和**群体联邦学习（FL）**。

### 群体深度学习自适应

如今的移动视频应用程序已经引起了广泛的关注。压缩的DL模型被广泛用于实现设备上的视频推理，然而，它很容易受到从动态变化的移动环境中捕获的实时视频的非平稳**数据漂移**的影响。为了对抗数据漂移，提出了一个**基于 DeepSwarm 框架的群体 DL 适应系统**，该系统使每个智能体能够使用从本地和其他智能体新收集的传感器数据持续更新，如图所示。多个智能体可以独立启动此深度学习适应任务。主要目标是最大限度地提高平均准确度，表示所有代理的高精度推理时间与总生命周期（包括推理、等待和重新训练时间）的比率。该系统由三个组成部分组成：**数据漂移感知视频帧采样**、**反馈感知DL自适应触发器**、**自适应DL自适应和资源调度**。

- **数据漂移感知视频帧采样**：作者采用了一种专用的帧采样策略，以数据漂移感知的方式处理各种数据漂移。对于突然或增量漂移，作者使用线性采样率来有效地选择视频帧，从而确保为适应深度学习模型提供大量数据。具体到渐变漂移，作者从帧差法开始，以消除冗余帧。随后，作者评估非冗余帧与数据分布的全局视图之间的距离，以预测每个帧的贡献，并为后续的深度学习适应任务选择最具代表性的帧。
- **反馈感知DL自适应触发器**：作者采用置信度评分，包括分类和定位置信度，以提高座席的处理准确性。此外，作者观察到，精度下降的开始并不总是深度学习适应的最佳触发时间点。为了识别触发时间点，我们开发了一个滑动窗口来测量精度下降率并监控数据漂移。具体来说，当下降超过预先设定的阈值时，开始适应，从旧的数据分布过渡到新的数据分布。然后，智能体评估置信度方差，以确定新的分布是否稳定，从而能够使用实时传感器数据进行更定制和有效的适应。
- **自适应DL自适应和资源调度**：构建了一个轻量级的预测网络。作者还开发了一个非负最小二乘求解器，用于对精度和训练时间之间的关系进行建模，以预测适应任务的精度增益。利用这些指标，作者采用动态编程算法来选择异步适配任务，并利用内存计算来加速适配，从而减少整体再训练延迟。该方案可有效处理矩阵乘法以生成伪标签。同时，作者优化了重新训练过程，以减轻电阻噪声对精度的影响。
- ![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/1ce2fff555ac4830b3c040a91f258c4f.png#pic_center)

### 实验结果

将该的系统与四种基线进行比较，即**域适应**、*没有来自其他代理的数据融合的 DeepSwarm*、**原始终端 DL 模型** 和 **单终端适应**。具体来说，领域适应是一种使用对抗性训练处理数据漂移的有效方法。没有其他智能体数据融合的DeepSwarm和单智能体适应基线都采用单一来源数据的知识蒸馏进行适应，但前者包括全局模型更新。在这个实验中，作者采用了三种类型的智能体和轻量级深度学习模型，即修剪的Faster-RCNNs，精度为0.441，0.315 和 0.437。使用这些智能体收集的视频，作者比较了重新训练的深度学习模型的准确性增益。下表表明，DeepSwarm 在准确度方面取得了最佳的整体性能，与移动模型的原始模型相比，平均准确率提高了 40% 以上，而全局模型的平均准确率提高了 9%。
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/21cf5803d29a4f5c94158df20ed9712f.png#pic_center)

### 群体联邦学习

作者进一步将 *DeepSwarm* 与物联网系统中的联合学习框架集成。联邦学习 （FL） 允许智能体上传 DL 模型，而不是传输数据以进行联合 DL 训练。然而，具有**异步传感器数据和异构代理资源**的真实移动系统对联邦学习提出了挑战。另一个挑战是**个性化**，因为移动代理在对传感数据和深度学习推理结果的偏见方面表现出显着差异。然而，现有的个性化联邦学习方法假设同步，这是不切实际的。因此，作者采用*DeepSwarm*在Swarm DL模型的异步个性化联邦学习中进行过期控制。*DeepSwarm* 由两个主要技术块组成：
**Data-aware Asynchronous Agent Association for Staleness Control**

- 对于实时代理聚类，DeepSwarm 采用了到达时的初始聚类关联机制。最初，聚类中心是使用服务器上到达的前几个模型参数设置的，一直持续到达到预定义的聚类数量阈值。然后，根据最小 L1 距离将代理分配到最近的集群。
- 为了控制由于集群中的异步代理而导致的模型陈旧，提出了将服务器新聚合的深度学习模型及时分发到集群内的代理。DeepSwarm 将个性化集群定义为广播范围。通过将广播限制到具有相似数据分布的集群内客户端，作者缩小了广播范围。广播频率是根据自上次广播以来的历史模型变化和下一次聚合之前的预测变化动态调整的。
  **Feedback-aware Dynamic Cluster Refinement**
  在整个联邦学习过程中，服务器会根据上传的反馈动态优化集群，以微调集群。集群细化涉及两个迭代步骤：扩展和合并。
- 服务器启动一个 clsuter 扩展过程，将代理分配给新的集群。为了防止在代理较少的新扩展集群中发生过拟合，中心模型中的大多数参数都被冻结，并且只有输出层被独占训练。冻结约束会逐渐解除，直到服务器触发集群合并。
- 当集群数量超过阈值时，将发生集群合并。对于数据分布相似的聚类，采用了基于细粒度动量的权重聚合方案，将进行迭代组合，直到聚类数量降至合并阈值以下。
  ![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/7739a0e8d2414abaae5ef216979483a1.png#pic_center)

### 实验结果

将 DeepSwarm 与 5 个 SOTA 基线进行了比较，包括标准 FL 方法 **FedAvg**、异步 FL 方法 **FedAsync**、半异步 FL 方法 **FedSelect** 和 **FedSEA**，以及个性化 FL 方法 **ClusterFL**。作者进行了实验来验证 DeepSwarm 在三个典型任务中的有效性，包括**图像分类 （IC）**、**人体活动识别 （HAR）** 和**声音检测 （SD）**。在这个实验中，作者利用了一个模拟环境，其中作者的模拟集群包括 20% 的 Jetson Nano、20% 的 Jetson NX Xavier、20% 的 Jetson Orin 和 40% 的 Raspberry Pi 4。对于 IC，作者将CIFAR10  分为 **120 个客户端**。对于HAR，作者将UCI-HAR 分开到 **30 个客户端**。对于 SD，作者将 Ubisound拆分为 **10 个客户端**。结果表明，DeepSwarm在收敛时间上**减少了88.2%**，在准确率上**提高了46%**。
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/b1f96cf4e9e04518a0a7e9189484bf01.png#pic_center)

## Citing DeepSwarm

If you find this repository useful, please consider giving a citation

```
@article{DeepSwarm,
author = {Sicong LIU, Bin GUO, Ziqi WANG, Lehao WANG, Zimu ZHOU, Xiaochen LI, Zhiwen YU},
title = {DeepSwarm: Towards Swarm Deep Learning with Bidirectional Optimization of Data Acquisition and Processing},
publisher = {Front. Comput. Sci.},
journal = {Frontiers of Computer Science},
url = {https://journal.hep.com.cn/fcs/EN/abstract/article_44024.shtml},
doi = {10.1007/s11704-024-40465-z}
}    
```
