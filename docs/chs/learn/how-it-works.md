# 工作原理

## 协议

Fluence协议构成了计算资源网络，并定义了执行计算的cloudless栈。

Fluence protocol forms the network of compute resources and defines the cloudless stack to execute computations.

<div style={{ textAlign: "center" }}>
  <img
    src="/img/fluence-functions.png"
    alt="Fluence network overview"
    style={{ display: "block", margin: "auto", maxWidth: "75%" }}
  />
  <p>Fluence网络概览</p>
</div>

### Cloudless函数, Aqua

Fluence网络完全运行在Aqua协议上，该协议提供了无需中心化协调的安全分布式执行。Aqua这个名字也用于一个特定领域的脚本语言，它被编译成 **pi-calculus(π-演算)** 操作，并允许表达无死锁的分布式算法。Aqua协议是免部署的：Aqua脚本被打包成数据包，并在网络中按脚本自身编程的方式执行。此外，Aqua保证了脚本执行的密码学安全性：所有请求及其逐步执行都由参与的Peer签名，使得执行的脚本可审计和可验证。

The Fluence network runs entirely on the Aqua protocol which provides secure distributed execution without centralized coordination. The Aqua name is also used for a domain specific scripting language that is compiled down to pi-calculus operations and allows the expression of deadlock-free distributed algorithms. The Aqua protocol is deploy-free: Aqua scripts are packaged into data packets and are executed as they go over the network as programmed by scripts themselves. Additionally, Aqua guarantees cryptographic security on script execution: all requests and their step by step execution are signed by participating peers, making executed scripts auditable and verifiable.

使用Aqua创建的代码我们称之为 **Cloudless 函数** ，因为它跨云、跨服务器、跨地理区域运行。Cloudless 函数为客户端应用程序和Fluence协议本身提供支持。服务发现、路由、负载均衡、子网初始化和操作、扩展和容错算法都是在Aqua上运行，并以Cloudless 函数的形式表达。

Code created with Aqua we call **Cloudless Functions**, because it runs cross-cloud, cross-server, and cross-geographies. Cloudless Functions power both customer applications and the Fluence protocol itself. Service discovery, routing, load balancing, subnets initiation and operation, scaling, and fault tolerance algorithms are all run over Aqua and expressed as Cloudless Functions.

### 计算函数，Marine, Marine

虽然Aqua操作服务器和云上的执行拓扑和流程，但对于在节点上运行计算，Fluence使用Marine，这是一个WebAssembly运行时，允许多模块执行，结合接口类型和WASI进行执行器访问。

While Aqua operates the topology and flow of the execution over servers and clouds, for running computation on nodes, Fluence uses Marine, a WebAssembly runtime allowing multi-module execution, incorporating interface-types and WASI for effector access.


Marine驱动计算函数，这些函数在单机内执行，类似于 serverless 云函数。Marine支持Rust和C++作为源语言，但随着WebAssembly标准的发展，更多的语言即将到来。

Marine powers **Compute Functions**, that are executed within single machine similarly to serverless cloud functions. Marine supports Rust and C++ as source languages, but more languages are coming with the development of the WebAssembly standard.

### 子网-Subnets

网络中的所有计算函数都通过副本化部署以确保容错性：在节点因硬件故障或网络中断而变得不可用的情况下。副本化部署称为子网。子网操作可以由开发者通过Cloudless函数完全自定义，因此开发者可以启用故障转移、负载均衡、共识或任何其他自定义算法。

All Compute Functions in the network are being deployed with replication to ensure fault tolerance: in the event a node becomes unavailable due to a hardware fault or network disruption. Replicated deployments are called Subnets. Subnet operation is fully customizable by developers via Cloudless Functions, so developers may enable failovers, load balancing, consensus, or any other custom algorithms.

子网在Fluence上启用了高可用数据存储的创建。可以将其视为热缓存或数据索引，而大量数据存储则外包给外部存储网络，无论是集中式（如S3）还是去中心化（如Filecoin/Arweave）。

Subnets enable creation of highly available data storage on Fluence. Think about hot cache or data indexing, while storing large amounts of data is outsourced to external storage networks, whether centralized (S3) or decentralized (Filecoin/Arweave).

### 计算相关的证明

Fluence协议强制为网络中的所有执行生成密码学证明。提供商为其计算生成证明，客户只为伴随证明的工作付费，证明工作已经过验证并且正确。

The Fluence protocol enforces generation of cryptographic proofs for all execution in the network. Providers generate proofs for their computation and customers pay only for the work accompanied by proofs that the work was validated and correct.

#### Aqua 安全性

当 Peer 在Fluence中运行时，它们不断支持传入的Cloudless函数调用，这反过来要求中继函数进一步或在该Peer上运行计算函数。对于每个传入的Cloudless函数，Peer验证之前涉及的Peer的执行跟踪，确保此流程的执行正确进行。由错误的Peer执行或受到干扰拓扑的Cloudless函数将被丢弃。

When peers operate in Fluence, they constantly serve incoming Cloudless Function calls that in its turn require relaying the function further or running a Compute Function on that peer. For every incoming Cloudless Function, the peer validates the execution trace of previous involved peers, ensuring that the execution of this flow happens correctly. Cloudless Functions executed by wrong peers or disturbed topology are discarded.

如果Cloudless函数要求Peer运行计算函数，Peer执行工作，扩展执行跟踪，并将请求进一步转发。这样，协议确保正确操作并为所有执行生成审计跟踪。

If a Cloudless Function demands the peer to run a Compute Function, the peer does the job, expands the execution trace, and forwards the request further as requested. This way, the protocol ensures the correct operation and produces audit trails for all executions.

#### 处理过程证明
协议强制对Aqua执行进行概率性链上验证。因为所有计算都被封装在Aqua中，这意味着平台上执行的所有内容都会概率性地在链上得到验证。提供商必须提交所需的执行以赚取奖励，否则将被削减。

The protocol enforces probabilistic validation on-chain for Aqua executions. Because all computations are wrapped into Aqua, it means that everything that is executed on the platform probabilisticly gets verified on-chain. Providers have to submit required executions in order to earn rewards or will be slashed.

#### 执行证明
Fluence的Marine WebAssembly运行时生成的特定代码执行的密码学证明。每次函数执行都伴随着这种证明，这些证明由参与后续执行的节点验证，并包含在处理证明中。

A cryptographic proof for particular code execution on Fluence. Every function execution is accompanied with this proof produced by Fluence’s Marine WebAssembly runtime. These proofs are validated by nodes participating in follow-on execution and included in Proof of Processing.


## 市场

链上市场将计算资源提供商与为资源付费的客户进行匹配。市场完全无需许可，因此任何提供商都可以参与并发布其可用的资源容量。

On-chain marketplace matches compute providers with customers who pay for using the compute resources offered by providers. The marketplace is completely permissionless, so any providers may participate and publish their available capacity.

市场托管在由IPC驱动的Fluence自有链上，，由Fluence计算提供商验证，并锚定在Filecoin L1上。自有链使得廉价和快速的交易成为可能，以支持任何规模的计算资源租赁：从微小负载到大规模。

The marketplace is hosted on Fluence's own chain powered by IPC, validated by Fluence Compute Providers and anchored to Filecoin L1. The own chain enables cheap and fast transactions to enable renting compute resources at any scale: from tiny loads to massive scale.

<div style={{ textAlign: "center" }}>
  <img
    src="/img/marketplace-providers.png"
    alt="Compute providers on the Fluence marketplace"
    style={{ display: "block", margin: "auto", maxWidth: "75%" }}
  />
  <p>Fluence市场上的计算提供商资源</p>
</div>

<div style={{ textAlign: "center" }}>
  <img
    src="/img/marketplace-provider-resources.png"
    alt="Compute provider resources"
    style={{ display: "block", margin: "auto", maxWidth: "75%" }}
  />
  <p>Compute provider resources</p>
</div>

### 容量证明
Fluence通过强制执行称为容量证明的密码学证明，确保提供商广告的资源存在且可用。提供商将其硬件资源应用于不断生成容量证明，以确认这些资源已准备好为客户服务。协议按分配的功率比例奖励此类资源Fluence代币。

Fluence ensures that resources advertized by providers exist and available by enforcing a cryptographic proof called Proof of Capacity. Providers apply their hardware resources to constantly generate Proofs of Capacity to confirm that these resources are ready to serve customers. Protocol rewards such resources with Fluence token proportionally to the allocated power.

每当客户需要来自选定提供商的计算能力时，这些资源就从生成证明切换到为客户的应用程序服务。

Whenever customers need computing power from chosen providers, these resources are switched from generating proofs to serving customers' application.

<div style={{ textAlign: "center" }}>
  <img
    src="/img/marketplace-capacity.png"
    alt="Compute units submitting Proofs of Capacity"
    style={{ display: "block", margin: "auto", maxWidth: "75%" }}
  />
  <p>Compute units submitting Proofs of Capacity</p>
</div>

### 资源定价

客户可以根据提广告的价格和其他参数选择提供商，或者结合最高限价发布工作，由任何提供商接单。

Customers may select providers by price advertised and other parameters, or alternatively publish work and required max price to be picked up by any provider.

在底层，对于每个应用程序部署，都会在客户和提供商列表之间创建一个链上交易。交易记录财务细节（价格、预付款和提供商所需的抵押品）、与所需服务相关的技术要求（访问某些数据、二进制文件或Web API）以及网络中代码安装的链接。

Under-the-hood, for every application deployment, a Deal is being created on-chain between a customer and list of providers. Deals record financial detail (prices, pre-payment, and required collaterals from providers), technical requirements related to required services (access to certain data, binaries or web API), and a link to code installations in the network.

<div style={{ textAlign: "center" }}>
  <img
    src="/img/marketplace-matching.png"
    alt="Matching criteria for selecting providers"
    style={{ display: "block", margin: "auto", maxWidth: "75%" }}
  />
  <p>Matching criteria for selecting providers</p>
</div>

### 计价模型

最初，计费模式是预付费的，基于资源租赁时间和所需epoch。最小资源租赁是一个包含2个epoch的**计算单位**，其中epoch定义为1天，计算单位是1个Core、4GB内存、5GB虚拟磁盘空间。客户需要预付最小期限的费用，以确保提供商得到工作的报酬。

Initially, the billing model is pre-paid, based on time of resource rental and accounted in epochs. Minimal resource rental is a single **Compute Unit** for 2 epochs, where one epoch is defined as 1 day, and Compute Unit is 1 core, 4GB memory, 5GB virtual disk space. Pre-payment for minimal period is required from the customer so providers are ensured of getting paid for work.

按需的计费模式和**弹性计算单位**将在项目的后续阶段引入。

The request-based billing model, and **Elastic Compute Units** will be introduced in next stages of the project.

### 网络

可以将Fluence网络视为一组内部互联的节点，每个节点都运行AquaVM和Marine，能够接收命令在本地部署和执行代码，并根据接收的Cloudless函数与其他节点协作。这些节点中的大多数不断参与经济活动：它们监控并进入交易，形成新的子网或调整在子网中的参与，根据交易指定安装应用程序，协调执行并支持传入的请求。它们还生成执行证明，并按照证明算法的规定提交它们以接收奖励。

The Fluence network can be thought of as a global set of interconnected nodes, each of which runs AquaVM and Marine, capable of receiving commands for deploying and executing code locally and collaborating with other nodes as specified by the received Cloudless Function. Most of these nodes are constantly involved in economic activity: they monitor and enter into Deals, form new Subnets or adjust participation in Subnets, install applications as specified by Deals, coordinate execution and serve incoming requests. They also produce proofs of the execution and submit them as specified by proof algorithms to receive rewards.
