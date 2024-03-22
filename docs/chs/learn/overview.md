import ReactPlayer from "react-player";

# 概览

## Fluence是什么

Fluence是一个由区块链经济驱动的、去中心化的serverless平台和计算平台。它是一个全球性的、无需许可的、可扩展的、安全的替代传统云计算平台的解决方案。我们称Fluence为 **Cloudless平台**，因为它实现了无需云服务器的serverless。

通过Fluence，开发者可以构建并部署应用程序到一个计算资源供应方网络，这些供应方涵盖范围包括专业数据中心，家用电脑等。供应方在价格和性能上进行竞争，为了得到报酬和赚取奖励，他们不断证明自己正在服务应用程序。

Using Fluence, developers build and deploy applications to a network of compute providers, where providers can range from professional data centers to home computers. Providers compete on price and performance and, to be paid and earn rewards, they constantly prove that they are serving applications.

Fluence由一个加密token驱动，供应方使用这种token作为参与的抵押品和货币激励。供应方通过服务应用程序赚取Fluence-Token和支付（通常是稳定币）。

Fluence is powered by a cryptographic token which is used by providers as collateral for participation and as a monetary incentive. Providers earn both the Fluence token and payment (usually stablecoin) for serving applications.

<ReactPlayer controls url="https://youtu.be/JrWw-0CZDaU" width="100%"/>

## 对于开发者

开发者可以使用Fluence构建和部署应用程序、后端、API和其他数字服务。Fluence的无服务器平台提供了类似于传统无服务器云的开发者体验，但额外允许开发者在分布式网络上管理应用程序的执行；选择供应方并随时切换他们。

Developers can use Fluence to build and deploy applications, backends, APIs, and other digital services. Fluence’s serverless platform provides a developer experience similar to the traditional serverless cloud but additionally allows developers to manage an application’s execution over the distributed network; choose providers and switch them at will.

与云平台不同，当使用Fluence时，开发者可以通过检查供应方在链上发布的证明来验证他们的应用程序是否按预期服务，计算是否正确执行。

Unlike on cloud platforms, when using Fluence, developers may verify that their applications are served as intended and computations executed correctly by checking proofs posted by providers on-chain.

Fluence整合了Web2和Web3数据存储和管理平台，为应用程序执行提供数据输入和输出。虽然Fluence不是为大规模数据持久化而设计的，但它非常适合数据缓存、索引、处理和查询。

Fluence integrates both Web2 and Web3 data storage and management platforms to plug data inputs and outputs for application execution. While Fluence isn’t designed for large scale data persistence, it perfectly fits for data caching, indexing, processing, and querying.

|                       |                   Fluence 组件                   |             Web 2 平替            |
|-----------------------|:-----------------------------------------------------:|:------------------------------------:|
| Cloud Functions[云函数]       | Compute Functions, Marine                             | AWS Lambda, Google Cloud Functions   |
| Distributed Workflows[分布式工作流] | Cloudless Functions, Aqua                             | AWS Step functions, Google Workflows |
| Cloud services[云服务]        | Aqua libraries                                        | Route53, ELB, Consul                 |
| Data services[数据服务]         | Subnets                                               | S3, RDS, DynamoDB, MongoDB           |

## 对于计算资源供应方

计算资源供应方通过在市场上租赁其容量来获得奖励。

Compute providers earn rewards for offering their capacity for rent on the marketplace.

供应方可以提供任何连接到网络的设备出租，包括专业设备或数据中心，甚至是个人计算设备（甚至是笔记本电脑或树莓派）。成为供应方很容易：不需要建立复杂的容错设置；这个可靠性由协议提供。然而，性能取决于供应方的硬件和互联网连接，因此专业服务器硬件在大多数情况下很可能会受到客户的青睐。

Providers can offer for rent any device connected to a network including a professional rig or data center or even a personal computing device (even a laptop or raspberry pi). It is easy to become a provider: it is not required to establish complex setups for fault tolerance. Instead, reliability is provided by the protocol. Performance though depends on the provider's hardware and internet connection, so professional server hardware would most likely be favored by customers in most cases.

供应方的收入来自两个方面。开发者支付给供应方，因为它们支撑app运行。协议还会奖励供应方Fluence-Token，因供应方提供计算能力及支撑网络连接，并有助于提高网络性能和延迟。

Provider revenue comes from two main sources. Developers pay to providers for useful work: serving applications. The protocol additionally rewards providers with Fluence token for keeping compute capacity connected to the network and contributing to improving network performance and latency.

供应方也不需要特别宣传他们的服务，因为市场会自动将他们与相关的客户连接起来。

Providers also don’t need to specifically advertise their services as the marketplace connects them to customers interested in their services.


## 对于社区

Fluence的计算安全模型由加密经济激励机制驱动。Fluence-Token持有者可以为计算硬件质押，以支持证明硬件在网络中的可用性并正确执行计算任务。为此，协议会奖励质押者额外的token。

Fluence's compute security model is powered by cryptoeconomic incentives. Fluence token holders may stake for compute hardware to support the attestation that the hardware is available on the network and performs compute jobs correctly. For this, the protocol rewards stakers with additional tokens.

Fluence由数字治理（DAO）管理，因此token持有者可以参与治理过程：创建提案，选择代表和治理委员会，并对提案进行投票。

Fluence is managed by digital governance (DAO), so token holders may participate in governance process: create proposals, choose delegators and governance committee, and vote for proposals.
