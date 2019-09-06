# 纳什合约网络白皮书 V0.1

**2019年9月1日**

**摘要:**

- [背景](#背景)
- [思路](#思路)
- [技术方案](#技术方案)

# 背景

2013年底，比特币突破1000美元关口。这不仅证明了对等电子支付网络的技术可行性，更是在社会学意义上，人类第一次实现了大规模对等网络协作。

2008年，中本聪（Satoshi Nakamoto）在[《比特币：一种对等网络电子现金系统》](https://bitcoin.org/bitcoin.pdf)中提出“区块链”概念。2009年，中本聪发布比特币网络客户端第一个版本，并开发出第一个区块，即[“创世区块”](https://www.blockchain.com/btc/block-height/0)。比特币的成功发布开创了一个全新的领域，点对点的分布式网络架构激发了人们对于去中心化世界的无穷想象。

维塔利克·布特林（Vitalik Buterin）撰写第一版[以太坊白皮书](https://blog.ethereum.org/2014/01/23/ethereum-now-going-public/),尝试通过智能合约将去中心化的应用场景从单一的电子货币扩展到通用应用领域。2014年，[以太坊通过ICO融资](https://github.com/ethereum/ethereum-org/blob/master/public/pdf/TermsAndConditionsOfTheEthereumGenesisSale.pdf)获取巨大成功，成为目前（至2019年9月1日）历史上最大金额的ICO项目。

从此之后，比特币的暴涨暴跌带来加密货币的热潮与投机疯狂。借力ICO，创业者们开始试图用“去中心化的场景”来重构和解决当今时代的生活、商业、社会甚至国家存在的各种问题，人们的想象力也扩展到了几乎无所不在的程度。

实现这些“去中心化的场景”通常需要P2P网络技术、加密技术、时间戳技术和区块链技术等一系列技术手段。为了沟通方便，人们往往把这些技术集合简称为“区块链”。目前，“区块链”相关的技术进步、商业模型和社会意义还处在探索之中。除了少数大企业在谨慎的试探之外，区块链技术并没有真正介入企业市场和个人生活。

经过大量的行业调研和长时间的技术研究，我们认为：从技术层面讲，“区块链”能够真正落地并大规模应用的关键是最大范围共通且扎实可靠的信任根基。只有构建在这个信任根基之上的区块链服务才有可能承载类似现有互联网规模的应用场景，眼前行业聚焦的交易量、共识速度等具体指标重要但并不关键。

首先，目前所有区块链项目的根本缺陷都是假设上链数据的可信。但实际上区块链系统最大的不确定性来自人。人们为了利益在数据获取源头甚至计算执行过程中篡改数据是无法监督的。只有保证上链数据的可信性，才能从根本上解决区块链项目的可信性问题。

其次，在工程角度上，目前区块链技术的单一全局共识机制本身约束了系统所能承载的容量天花板。一方面，单一的统一共识算法决定了极少数出块节点成了容量的瓶颈。另一方面，现有的区块链项目依赖算法信任，这种全局信任的成本无法满足大量小成本标的的交易场景。

# 思路

那么这个最大范围的信任根基是否存在？它究竟是什么？

我们回过头来看比特币，比特币最神奇地方在于只依靠非对称加密、工作量证明、P2P网络以及链式块存储技术解决了点对点之间的信任传递问题。比特币并没有重新发明或者定义某种算法就建立了一个最小化的信任根基，那么在比特币之后涌现的一系列技术是否存在可能将这个信任根放大，大到足以承载整个互联网的可能？也就是说，我们能够在互连网层级的规模上解决去中心化的信任，同时必须适应业务场景的无限复杂性。

目前看来，任何单一的技术都无法达到这个目标。如果要达到这个目标，就需要一系列的技术集合。当代计算机都遵循冯·诺伊曼结构，将整个系统分为输入输出（IO）、计算（运算器与控制器）、存储三个部分。多数区块链技术通过点对点分布式存储、非对称加密以及链式块存储满足存储可信，但IO与计算都只限定了特定类型来解决可信问题。单纯的算法无法解决任意数据类型的IO以及计算也是多数区块链存在的问题。要实现最大范围的信任根，我们需要解决IO、计算以及存储的可信问题。同时，实体（人、组织、甚至AI等）作为最重要的IO源之一，同样需要纳入信任范围。

![John_von_Neumann_arch](Design/John_von_Neumann_zh.jpg)

因此我们提出了信任空间的概念：信任空间被认为是网络空间的一个子集，网络空间当中的信息如果具有确定性，那么我们认为信息是在信任空间当中。信任空间的信息确定性我们定义如下：产生信息的主体(who)和环境（where）可以追溯到确定的信任根，产生信息的时间(when)确定，信息的内容(what)唯一。因此结合冯·诺伊曼结构之后，要实现信任空间至少需要满足以下四个条件：
1. 身份自主可信
2. 计算过程可信
3. 数据存储可信
4. 输入输出可信

身份自主可信是解决数字世界参与者的权利边界问题，计算过程可信是解决协作和交易过程的确定性预期，数据存储可信是解决数据的不可篡改，输入输出可信则是定义信任空间的边界。其中基于1与3可以确保用户对任何类型的数据声明其对数据拥有的权利，并可以将这种权利选择性的分享、出售或让渡给其它人。而2与4则确保用户在使用数据时不侵犯他人的权利。

身份自主可信需要满足以下条件：
1. 用户自主选择信任根
2. 用户自主控制主密钥对的生成与保存
3. 用户使用密钥需要有对应的认证手段，例如密钥、指纹甚至活体识别
4. 用户可以通过匿名与信任根的零知识证明保护自身隐私

作为身份自主可信的实现方案之一，分布式身份（Decentralized ID）目前已经作为草案提交了W3C（参见[这里](https://w3c-ccg.github.io/did-spec/)）同时基于DID也已经有了大量实现，例如　Indy、Sidetree等。作为分布式身份的主流标准之一，用户可以选择自主选择身份信任根（例如身份证、护照、学校提供的在读证明、公司提供的工作证明等），可以选择匿名模式，从而避免个人数据完全被厂商控制或者隐私泄漏的风险。当用户使用匿名模式，而应用场景要求用户证明自己的某个属性时（例如年龄、工作单位、所在地等），DID规范可以帮助人们通过身份信任根实现零知识属性证明。

我们允许用户通过DID实名或者匿名的声明他对数据的所有权、商用权、二次加工权等一系列权利，同时将内容与权利声明加密存储在点对点的分布式文件系统当中，例如IPFS。文件加密确保只有拥有密钥的用户可以读取对应内容，点对点分布式文件系统则保证内容能够以安全且快速的方式在网络上传播，提供给更多用户使用。点对点的分布式存储缺乏时间属性，这在更为严肃一些的场合会造成不可预知的问题，因此对于重要数据（例如对全网公开的数据、声明以及合约等）需要保存一份存证在一个由全局投票选拔出来的若干节点组成的联盟链当中。对于非重要数据（例如私有的数据、声明及合约等），我们认为无需进行全局共识。因此，数据存储可信需要满足以下条件：
1. 数据归属权明确不可篡改
2. 数据内容不可泄漏
3. 存储自身具备鲁棒性
4. 私有内容传播受限
5. 公开内容的声明需要全局存证

如果只是权利声明而没有实质性的保护，那么和现有互联网对于权利保护只能走法律途径没有不同，无法把维权成本大幅降低。要做到实质性的保护，我们需要将硬件级的信任根植入到操作系统当中，实现计算过程可信。信任空间当中的可信执行环境应当满足以下条件：
1. 应用运行在独立且尽可能隔离的环境当中
2. 操作系统限制应用程序对文件与网络的访问和修改，保护所有者对于内容的权利声明边界
3. 操作系统应当假设自身所处的环境是不可信的，防止修改、窥探、侧信道等攻击行为
4. 操作系统以及应用软件的来源只有两种：一是信任空间内私人共享，二是通过安全检测及审核之后的公开镜像库
5. 硬件应能够提供关键软件（包括但不限于密钥计算、权限控制、智能合约等）运行在保护范围当中的证明，并能够进行远程验证

幸运的是，现代CPU普遍提供了可信执行环境，例如[Intel SGX](https://software.intel.com/en-us/sgx)、[AMD SEV](https://developer.amd.com/sev/)、[ARM Trustzone](https://developer.arm.com/ip-products/security-ip/trustzone)等，并提供了高度隔离的虚拟化容器，例如[Kata-containers](https://katacontainers.io)，可以让应用同时享受容器化的便利以及虚拟化的安全。在可信执行环境中，我们可以安全的存储和计算用户的私钥，并执行用户的内容、声明与合约。通过将操作系统的文件及网络接口逻辑处理放在可信环境中执行，可以让用户对于内容的使用限制在所有者声明范围之内，最大化的保护内容所有者的权益。而操作系统级的接口管理带来一个额外的好处，就是运行在操作系统上的应用几乎无需任何修改及适配就能运行在区块链的环境之中，也就是说，由应用创建的任何数据天生就是链上数据，通过可信DID身份以及可信软硬件环境，链上数据天生就具有可信属性。

这也就意味着现有PC生产力环境输出的任何类型的数字内容，包括代码、程序、照片、CG、音乐、视频等，天生就在信任空间当中。这些多种类的数字内容在输入输出的环节同样应当确保在信任空间当中。信任空间的IO同样需要满足以下条件：
1. 输入终端设备自身需要对产生的内容记录可验证的签名
2. 输入输出过程需要确保内容不被泄漏或者篡改
3. 所有输入输出的具体行为都绑定实体的具体身份（DID）

网络传输环节的解决方案已经非常成熟（TLS/SSL等）。输入输出终端可信的解决方案目前并不多，例如数字版权管理(DRM，Digital rights management)等。但我们将这个视为产业升级的机会，能够通过IoT等更低成本的方式将内容保护真正普惠到每一个创作者。

信任空间中的多样化数字内容，在结合合适的智能合约形式之后，有可能激发新的生产力。现有的智能合约形式都是基于代码的形式，对于开发人员来说学习成本并不高，但是对于其它职业的创作者，如作者、记者、摄像师、导演、绘画师、音乐家、艺术家等如果要参与到合作当中来，重新学习智能合约的开发语言则会导致整个系统门槛太高。为了能让大多数人都能参与进来，智能合约需要以自然语言的形式表达，同时能够无歧义的翻译成多种语言。通过智能合约之间相互引用的特性，用户可以很容易的形成针对特定内容二次开发、代理销售等协作方式。同时数字内容的边际成本为零的特性，有可能让有限的利润进行几乎无限的分配，从而让生产过程中所有的人都能够从中获益。同时，信任空间提供的可追溯属性，让工作量按件、按量、按时等计费方式得以可靠实现，使实时动态的按劳分配有可能成为智能合约的重要属性之一。

# 技术方案

如何构建一个信任空间呢？

从之前的描述来看，一个信任空间的建立从严格意义上要将密码学应用到从底层硬件、操作系统、应用软件等一系列的环节当中。在这些重构当中，我们认为最核心的在于网络计算机之间交换信息前的验证协议，也被称之为“信任握手”。不同于TCP协议的三次握手，“信任握手”构建在协议层之上。在建立加密通讯通道之后，负责交换双方的软硬件环境信息以及用户信息，如下图所示。“信任握手”主要包含的内容有：1. 用户的可验证DID；2. 硬件加载软件时生成的度量信息、运行环境信息以及软件DID；3. 硬件的DID以及硬件对1与2信息的数字签名；4. 请求的具体内容。

![TrustHandshake_ZH](Design/TrustHandshake_ZH.jpg)

其中1主要用于提供身份信息以及远程证明方式，对于某些特定类型的内容请求，响应方可以要求请求发起方提供更具体的身份信息证明，例如年龄、国籍等，避免信息传播到不适当的领域，同时请求方提供的远程证明方式也应当被响应方认可，如果响应方不认可请求方提供的远程证明方式，或者请求方提供的身份信息不符合要求，响应方可以拒绝服务；2主要是提供硬件认证过的程序加载信息，避免软件伪造自身版本，确保运行的代码正确性，响应方需要对请求方的软件版本进行验证（直接判断或者经过第三方）以决定对方的软件环境是否安全，是否符合自身的运行需求，如果不符合，则可以要求请求方通过符合要求的版本；3确定硬件的身份和对应的版本，并通过第三方对签名信息进行验证，确保签名内容是由指定版本的硬件产生，而非通过软件模拟；只有通过这三点的确认，才能迅速建立双方信任，确保请求内容交给对方之后，自身的利益不会受损。

负责发起握手、校验握手的程序，我们称之为“权利代理”，该程序实质上是代理行使他人权利，确保用户使用内容是在他人权利声明范围之内进行，同时也保护用户不受不符合自身要求的内容的侵扰。这个程序的形式是多样化的，可以是内核模块、独立程序甚至是浏览器插件，但无论它是以什么形式存在，都应当是用户访问这些内容的唯一入口，以及生成数据的唯一出口。权利代理应当完全遵守数据所有者通过智能合约表达的意愿，例如是否允许导出到信任空间之外（拷贝、复制粘贴、打印等），是否允许在数字内容上进行再创作等，是否允许保存在本地等等。

权利代理在运行时应当感知自身的软硬件运行环境，并对运行环境提出要求，例如硬件级别的加密支持、内存隔离、内存加密、安全运行验证等。也就是软硬件环境原理上来说能够提供的证明越多安全级别越高，同时验证渠道并不限于通过第三方网站验证、或者基于记录在公开的分布式账本上的公钥进行验证等。也许有人觉得这些运行环境和条件证明过于繁琐，在90年代初期互联网刚对公众开放时，用户为了交流信息同样需要购买安装调试对应的软硬件；信任空间交流的不只是信息，还有信任，而信任的传递同样依赖于软硬件的组合。

作为信任空间的基础设施之一，权利代理程序应当是自由开源且由社区共同开发的，并且允许任何人开发权利代理程序。对应的版本经由社区技术委员会讨论之后建立互信机制。对于权利代理程序的要求就是不能是闭源，且不应当阻止用户选择自己认为适合的权利代理程序。

围绕权利代理程序，信任空间的基础设施还应当包含如下：
* 合约语言 灵犀 Telepathy

Telepathy 作为一种类自然语言的编程语言，可以视为信任空间内一种法律的DSL（Domain-Specific Language），无需实现图灵完备，同时可以自动执行。Telepathy 的组成要素与一般合同并无二致，包括引用、定义、条款三要素。引用包含两种，一种是合约引用，一种是条款引用；合约引用将会直接链接到其它合约，并执行其中的指定条款；而条款引用则是引用合约内部条款，通过条款的共同作用达到目的。定义一般是指定签约方以及合约的操作对象，签约方可以指定（双方或者多方合约）也可以不指定（使用声明）；操作对象包含加密货币、文件、文件内容甚至计数、统计等任何可以通过扩展手段采集的结构化数据。条款则是定义条件判断以及执行内容。Telepathy 应当有专用的编辑器以及运行环境；专用编辑器不但方便用户编写，同时方便用户对合约条款进行演算，判断己方利益以及检查条款冲突；而运行环境则会安全执行合约，同时将所有操作打包为一个交易，只有交易整体成功提交才能最终执行。Telepathy运行在权利代理或者联盟存证链当中，通过功能插件与支付插件的接口对外操作，合约一旦生成，外部除了触发合约执行和展示合约内容以外不能改变合约运行内容或条件；功能插件主要是执行采集、计数、统计等功能的外部实现，通常建议以动态链接库的方式与合约集成，功能对于插件的入参与出参类型有严格的限制，同时应当对于任何类型的参数输入都能正常处理，不能轻易终止处理或者崩溃；对于支付插件来说，主要用于对接各种支持点对点支付的电子货币，并负责各类电子货币之间的实时兑换，确保用户购买时支付的资金能够正确的转入到卖方账户中。

* 分布式文件系统 Decentralized Filesystem

DFS主要承担内容保存及分发的功能，DFS分布在整个平台所有参与者之中，DFS之中分为两种角色，一种是用户节点，用户可以在本地保存自己的内容，以及自己经常访问或希望收藏的内容；另一种是备份/分发节点，负责数字内容的备份与分发；默认情况下若干备份/分发节点组建一个集群，而整个平台当中有若干集群存在，每一个集群都由一个运营方维护，每个用户可以选择至少一个运营方作为自己的备份/分发节点；而备份/分发节点通过为用户内容的服务，根据容量或者流量从用户的内容收入当中收取一定的费用。DFS存储的内容主要包括：用户私有数据、用户公开数据、应用程序日志、公开应用程序镜像库、私有应用程序镜像库、存证数据、合约交易等。运营方可以选择拒绝为某位或者某类用户服务，但是不能在服务期间删除或者丢失用户数据。

* 联盟存证链 Consortium Blockchain of Evidence

CBE主要承担身份、声明、合约与交易的存证以及查询；CBE当中具有写入权限的成员是由社区投票选举出来进行记账，同时也是平台规则的讨论与制定者，代表社区成员发表意见；联盟的最终决议将以全局合约的形式存储在平台当中；考虑到联盟链负载较高，联盟链的共识算法将会采用允许高并发的共识算法，例如PBFT或改进型BFT进行全局共识；共识记账接受全局监督，记账结果记录在DFS当中以便随时查阅。
