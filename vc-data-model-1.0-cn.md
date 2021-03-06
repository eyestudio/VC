# 可验证凭证数据模型1.0

原文地址：https://w3c.github.io/vc-data-model

[toc]

## 1、 介绍

本节是非规范性的。

证件是我们日常生活的一部分；驾照被用来证明我们有能力驾驶机动车，大学学位可以用来证明我们的教育水平，政府颁发的护照使我们能够在国家之间旅行。这些证书在物理世界中使用时为我们带来了好处，但在网络上的使用仍然难以实现。

目前，在网络上很难表达教育学历、医疗数据、金融账户详情以及其他各种第三方验证的机器可读的个人信息。在网络上表达数字证书的困难，使得通过网络获得与物理证书在物理世界中为我们提供的同样的利益成为一种挑战。

本规范提供了一种标准的方式，在网络上以一种加密安全、尊重隐私和机器可验证的方式来表达凭证。

对于那些不熟悉可验证凭证相关概念的人来说，下面的章节将提供以下概述。

- 构成可验证凭证的组成部分
- 构成可验证展示的组成部分
- 一个生态系统，在这个系统中，可验证凭证和可验证展示有望成为有用的东西。
- 本规范所依据的用例和要求；

### 1.1 什么是可验证凭证？

本节是非规范性的。

在物理世界中，一份证书可能包括：

- 与识别全权证书主体有关的信息（例如，照片、姓名或身份证号码）。
- 与发证机关有关的信息（例如，市政府、国家机构或认证机构）。
- 与该证件类型有关的信息（例如，荷兰护照、美国驾照或健康保险卡）。
- 发证机关宣称的有关主体的具体属性或特性的信息(例如，国籍、有权驾驶的车辆类别或出生日期)
  与证书如何产生有关的证据；
- 与凭证上的限制条件有关的信息(例如，失效日期或使用条款)。

可验证凭证可以代表实物凭证所代表的所有相同信息。数字签名等技术的加入，使可验证凭证比实物凭证更不易被篡改，更值得信赖。

可验证凭证的持有人可以生成可验证展示，然后将这些可验证展示分享给核验人，以证明自己拥有具有一定特征的可验证凭证。

可验证凭证和可验证展示都可以快速传输，在试图远距离建立信任时，比物理对应物更方便。

虽然本规范试图提高数字凭证表达的便捷性，但它也试图平衡这一目标与一些隐私保护目标。数字信息的持久性，以及不同来源的数字数据很容易被收集和关联起来，这构成了一个隐私问题，而使用可验证的和容易被机器读取的凭证有可能使这个问题变得更糟。本文件在第7节中概述并试图解决其中的一些问题。隐私方面的考虑。本文档中还提供了如何使用隐私增强技术（如零知识证明）使用该数据模型的例子。

### 1.2 生态系统概述

本节描述了核心行为者的角色，以及在可验证凭证有望发挥作用的生态系统中它们之间的关系。角色是一个抽象的概念，可以以许多不同的方式实现。角色的分离表明了可能的接口和标准化协议。本规范中介绍了以下角色：

**持有人**

一个实体通过拥有一个或多个可验证凭证，并从中生成可验证展示，从而可以履行的角色。例子：持有人包括学生、员工和客户。

**签发人**

一个实体通过对一个或多个主体提出权利主张，从这些权利主张中创造一个可验证凭证，并将可验证凭证传送给持有人而发挥的作用。签发人的例子包括公司、非营利组织、行业协会、政府和个人。

**主体**

对其提出主张的实体。例如，主体包括人、动物和事物。在许多情况下，可验证凭证的持有人是主体，但在某些情况下不是。例如，父母（持有人）可能持有子女（主体）的可验证凭证，或者宠物主人（持有人）可能持有其宠物（主体）的可验证凭证。关于这些特殊情况的更多信息，请参见附录§C.主体与持有人的关系。

**核验人**

一个实体通过接收一个或多个可验证凭证（可选择在可验证展示中）进行处理而发挥的作用。核验人的例子包括雇主、安全人员和网站。

**可验证数据登记处**

一个系统可能发挥的作用是，通过调解标识符、密钥和其他相关数据的创建和验证，如可验证凭证模式、撤销登记册、签发人公钥等，使用可验证凭证可能需要这些数据。有些配置可能需要主体的可关联标识符。可验证数据登记处的例子包括可信数据库、分散式数据库、政府身份数据库和分布式账本。通常，一个生态系统中使用的可验证数据登记处类型不止一种。

![该图显示了凭证如何从发行者流向持有者，演示如何从持币者流向验证者，所有三个方面都可以使用逻辑可验证数据注册表中的信息](https://w3c.github.io/vc-data-model/diagrams/ecosystem.svg)

*图 1：角色和信息流构成了本规范的基础。*

> 注：
>
> 上文图 1 提供了一个生态系统的例子，本规范中的其他概念都是基于此。还存在其他生态系统，如受保护的环境或专有系统，在这些系统中，可核查的凭证也能带来好处。

### 1.3 用例和需求

本节是非规范性的。

可验证凭证用例文件[VC-USECASES]概述了一些读者可能认为有用的关键主题，包括：

- 对上文介绍的作用进行更全面的解释

- 在教育、金融、医疗、零售、专业许可和政府等垂直市场中确定的需求。

- 生态系统中各角色执行的共同任务及其相关要求

- 工作组确定的共同序列和流程。

通过记录和分析用例文件，为本规范确定了以下理想的生态系统特征：

- 可验证的凭证是指签发人以不可篡改和尊重隐私的方式作出的声明。
- 持有人将来自不同签发人的可验证凭证集合成一个单一的艺术品，即可验证展示。
- 签发人可以签发任何主题的可验证凭证。
- 作为签发人、持有人或核验人，既不需要注册，也不需要任何机构的批准，因为所涉及的信任是双方之间的。
- 可验证展示允许任何核验人验证来自任何签发人的可验证凭证的真实性。
- 持有人可以从任何人那里收到可验证的凭证。
- 持有人可以通过任何用户代理与任何签发人和任何核验人互动。
- 持有人可以分享可验证的展示，然后可以在不向签发人透露核验人身份的情况下对其进行验证。
- 持有人可以将可验证的凭证存储在任何地点，而不影响其可验证性，签发人也不会知道其存储地点或何时被访问。
- 持有人可以向任何核验人展示**可验证展示**，而不影响债权的真实性，也不会将该行为透露给签发人。
- 核验人可以核验任何持有人提交的可验证展示，其中包含任何签发人的索赔证明。
- 核验不应依赖签发人和核验人之间的直接互动。
- 核验不应向任何签发人透露核验人的身份。
- 规范必须提供一种方法，让签发人发出支持选择性披露的可验证凭证，而不要求所有符合要求的软件支持该功能。
- 签发人可以签发支持选择性披露的可验证凭证。
- 如果单个可验证凭证支持选择性披露，那么持有人就可以在不透露整个可验证凭证的情况下展示权利要求的证明。
- 可验证展示可以披露可验证凭证的属性，或者满足核验人要求的派生谓词。派生谓词是布尔条件，如大于、小于、等于、在集合中等等。
- 签发人可以签发可撤销的可验证凭证。
- 可验证凭证和可验证展示必须以一种或多种机器可读数据格式进行序列化。序列化和/或去序列化的过程必须是确定的、双向的和无损的。可验证的凭证或可验证的呈现的任何序列化都需要在确定性过程中可转换为本文档中定义的通用数据模型，从而所产生的可验证的凭证可以以可互操作的方式处理。序列化的形式还需要能够从数据模型中生成，而不会丢失数据或内容。
- 数据模型和序列化必须可以在最小的协调下进行扩展。
- 签发人的撤销不应透露任何有关主体、持有人、具体的可验证凭证或核验人的识别信息。
- 签发人可以披露撤销原因。
- 签发人撤销可验证凭证时，应区分因加密完整性而撤销（例如，签名密钥泄露）和因状态改变而撤销（例如，驾驶执照被暂停）。
- 签发人可以提供刷新可验证凭证的服务。 

### 1.4 符合标准

除了标记为非规范性的部分外，本规范中的所有编写指南、图表、示例和注释都是非规范性的。本规范中的其他所有内容都是规范的。

本文档中的关键词MAY、MUST、MUST NOT、RECOMMENDED和SHOULD应按照BCP 14 [RFC2119] [RFC8174]中的描述进行解释，当且仅当它们出现在所有大写字母中时，如这里所示。

符合性文档是指数据模型的任何具体表达，符合本规范中的规范性声明。具体来说，所有相关的规范性声明在《第4节. 基本概念》、《第 5 节. 高级概念》和《第 6 节. 本文档的语法》。符合要求的文档的序列化格式必须是确定性的、双向的和无损的，如第6节所述。语法。符合文件可以用任何这样的序列化格式传输或存储。

符合处理器是任何以软件和/或硬件实现的算法，它产生或消耗符合文件。当不符合要求的文档被消耗时，符合要求的处理器必须产生错误。

本规范不对生态系统中的角色（如签发人、持有人或核验人）的符合性做出规范性声明，因为生态系统角色的符合性是高度应用、用例和市场垂直特定的。

数字证明机制，其中的一个子集是数字签名，需要确保可验证凭证的保护。拥有和验证证明，可能取决于证明的语法（例如，使用JSON Web Token的JSON Web签名来证明密钥持有者），是处理可验证凭证的一个重要部分。在本报告发表时，工作组成员已经使用至少三种证明机制实施了可验证凭证：

- JSON网络令牌[ [RFC7519](https://w3c.github.io/vc-data-model/#bib-rfc7519) ]使用JSON网络签名担保[ [RFC7515](https://w3c.github.io/vc-data-model/#bib-rfc7515) ]
- 链接的数据签名[ [LD-SIGNATURES](https://w3c.github.io/vc-data-model/#bib-ld-signatures) ]
- Camenisch-Lysyanskaya零知识证明[ [CL签名](https://w3c.github.io/vc-data-model/#bib-cl-signatures)] 。

请实施者注意，截至本规范发布之日，并非所有的证明机制都是标准化的。工作组希望其中一些机制以及新的机制能够独立地成熟起来，并在一段时间内实现标准化。鉴于有多种有效的证明机制，本规范并不对任何一种数字签名机制进行标准化。本规范的目标之一是提供一个数据模型，该模型可以被各种当前和未来的数字证明机制所保护。本规范的符合性并不取决于特定证明机制的细节，它要求明确识别可验证凭证使用的机制。

本文档还包含包含JSON和JSON-LD内容的例子。这些例子中的一些字符是无效的JSON，例如内联注释(//)和使用省略号(...)来表示对例子没有什么价值的信息。如果实施者希望将这些信息作为有效的JSON或JSON-LD使用，请注意删除这些内容。



## 2、术语

*本节是非规范性的。*

以下术语用于描述本说明书中的概念。

**主张**

对某一主题作出的主张。

**凭证**

签发人提出的一组一个或多个主张。可验证凭证是一种不可篡改的凭证，其作者身份可通过密码学方式加以核实。可验证凭证可以用来建立可验证展示，而这些展示也可以进行密码学验证。凭证中的主张可以是关于不同的主题。

**数据最小化**

将共享数据量严格限制为成功完成任务或目标所需的最低限度的行为。

**分散标识符**

基于URL的可移植标识符，也称为DID，与一个实体相关联。这些标识符最常用于可验证凭证中，并与主体相关联，从而使可验证凭证本身可以很容易地从一个存储库移植到另一个存储库，而无需重新发布凭证。DID的一个例子是 `did:example:123456abcdef`。

**分散标识符文件**

也被称为DID文档，这是一个使用可验证的数据注册表进行访问的文档，包含了与特定的去中心化标识符相关的信息，如相关的存储库和公钥信息。

**派生谓词**

关于可验证凭证中另一个属性的值的可验证布尔声明 。这些在零知识证明风格的可验证展示中很有用， 因为它们可能会限制信息公开。例如，如果可验证凭证包含用于表示特定高度（以厘米为单位）的属性，则派生谓词可能会引用可验证凭证中的height属性，这表明签发人证明了满足最小高度要求的高度值，而没有实际披露特定的高度。高度值。例如，对象的身高超过150厘米。

**电子签名**

一种证明数字消息真实性的数学方案。

**实体**

具有独特和独立存在的事物，例如在生态系统中执行一个或多个角色的个人，组织或设备。

**图形**

由主体及其与其他主体或数据的关系组成的信息网络。

**持有人**

一个实体通过拥有一个或多个可验证凭证并据此生成可验证展示而可能发挥的作用。持有人通常是，但并不总是他们所持有的可验证凭证的主体。持有者将其凭证存储在凭证库中。

**身份**

追踪不同背景下的实体的手段。数字身份使人们能够跟踪和定制实体在不同数字环境下的互动，通常使用标识符和属性。身份信息的意外分发或使用会损害隐私。收集和使用这类信息应当遵循数据最小化原则。

**身份提供者**

身份提供者，有时简称IdP，是一个为持有人创建、维护和管理身份信息的系统，同时在联盟或分布式网络中为依赖方应用提供认证服务。在这种情况下，持有人始终是主体。即使可验证凭证是不记名凭证，也假定可验证凭证仍然是主体，如果不是主体，则是被攻击者窃取。本规范不使用这个术语，除非将本文档中的概念与其他规范进行比较或映射。本规范将身份提供者的概念分解为两个不同的概念：签发人和持有人。

**签发人**

一个实体可以通过对一个或多个主体提出主张，从这些主张中创建一个可验证的凭证，并将可验证的凭证传送给持有人来履行的角色。

**展示**

由一个或多个签发人签发的一个或多个可验证凭证所产生的、与特定核验人共享的数据。可验证展示是一种不可篡改的展示文稿，其编码方式是在经过密码学核查过程后，可以相信数据的作者身份。某些类型的可验证展示可能包含从原始可验证凭证合成的数据，但不包含原始可验证凭证（例如，零知识证明）。

**资料库**
一种程序，如存储库或个人可验证凭证钱包，用于存储和保护对持有人可验证凭证的访问。

**选择性披露**

持有人能够对分享什么信息做出精细的决定。

**课题**

一件事情，对其提出要求。

**用户代理**
浏览器或其他网络客户端等程序，用于协调持有人、签发人和核验人之间通信。

**验证**

保证可验证凭证或可验证展示满足核验人和其他利益相关者的需要。本规范只限于验证可验证凭证和可验证展示，无论其用途如何。验证可验证凭证或可验证展示不在本规范的范围之内。

**可验证的数据登记册**
一个系统可能发挥的作用是，通过调解标识符、密钥和其他相关数据的创建和验证，如可验证凭证模式、撤销登记册、签发人公钥等，使用可验证凭证可能需要这些数据。有些配置可能需要主体的可关联标识符。有些登记处，如UUIDs和公钥的登记处，可能只是作为标识符的命名空间。

**验证**

评价可验证凭证或可验证展示是否分别是签发人或展示人的真实和及时的声明。这包括检查：凭证(或展示)是否符合规格；证明方法是否符合要求；如果存在，状态检查是否成功。

**核验人**

一个实体通过接收一个或多个可验证凭证来执行的角色，可选择在一个可验证展示中进行处理。其他规范可能将这一概念称为依赖方。

**URI**

由[ [RFC3986](https://w3c.github.io/vc-data-model/#bib-rfc3986) ]定义的统一资源标识符。

## 3、核心数据模型

*本节是非规范性的。*

以下各节概述了核心数据模型概念，如索赔、凭证和展示，它们构成了本规范的基础。

### 3.1 主张

主张是关于一个主体的陈述。主体是可以提出主张的事物。权利要求是用**主体-属性-价值**关系来表达的。

![图2 主张的基本结构](https://w3c.github.io/vc-data-model/diagrams/claim.svg)

*图2 主张的基本结构*

上文图2所示的主张数据模型功能强大，可用于表达多种多样的陈述。例如，某人是否毕业于某所大学，可以用下图3所示来表示。

![图3 表达帕特是 "榜样大学 "校友的基本主张](https://w3c.github.io/vc-data-model/diagrams/claim-example.svg)

*图3 表达Pat是 "Example University" 校友的基本主张*

各个主张可以合并在一起，以表达一个主题的信息图。下文图4所示的例子是对前一个主张的扩展，增加了Pat认识Sam和Sam被聘为教授的主张。

![用另一个名为Knows的属性扩展前一个图，该属性的值是Sam，而Sam的属性jobTitle的值是Professor](https://w3c.github.io/vc-data-model/diagrams/claim-extended.svg)

*图4 多个主张可以组合成一个信息图来表达*

至此，引入了主张和信息图的概念。为了能够信任主张，希望在图中加入更多的信息。

### 3.2 凭证

凭证是同一实体提出的一组一个或多个主张。凭证还可能包括一个标识符和元数据，以描述凭证的属性，如签发人、失效日期和时间、代表图像、用于核查目的的公用钥匙、撤销机制等。元数据可能由签发人签名。可验证的凭证是一组不可篡改的主张和元数据，通过密码学方式证明是谁签发的。

![验证凭证包含凭证元数据，主张和证明](https://w3c.github.io/vc-data-model/diagrams/credential.svg)

*图5 可验证凭证的基本组成部分。*

可验证凭证包括数字员工身份证、数字出生证明和数字教育证书等。

> 注意：
>
> 凭证标识符通常用于识别凭证的具体实例。这些标识符也可用于关联。建议希望最大限度地减少关联性的持有人使用不透露凭证标识符的选择性披露方案。

上图5显示了可验证凭证的基本组成部分，但抽象了关于如何将主张组织成信息图，然后将信息图组织成可验证凭证的细节。下图6显示了一个可验证凭证的比较完整的描述，它通常由至少两个信息图组成。第一个图表达了可验证凭证本身，它包含了凭证元数据和主张。第二张图表示数字证明，通常是数字签名。

![图中的凭证图在顶部，凭证通过证明连接到底部的证明图。 Credental Graph的凭证123具有4个属性：值AlumniCredential的“类型”，示例大学的“发行人”，2010-01-01T19：73：24Z的“ issuanceDate”和具有alumniOf属性且具有值的Pat的credentialSubject例子大学。 证明图具有具有5个属性的签名456：RsaSignature2018的``类型''，示例大学公共密钥7的``verificationMethod''，2017-06-18T21：19：10Z的``创建''以及BavEll0的``jws''... 3JT24 ='](https://w3c.github.io/vc-data-model/diagrams/credential-graph.svg)

图6与基本可验证凭证相关的信息图。

> 注意：
>
> 一个凭证，如结婚证，有可能包含多个不同主体的主张，但不需要关联。

> 注意：
>
> 有可能有一种凭证不包含关于被签发凭证的实体的任何主张。例如，一种只包含关于某只狗的权利主张的证书，但发给它的主人。



### 3.3 展示

本节是非规范性的。

加强隐私是本规范的一个关键设计特征。因此，对于使用该技术的实体来说，重要的是要能够只表达适合特定情况的角色的部分。一个人的persona子集的表达被称为可验证展示。不同角色的例子包括一个人的职业角色、其在线游戏角色、其家庭角色或隐姓埋名角色。

可验证展示表达来自一个或多个可验证凭证的数据，并以数据的作者身份可验证的方式进行包装。如果可验证凭证被直接呈现，它们就成为可验证展示。由可验证凭证衍生出来的数据格式，如果在密码学上是可验证的，但其本身并不包含可验证凭证，也可能是可验证展示。

展示中的数据往往是关于同一主题的，但可能是由多个发布者发布的。这类信息的汇总通常表示个人、组织或实体的一个方面。

![可验证的展示文稿包含展示文稿元数据，可验证的凭据和证明](https://w3c.github.io/vc-data-model/diagrams/presentation.svg)

*图7 可验证展示的基本组成部分。*

上图7显示了可验证展示的组成部分，但抽象了关于如何将可验证凭证组织成信息图，然后再组织成可验证展示的细节。下图8显示了一个更完整的可验证展示的描述，它通常由至少四个信息图组成。第一个图表达了可验证展示本身，其中包含展示元数据。图中的verifiable Presentation属性指的是一个或多个可验证凭证（每个凭证都是一个自足的图），它又包含凭证元数据和主张。第三张图表达了凭证图证明，它通常是一个数字签名。第四个图表示展示图证明，它通常是一个数字签名。

![展示图在顶部的展示图，通过证明连接到底部的展示图。 Presentation Graph具有具有3个属性的Presentation ABC：值VerifiablePresentation的“类型”，值Not Archive的“ termsOfUse”和值为6的“ verifiableCredential”。Presentation Proof Graph具有具有5个属性的Signature 8910：“ type” RsaSignature2018的示例，示例展示者公钥11的``验证方法''，2018-01-15T12：43：56Z的``创建''，d28348djsj3239的``挑战''以及``p2KaZ ... 8Fj3K =''的``jws''](https://w3c.github.io/vc-data-model/diagrams/presentation-graph.svg)

*图8与基本的可验证展示相关的信息图。*

> 注：
> 可以有一个展示，比如商业人物，它借鉴了多个关于不同主题的凭证，这些凭证往往是相关的，但不是必须的。

### 3.4 具体生命周期示例

本节是非规范性的。

前面的章节介绍了主张、可验证凭证和使用图形描述的可验证展示等概念。本节提供了一组具体的简单但完整的数据模型生命周期示例，这些示例用本规范支持的一种具体语法来表达。在可验证凭证生态系统中，凭证和展示的生命周期通常采取共同的路径：

1. 签发一个或多个可验证凭证。

2. 将可验证凭证存储在凭证库（如数字钱包）中。

3. 将可验证凭证组成一个可验证展示，供核验人使用。

4. 由核验人对可验证展示进行验证。

为了说明这个生命周期，我们将以从大学兑换校友折扣为例。在下面的例子中，Pat从大学收到了一张校友可验证凭证，Pat将这张可验证凭证存储在一个数字钱包中。

```json
//例1:可验证凭证的简单示例

{
  //设置上下文，该上下文确定了我们将要使用的特殊术语
  //例如“ issuer”和“ alumniOf”。
  “ @context”：[
    “ https://www.w3.org/2018/credentials/v1”，
    “ https://www.w3.org/2018/credentials/examples/v1”
  ]，
  //指定凭证的标识符
  “ id”：“ http://example.edu/credentials/1872”，
  //凭证类型，用于声明凭证中应包含哪些数据
  “ type”：[“ VerifiableCredential”，“ AlumniCredential”]，
  //发出凭证的实体
  “ issuer”：“ https://example.edu/issuers/565049”，
  //颁发凭证时间
  “ issuanceDate”：“ 2010-01-01T19：73：24Z”，
  //关于凭证主题的声明
  “ credentialSubject”：{
    //凭证唯一主题的标识符
    “ id”：“ did：example：ebfeb1f712ebc6f1c276e12ec21”，
    //关于凭证的唯一主题的断言
    “ alumniOf”：{
      “ id”：“ did：example：c276e12ec21ebfeb1f712ebc6f1”，
      “名称”： [{
        “ value”：“ Example University”，
        “ lang”：“ en”
      }，{
        “ value”：“大学典范”，
        “ lang”：“ fr”
      }]
    }
  }，
  //证明凭证被篡改的数字证明
  //有关详细信息，请参见本节末尾的注释
  “证明”：{
    //用于生成签名的加密签名套件
    “ type”：“ RsaSignature2018”，
    //签名创建的日期
    “ created”：“ 2017-06-18T21：19：10Z”，
    //此证明的目的
    “ proofPurpose”：“ assertionMethod”，
    //可以验证签名的公钥标识符
    “ verificationMethod”：“ https://example.edu/issuers/keys/1”，
    //数字签名值
    “ jws”：“ eyJhbGciOiJSUzI1NiIsImI2NCI6ZmFsc2UsImNyaXQiOlsiYjY0Il19..TCYt5X
      sITJX1CxPCT8yAV-TVkIEq_PbChOMqsLfRoPsnsgw5WEuts01mq-pQy7UJiN5mgRxD-WUc
      X16dUEMGlv50aqzpqh4Qktb3rk-BuQy72IFLOqV0G_zS245-kronKb78cPN25DGlcTwLtj
      PAYuNzVBAh4vGHSrQyHUdBBPM”
  }
}
```

随后，Pat 试图兑换校友折扣。验证器，即票务销售系统，指出任何 "例子大学 "的校友都可以享受体育赛事季票的折扣。使用移动设备，Pat 开始购买季票的过程。在这个过程中，有一个步骤要求提供一个校友可验证凭证，这个要求被路由到帕特的数字钱包。数字钱包会询问帕特是否愿意提供以前发行的可验证凭证。帕特选择校友可验证凭证，然后将其组成一个可验证展示。可验证展示会被发送给验证者并进行验证。



```json
例2：可验证展示文稿的简单示例
{
  “ @context”：[
    “ https://www.w3.org/2018/credentials/v1”，
    “ https://www.w3.org/2018/credentials/examples/v1”
  ]，
  “ type”：“ VerifiablePresentation”，
  //上一个示例中发布的可验证凭证
  “ verifiableCredential”：[{
    “ @context”：[
      “ https://www.w3.org/2018/credentials/v1”，
      “ https://www.w3.org/2018/credentials/examples/v1”
    ]，
    “ id”：“ http://example.edu/credentials/1872”，
    “ type”：[“ VerifiableCredential”，“ AlumniCredential”]，
    “ issuer”：“ https://example.edu/issuers/565049”，
    “ issuanceDate”：“ 2010-01-01T19：73：24Z”，
    “ credentialSubject”：{
      “ id”：“ did：example：ebfeb1f712ebc6f1c276e12ec21”，
      “ alumniOf”：{
        “ id”：“ did：example：c276e12ec21ebfeb1f712ebc6f1”，
        “name”： [{
          “ value”：“ Example University”，
          “ lang”：“ en”
        }，{
          “ value”：“ Exemple d'Université ”，
          “ lang”：“ fr”
        }]
      }
    }，
    “proof”：{
      “ type”：“ RsaSignature2018”，
      “ created”：“ 2017-06-18T21：19：10Z”，
      “ proofPurpose”：“ assertionMethod”，
      “ verificationMethod”：“ https://example.edu/issuers/keys/1”，
      “ jws”：“ eyJhbGciOiJSUzI1NiIsImI2NCI6ZmFsc2UsImNyaXQiOlsiYjY0Il19..TCYt5X
        sITJX1CxPCT8yAV-TVkIEq_PbChOMqsLfRoPsnsgw5WEuts01mq-pQy7UJiN5mgRxD-WUc
        X16dUEMGlv50aqzpqh4Qktb3rk-BuQy72IFLOqV0G_zS245-kronKb78cPN25DGlcTwLtj
        PAYuNzVBAh4vGHSrQyHUdBBPM”
    }
  }]，
  // Pat在展示文稿上进行数字签名
  //防止重放攻击
  “proof”：{
    “ type”：“ RsaSignature2018”，
    “ created”：“ 2018-09-14T21：19：10Z”，
    “ proofPurpose”：“authentication”，
    “ verificationMethod”：“ did：example：ebfeb1f712ebc6f1c276e12ec21＃keys-1”，
    //“挑战”和“域”可防止重放攻击
    “challenge”：“ 1f44d55f-f161-4938-a659-f8026467f126”，
    “ domain”：“ 4jt78h47fh47”，
    “ jws”：“ eyJhbGciOiJSUzI1NiIsImI2NCI6ZmFsc2UsImNyaXQiOlsiYjY0Il19..kTCYt5
      XsITJX1CxPCT8yAV-TVIw5WEuts01mq-pQy7UJiN5mgREEMGlv50aqzpqh4Qq_PbChOMqs
      LfRoPsnsgxD-WUcX16dUOqV0G_zS245-kronKb78cPktb3rk-BuQy72IFLN25DYuNzVBAh
      4vGHSrQyHUGlcTwLtjPAnKb78“
  }
}
```

## 4、基本概念

本节介绍了本规范的一些基本概念，为后面的第5节高级概念做准备《高级概念》的准备。

### 4.1 语境

当两个软件系统需要交换数据时，需要使用两个系统都能理解的术语。作为一个类比，考虑两个人如何交流。两个人都必须使用相同的语言，而且他们使用的词语对彼此的意义必须相同。这可能被称为对话的语境。

可验证的凭证和可验证的演示有许多属性和价值，这些属性和价值是由URI识别的。然而，这些URI可能很长，而且对人类不是很友好。在这种情况下，短式的对人类友好的别名会更有帮助。本规范使用 @context 属性将这种短式别名映射到特定可验证凭证和可验证演示所需的 URI 上。

> 注
>
> 在JSON-LD中，@context属性也可以用来传达其他细节，如数据类型信息、语言信息、转换规则等，这些信息超出了本规范的需求，但在未来或相关工作中可能有用。更多信息请参见第3.1节：[JSON-LD]规范的上下文。

可验证凭证和可验证展示必须包含 @context 属性。

**@context**
@context属性的值必须是一个有序的集合，其中第一项是一个URI，其值为`https://www.w3.org/2018/credentials/v1`。为便于参考，附录§B.基础上下文中提供了基础上下文的副本。数组中的后续项必须表达上下文信息，并由 URI 或对象的任意组合组成。建议 @context 中的每一个 URI 都是这样的，如果被 dereferenced，就会产生一个包含 @context 的机器可读信息的文档。

> 注
>
> 虽然本规范要求存在@context属性，但并不要求使用JSON-LD处理@context属性的值。这是为了支持使用纯 JSON 库进行处理，例如当可验证凭证被编码为 JWT 时可能会使用的那些库。所有库或处理器必须确保@context属性中的值的顺序是特定应用所期望的。支持JSON-LD的库或处理器可以按照预期使用完整的JSON-LD处理来处理@context属性。

```json
EXAMPLE 3: Usage of the @context property
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "id": "http://example.edu/credentials/58473",
  "type": ["VerifiableCredential", "AlumniCredential"],
  "credentialSubject": {
    "id": "did:example:ebfeb1f712ebc6f1c276e12ec21",
    "alumniOf": {
      "id": "did:example:c276e12ec21ebfeb1f712ebc6f1",
      "name": [{
        "value": "Example University",
        "lang": "en"
      }, {
        "value": "Exemple d'Université",
        "lang": "fr"
      }]
    }
  },
  "proof": {  }
}
```

上面的例子使用基本上下文URI(`https://www.w3.org/2018/credentials/v1`)来建立对话是关于可验证凭证。第二个URI (`https://www.w3.org/2018/credentials/examples/v1`)建立了对话是关于例子的。

> 注
>
> 本文档使用示例上下文URI(`https://www.w3.org/2018/credentials/examples/v1`)来演示示例。希望实施者不要将此URI用于任何其他目的，例如在试验或生产系统中。
>

`https://www.w3.org/2018/credentials/v1` 上的数据是一个静态文档，永远不会更新，应该下载和缓存。与可验证凭证数据模型相关的人可读词汇文件可在 `https://www.w3.org/2018/credentials` 找到。这一概念将在第5.3节可扩展性中进一步阐述。

### 4.2 识别符

当表达关于特定事物（如人、产品或组织）的声明时，使用某种标识符通常是有用的，这样其他人就可以表达关于同一事物的声明。本规范为这种标识符定义了可选的 id 属性。id 属性旨在毫不含糊地指代一个对象，如人、产品或组织。使用id属性可以在可验证凭证中表达关于特定事物的声明。

如果存在id属性：

- id属性必须表达一个标识符，其他人在表达关于由该标识符标识的特定事物的声明时，必须使用该标识符。
- id 属性必须不具有一个以上的值。
- id 属性的值必须是一个 URI。

>注释
>
>开发者应记住，在需要假名的情况下，标识符可能是有害的。鼓励开发者在考虑这种情况时仔细阅读第7.3节基于标识符的相关性。还有其他类型的相关机制在第7节中有所记载。产生隐私问题的隐私考虑因素。当隐私是一个强烈的考虑因素时，id属性可以被省略。

**id**

id 属性的值必须是一个 URI。建议 id 中的 URI 如果被解引，则会产生一个包含关于 id 的机器可读信息的文档。

```json
EXAMPLE 4: Usage of the id property
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "id": "http://example.edu/credentials/3732",
  "type": ["VerifiableCredential", "UniversityDegreeCredential"],
  "credentialSubject": {
    "id": "did:example:ebfeb1f712ebc6f1c276e12ec21",
    "degree": {
      "type": "BachelorDegree",
      "name": "Bachelor of Science and Arts"
    }
  },
  "proof": { ... }
}
```

上面的例子使用了两种类型的标识符。第一个标识符用于可验证凭证，使用基于HTTP的URL。第二种标识符是针对可验证凭证的主体（关于主张的事情），使用分散式标识符，也称为 DID。

> 注
>
> 从本出版物开始，DIDs是一种新的标识符，它不是可验证凭证发挥作用的必要条件。具体而言，可验证凭证不依赖于DID，而DID也不依赖于可验证凭证。但是，预计许多可验证凭证将使用DID，实现本规范的软件库可能需要解析DID。基于DID的URL用于表达与主体、签发人、持有人、凭证状态列表、加密密钥以及其他与可验证凭证相关的机器可读信息相关的标识符。

### 4.3 类型

处理本文档中指定的各类对象的软件系统使用类型信息来确定所提供的可验证凭证或可验证展示是否合适。本规范为类型信息的表达定义了一个类型属性。

可验证凭证和可验证展示必须有一个类型属性。也就是说，任何没有类型属性的凭证或展示都是不可验证的，所以既不是可验证凭证，也不是可验证演示。

**type**

类型属性的值必须是或映射到（通过对@context属性的解释）一个或多个URI。如果提供了一个以上的URI，URI必须被解释为一个无序的集合。语法上的便利性应该被用来方便开发者使用。这些便利条件可能包括JSON-LD术语。建议类型中的每一个URI如果被派生，就会产生一个包含关于类型的机器可读信息的文档。



```json
EXAMPLE 5: Usage of the type property
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "id": "http://example.edu/credentials/3732",
  "type": ["VerifiableCredential", "UniversityDegreeCredential"],
  "credentialSubject": {
    "id": "did:example:ebfeb1f712ebc6f1c276e12ec21",
    "degree": {
      "type": "BachelorDegree",
      "name": "Bachelor of Science and Arts"
    }
  },
  "proof": { ... }
}
```

关于本规范，下表列出了必须有指定类型的对象：

| Object                                                       | Type                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [Verifiable credential](https://w3c.github.io/vc-data-model/#dfn-verifiable-credentials) object (a subclass of a [credential](https://w3c.github.io/vc-data-model/#credentials) object) | `VerifiableCredential` and, optionally, a more specific [verifiable credential](https://w3c.github.io/vc-data-model/#dfn-verifiable-credentials) [type](https://w3c.github.io/vc-data-model/#dfn-type). For example, `"type": ["VerifiableCredential", "UniversityDegreeCredential"]` |
| [Credential](https://w3c.github.io/vc-data-model/#credentials) object | `VerifiableCredential` and, optionally, a more specific [verifiable credential](https://w3c.github.io/vc-data-model/#dfn-verifiable-credentials) [type](https://w3c.github.io/vc-data-model/#dfn-type). For example, `"type": ["VerifiableCredential", "UniversityDegreeCredential"]` |
| [Verifiable presentation](https://w3c.github.io/vc-data-model/#dfn-verifiable-presentations) object (a subclass of a [presentation](https://w3c.github.io/vc-data-model/#presentations) object) | `VerifiablePresentation` and, optionally, a more specific [verifiable presentation](https://w3c.github.io/vc-data-model/#dfn-verifiable-presentations) [type](https://w3c.github.io/vc-data-model/#dfn-type). For example, `"type": ["VerifiablePresentation", "CredentialManagerPresentation"]` |
| [Presentation](https://w3c.github.io/vc-data-model/#presentations) object | `VerifiablePresentation` and, optionally, a more specific [verifiable presentation](https://w3c.github.io/vc-data-model/#dfn-verifiable-presentations) [type](https://w3c.github.io/vc-data-model/#dfn-type). For example, `"type": ["VerifiablePresentation", "CredentialManagerPresentation"]` |
| [Proof](https://w3c.github.io/vc-data-model/#proofs-signatures) object | A valid proof [type](https://w3c.github.io/vc-data-model/#dfn-type). For example, `"type": "RsaSignature2018"` |
| [credentialStatus](https://w3c.github.io/vc-data-model/#status) object | A valid [credential](https://w3c.github.io/vc-data-model/#dfn-credential) status [type](https://w3c.github.io/vc-data-model/#dfn-type). For example, `"type": "CredentialStatusList2017"` |
| [termsOfUse](https://w3c.github.io/vc-data-model/#terms-of-use) object | A valid terms of use [type](https://w3c.github.io/vc-data-model/#dfn-type). For example, `"type": "OdrlPolicy2017"`) |
| [evidence](https://w3c.github.io/vc-data-model/#evidence) object | A valid evidence [type](https://w3c.github.io/vc-data-model/#dfn-type). For example, `"type": "DocumentVerification2018"` |

> 注
>
> 可验证凭证数据模型的类型系统与[JSON-LD]相同，详见第5.4节：指定类型和第8节：JSON-LD语法。当使用JSON-LD上下文时（见第5.3节可扩展性），本规范将@type关键字别名为type，使JSON-LD文档更容易理解。虽然应用开发者和文档作者不需要理解JSON-LD类型系统的具体内容，但本规范的实现者如果想支持可互操作的可扩展性，则需要理解。

所有的凭证、展示和封装对象都必须指定或关联其他更狭义的类型（例如，像UniversityDegreeCredential），以便软件系统能够处理这些附加信息。

当处理本规范中定义的封装对象时，（例如，与credentialSubject对象相关联的对象或深嵌在其中的对象），软件系统should使用层次结构中更高的封装对象中指定的类型信息。具体而言，封装对象，例如凭证，showuld传达相关联的对象类型，以便验证者可以根据封装对象类型快速确定相关联的对象的内容。

例如，一个类型为UniversityDegreeCredential的凭证对象，向验证者发出信号：与credentialSubject属性相关联的对象包含了id属性中的标识符。

- id属性中的Subject的标识符
- type属性中的学位类型。
- name属性中的学位的标题。

这使得实现者能够依靠与类型属性相关联的值来进行验证。对类型及其相关属性的期望至少应该被记录在一个人类可读的规范中，最好是在一个额外的机器可读的表示中。

> 注释
> 本规范所述数据模型中使用的类型系统允许以多种方式将类型与数据联系起来。促请实施者和作者阅读《可验证证书实施指南》[VC-IMP-GUIDE]中关于类型的部分。

### 4.4 凭证主题

一个可验证凭证包含关于一个或多个主体的权利要求。本规范定义了一个 credentialSubject 属性，用于表达关于一个或多个主体的主张。

一个可验证的凭证必须有一个 credentialSubject 属性。

**credentialSubject**

credentialSubject 属性的值被定义为一组对象，这些对象包含一个或多个属性，这些属性分别与可验证凭证的主题相关。每个对象可以包含一个 ID，如第 4.2 节标识符所述。

```json
EXAMPLE 6: Usage of the credentialSubject property
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "id": "http://example.edu/credentials/3732",
  "type": ["VerifiableCredential", "UniversityDegreeCredential"],
  "credentialSubject": {
    "id": "did:example:ebfeb1f712ebc6f1c276e12ec21",
    "degree": {
      "type": "BachelorDegree",
      "name": "Bachelor of Science and Arts"
    }
  },
  "proof": { ... }
}
```

可以在一个可验证凭证中表达与多个主体相关的信息。下面的示例指定了两个主体，他们是配偶。注意使用数组符号将多个主体与 credentialSubject 属性关联起来。

```json
EXAMPLE 7: Specifying multiple subjects in a verifiable credential
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "id": "http://example.edu/credentials/3732",
  "type": ["VerifiableCredential", "RelationshipCredential"],
  "credentialSubject": [{
    "id": "did:example:ebfeb1f712ebc6f1c276e12ec21",
    "name": "Jayden Doe",
    "spouse": "did:example:c276e12ec21ebfeb1f712ebc6f1"
  }, {
    "id": "did:example:c276e12ec21ebfeb1f712ebc6f1",
    "name": "Morgan Doe",
    "spouse": "did:example:ebfeb1f712ebc6f1c276e12ec21"
  }],
  "proof": { ... }
}
```

### 4.5 签发人

本规范定义了一个属性，用于表达可验证凭证的签发人。

一个可验证凭证必须有一个签发人属性。

**issuer**

签发人属性的值必须是一个URI或一个含有id属性的对象。建议签发人或其id中的URI如果被派生，就会产生一个包含关于签发人的机器可读信息的文件，可用于验证凭证中表达的信息。

```json
EXAMPLE 8: Usage of issuer property
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "id": "http://example.edu/credentials/3732",
  "type": ["VerifiableCredential", "UniversityDegreeCredential"],
  "issuer": "https://example.edu/issuers/14",
  "issuanceDate": "2010-01-01T19:23:24Z",
  "credentialSubject": {
    "id": "did:example:ebfeb1f712ebc6f1c276e12ec21",
    "degree": {
      "type": "BachelorDegree",
      "name": "Bachelor of Science and Arts"
    }
  },
  "proof": { ... }
}
```

还可以通过将对象与签发人属性相关联来表达关于签发人的附加信息。

```json
EXAMPLE 9: Usage of issuer expanded property
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "id": "http://example.edu/credentials/3732",
  "type": ["VerifiableCredential", "UniversityDegreeCredential"],
  "issuer": {
    "id": "did:example:76e12ec712ebc6f1c221ebfeb1f",
    "name": "Example University"
  },
  "issuanceDate": "2010-01-01T19:23:24Z",
  "credentialSubject": {
    "id": "did:example:ebfeb1f712ebc6f1c276e12ec21",
    "degree": {
      "type": "BachelorDegree",
      "name": "Bachelor of Science and Arts"
    }
  },
  "proof": { ... }
}
```

注
发行人属性的值也可以是JWK（例如，"`https://example.com/keys/foo.jwk`"）或DID（例如，"`did:example:abfe13f712120431c276e12ecab`"）。

### 4.6 签发日期

本规范定义了 issuanceDate 属性，用于表达凭证生效的日期和时间。

**issuanceDate**

一个凭证必须有一个issueanceDate属性。issuanceDate 属性的值必须是一个 [RFC3339] 结合日期和时间的字符串值，代表凭证变得有效的日期和时间，它可以是未来的日期和时间。请注意，这个值代表与 credentialSubject 属性相关联的信息变得有效的最早时间点。



```json
EXAMPLE 10: Usage of issuanceDate property
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "id": "http://example.edu/credentials/3732",
  "type": ["VerifiableCredential", "UniversityDegreeCredential"],
  "issuer": "https://example.edu/issuers/14",
  "issuanceDate": "2010-01-01T19:23:24Z",
  "credentialSubject": {
    "id": "did:example:ebfeb1f712ebc6f1c276e12ec21",
    "degree": {
      "type": "BachelorDegree",
      "name": "Bachelor of Science and Arts"
    }
  },
  "proof": { ... }
}
```

> 注
>
> 预计本规范的下一版本将增加 validFrom 属性，并将废弃 issuanceDate 属性，改用新的 issuance 属性。这两个属性的取值范围预计将保持为[RFC3339]组合日期和时间字符串。实施者被告知，validFrom和issued属性是保留的，不鼓励用于任何其他目的。

### 4.7 证明(签名)

要使一个凭证或展示成为可验证凭证或可验证演示，必须至少表达一种证明机制，以及评估该证明所需的细节；也就是可验证。

本规范确定了两类证明机制：外部证明和嵌入式证明。外部证明是一种包装该数据模型表达式的证明，如JSON Web Token，这在§6.3.1 JSON Web Token节中有详细说明。嵌入证明是一种将证明包含在数据中的机制，比如关联数据签名，这将在§6.3.2关联数据证明中阐述。

当嵌入证明时，必须使用证明属性。

**proof**

一个或多个加密证明，可用于检测篡改和验证证书或展示的作者身份。嵌入式证明所使用的具体方法必须使用类型属性包含在内。

因为数学证明所使用的方法因表示语言和所使用的技术而不同，所以作为证明属性的值的名值对的集合也会相应变化。例如，如果数字签名用于证明机制，则证明属性的名值对预计包括签名、签名实体的引用和签名日期的表示。下面的例子使用了RSA数字签名。

```json
EXAMPLE 11: Usage of the proof property on a verifiable credential
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "id": "http://example.gov/credentials/3732",
  "type": ["VerifiableCredential", "UniversityDegreeCredential"],
  "issuer": "https://example.edu",
  "issuanceDate": "2010-01-01T19:73:24Z",
  "credentialSubject": {
    "id": "did:example:ebfeb1f712ebc6f1c276e12ec21",
    "degree": {
      "type": "BachelorDegree",
      "name": "Bachelor of Science and Arts"
    }
  },
  "proof": {
    "type": "RsaSignature2018",
    "created": "2018-06-18T21:19:10Z",
    "proofPurpose": "assertionMethod",
    "verificationMethod": "https://example.com/jdoe/keys/1",
    "jws": "eyJhbGciOiJQUzI1NiIsImI2NCI6ZmFsc2UsImNyaXQiOlsiYjY0Il19
      ..DJBMvvFAIC00nSGB6Tn0XKbbF9XrsaJZREWvR2aONYTQQxnyXirtXnlewJMB
      Bn2h9hfcGZrvnC1b6PgWmukzFJ1IiH1dWgnDIS81BH-IxXnPkbuYDeySorc4
      QU9MJxdVkY5EL4HYbcIfwKj6X4LBQ2_ZHZIu1jdqLcRZqHcsDF5KKylKc1TH
      n5VRWy5WhYg_gBnyWny8E6Qkrze53MR7OuAmmNJ1m1nN8SxDrG6a08L78J0-
      Fbas5OjAQz3c17GY8mVuDPOBIOVjMEghBlgl3nOi1ysxbRGhHLEK4s0KKbeR
      ogZdgt1DkQxDFxxn41QWDw_mmMCjs9qxg0zcZzqEJw"
  }
}
```

> 注
>
> 正如在第1.4节一致性中所讨论的那样，有多种可行的证明机制，本规范不对可验证凭证使用的任何单一证明机制进行标准化，也不推荐。关于证明机制的更多信息，请参见以下规范。关联数据证明[LD-PROOFS]、关联数据签名[LD-SIGNATURES]、2018年RSA签名套件[LDS-RSA2018]和JSON网络签名（JWS）未编码有效载荷选项[RFC7797]。可验证凭证扩展注册表[VC-EXTENSION-REGISTRY]中提供了证明机制的清单。

### 4.8 有效期

本规范定义了用于表达凭证到期信息的 expirationDate 属性。

**expirationDate**

如果存在，则 expirationDate 属性的值必须是一个 [RFC3339] 组合日期和时间字符串的字符串值，表示凭证停止有效的日期和时间。

```json
EXAMPLE 12: Usage of the expirationDate property
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "id": "http://example.edu/credentials/3732",
  "type": ["VerifiableCredential", "UniversityDegreeCredential"],
  "issuer": "https://example.edu/issuers/14",
  "issuanceDate": "2010-01-01T19:23:24Z",
  "expirationDate": "2020-01-01T19:23:24Z",
  "credentialSubject": {
    "id": "did:example:ebfeb1f712ebc6f1c276e12ec21",
    "degree": {
      "type": "BachelorDegree",
      "name": "Bachelor of Science and Arts"
    }
  },
  "proof": { ... }
}
```

> 注
>
> 预计本规范的下一个版本将以废弃的方式添加 validUntil 属性，但保留与 expirationDate 属性的向后兼容性。建议实施者保留 validUntil 属性，不鼓励将其用于任何其他目的。

### 4.9 状态

本规范定义了以下 credentialStatus 属性，用于发现关于可验证凭证当前状态的信息，例如它是被暂停还是被撤销。

**credentialStatus**

credentialStatus 属性的值必须包括:
- id 属性，它必须是一个 URL。
- type 属性，它表示凭证状态类型（也称为凭证状态方法）。预计该值将提供足够的信息来确定凭证的当前状态。例如，该对象可以包含一个指向外部文档的链接，指出该凭证是否被暂停或撤销。

凭证状态信息的确切内容由具体的credentialStatus类型定义决定，并因其是否简单实现或是否是隐私增强等因素而异。

```json
EXAMPLE 13: Usage of the status property
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "id": "http://example.edu/credentials/3732",
  "type": ["VerifiableCredential", "UniversityDegreeCredential"],
  "issuer": "https://example.edu/issuers/14",
  "issuanceDate": "2010-01-01T19:23:24Z",
  "credentialSubject": {
    "id": "did:example:ebfeb1f712ebc6f1c276e12ec21",
    "degree": {
      "type": "BachelorDegree",
      "name": "Bachelor of Science and Arts"
    }
  },
  "credentialStatus": {
    "id": "https://example.edu/status/24",
    "type": "CredentialStatusList2017"
  },
  "proof": { ... }
}
```

定义状态方案的数据模型、格式和协议不属于本规范的范围。存在一个可验证的凭证扩展注册表[VC-EXTENSION-REGISTRY]，其中包含了可供希望实现可验证的凭证状态检查的实施者使用的状态方案。

### 4.10 展示

可使用展示来合并和展示凭证。它们的包装方式可以使数据的作者身份可以核实。演示文稿中的数据往往都是关于同一主体的，但对数据中的主体或签发人的数量没有限制。对多个可验证凭证的信息进行汇总，是可验证演示的典型用途。

一个可验证展示通常由以下属性组成。

**id**

id 属性是可选的，可用于为演示提供唯一的标识符。关于此属性的使用详情，请参见第 4.2 节标识符。

**type**

type属性是必需的，它表达了演示的类型，例如 VerifiablePresentation。有关使用此属性的细节，请参见第 4.3 节类型。

**verifiableCredential**

如果存在，则 verifiableCredential 属性的值必须由一个或多个可验证凭证，或由可验证凭证派生的数据以加密可验证的格式构造。

**holder**

如果存在，持有人属性的值预计是生成演示文稿的实体的URI。

**proof**

如果存在，证明属性的值可以确保演示是可验证的。关于这个属性的使用的细节，请看§4.7证明（签名）。

下面的例子显示了一个嵌入了可验证凭证的可验证展示：

```json
EXAMPLE 14: Basic structure of a presentation
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "id": "urn:uuid:3978344f-8596-4c3a-a978-8fcaba3903c5",
  "type": ["VerifiablePresentation", "CredentialManagerPresentation"],
  "verifiableCredential": [{ ... }],
  "proof": [{ ... }]
}
```

上面显示的verifiableCredential属性的内容是可验证凭证，正如本规范所描述的那样。证明属性的内容是证明，正如关联数据证明[LD-PROOFS]规范所描述的那样。在§6.3.1 JSON Web Token中给出了一个使用JWT证明机制的可验证演示的例子。

#### 使用衍生凭证的展示

一些零知识密码学方案可能使持有人能够间接证明他们持有可验证凭证的权利主张，而不透露可验证凭证本身。在这些方案中，来自可验证凭证的权利要求可能被用来推导出一个呈现的值，这个值是经过密码学论证的，如果合眼人信任发行者，就可以信任这个值。

例如，包含主张出生日期的可验证凭证可用于导出15岁以上的呈报值，该呈报值是以密码学方式验证的。也就是说，如果核查者信任签发人，他们仍然可以信任所得出的值。

> 注
>
> 关于包含派生数据而非直接嵌入可验证凭证的ZKP式可验证演示的例子，请参见§5.8零知识证明。
>

使用零知识证明的选择性披露方案可以使用该模型中表达的权利要求来证明关于这些权利要求的附加声明。例如，指定主体出生日期的权利要求可以作为谓词，证明主体的年龄在给定的范围内，从而证明主体有资格获得与年龄相关的折扣，而不实际揭示主体的出生日期。持有人可以灵活地以任何适用于所需的可核查表述的方式使用该主张。

![Pat has a property             dateOfBirth whose value is 2010-01-01T19:73:24Z](https://w3c.github.io/vc-data-model/diagrams/claim-example-2.svg)

*图9 表示Pat的出生日期为2010-01-01T19:23:24Z的基本权利要求。日期编码将由模式决定。*

## 5、高级概念

在第4节介绍的概念的基础上，本节将探讨有关可验证凭证的更复杂的问题。基本概念中介绍的概念的基础上，本节将探讨有关可验证凭证的更复杂的主题。

### 5.1 生命周期细节

本节是非规范性的。

第1.2节生态系统概述提供了可验证凭证生态系统的概述。本节更详细地介绍了设想中的生态系统的运作方式。

![该图显示了凭证如何从发行者流向持有者，以及可选地从一个持有者流向另一持有者； 以及展示如何从持有人流向验证人，各方都可以使用逻辑可验证数据注册表中的信息](https://w3c.github.io/vc-data-model/diagrams/ecosystemdetail.svg)

*图10 本规范的角色和信息流。*

可验证凭证生态系统中的角色和信息流如下：

- 签发人向持有人签发可验证凭证。签发总是发生在涉及凭证的任何其他行动之前。
- 持有人可以将其一个或多个可验证凭证转让给另一个持有人。
- 持有人将其一个或多个可验证凭证提交给核验人，可选择在一个可验证展示中。
- 核验人核实所提交的可验证展示和可验证凭证的真实性。这应该包括检查凭证状态，以撤销可验证凭证。
- 签发人可能会撤销一个可验证凭证。
- 持有人可能会删除一个可验证凭证。

> 注意
>
> 上述操作的顺序不是固定的，某些操作可能会执行不止一次。这种动作重复可能是立即发生的，也可能在以后发生。

最常见的行动操作顺序是：

1. 签发人向持有人发行

2. 持有人向核验人提交

3. 核验人进行核查

本规范没有定义传输可验证凭证或可验证展示的任何协议，但假设其他规范确实规定了实体之间如何传输这些凭证或展示，那么本可验证凭证数据模型可直接适用。

本规范也没有定义授权框架，也没有定义核验人在验证可验证凭证或可验证展示后可能做出的决定，要考虑到可验证凭证的持有人、可验证凭证的签发人、可验证凭证的内容以及自身的政策。

特别是§5.6使用条款和§C.主体与持有人的关系两节规定了验证者如何确定。

- 持有人是否是可验证凭证的主体。
- 主体与持有人之间的关系。
- 原始持有人是否将可验证凭证传给了后续持有人。
- 持有人或验证人对使用可验证凭证的任何限制。



### 5.2 信任模式

本节是非规范化的。

可验证凭证信任模型如下：

- 核验人相信签发人会签发它所收到的凭证。为了建立这种信任，一个凭证要具备以下两种情况：

  - 包括一个证明，证明签发人生成了证书（即是一个可验证证书），或者：
  - 传送方式明确证明签发人生成了可验证凭证，而且可验证凭证在传输或储存过程中没有被篡改。这种信任可能会被削弱，这取决于核验人的风险评估。

- 所有实体都相信，可验证数据登记表是不可篡改的，是正确记录哪些数据由哪些实体控制的。

- 持有人和核验人相信签发人会发布关于主体的真实（即不是虚假）凭证，并在适当的时候迅速撤销。

- 持有人相信存储库会安全地存储凭证，不会将凭证发布给除持有人以外的任何人，也不会在其保管期间损坏或丢失凭证。

这种信任模式区别于其他信任模式，它确保了：

- 签发人和核验人不需要信任存储库。
- 签发人不需要了解或信任核验人。

通过将身份提供者和依赖方之间的信任脱钩，建立了一个更加灵活和动态的信任模式，从而增加了市场竞争和客户选择。

关于该信任模式如何与工作组研究的各种威胁模式互动的更多信息，请参见《可验证凭证使用案例》文件[VC-USECASES]。

> 注
>
> 本规范中详述的数据模型并不意味着是一种过渡性的信任模型，如传统的证书颁发机构信任模型所提供的模型。在可验证凭证数据模型中，核验人要么直接信任签发人，要么不信任签发人。虽然可以使用可验证凭证数据模型建立跨式信任模型，但敦促实施者了解以证书颁发机构系统所采用的方式广泛委托信任所带来的安全弱点。

### 5.3 可扩展性

可验证凭证数据模型的目标之一是实现无许可创新。为实现这一目标，数据模型需要以多种不同方式进行扩展。该数据模型需要：

- 通过使用基于图的数据模型，对复杂的多实体关系进行建模。
- 通过使用[LINKED-DATA]，扩展用于描述数据模型中信息的机器可读词汇，而不需要使用一个集中的系统来进行扩展。
- 通过使用关联数据证明[LD-PROOFS]、关联数据签名[LD-SIGNATURES]以及各种签名套件，支持多种类型的加密证明格式。
- 以一种深受软件开发者和网页作者欢迎的数据格式提供上述所有的可扩展性机制，并通过使用[JSON-LD]来实现。

这种数据建模的方法通常被称为开放世界假设，这意味着任何实体都可以对任何其他实体说任何话。虽然这种方法似乎与构建简单和可预测的软件系统相冲突，但与封闭的软件系统相比，开放世界假设的可扩展性与程序正确性之间的平衡总是更具挑战性。

本节的其余部分将通过一系列的例子来描述如何同时实现可扩展性和程序正确性。

让我们假设从下面的可验证凭证开始。

```json
EXAMPLE 15: A simple credential
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "id": "http://example.com/credentials/4643",
  "type": ["VerifiableCredential"],
  "issuer": "https://example.com/issuers/14",
  "issuanceDate": "2018-02-24T05:28:04Z",
  "credentialSubject": {
    "id": "did:example:abcdef1234567",
    "name": "Jane Doe"
  },
  "proof": { ... }
}
```

这个可验证的凭证说明与 `did:example:abcdef1234567` 相关联的实体有一个值为 Jane Doe 的名字。

现在让我们假设一个开发者想要扩展可验证的凭证来存储两个额外的信息：一个内部企业参考号，以及Jane最喜欢的食物。

首先要做的是创建一个包含两个新术语的JSON-LD上下文，如下所示。

```json
EXAMPLE 16: A JSON-LD context
{
  "@context": {
    "referenceNumber": "https://example.com/vocab#referenceNumber",
    "favoriteFood": "https://example.com/vocab#favoriteFood"
  }
}
```

在创建了这个JSON-LD上下文后，开发者将其发布在某个地方，以便将处理可验证凭证的验证者可以访问它。假设上面的JSON-LD上下文发布在`https://example.com/contexts/mycontext.jsonld`，我们可以通过包含上下文并为可验证凭证添加新的属性和凭证类型来扩展这个例子。

```json
EXAMPLE 17: A verifiable credential with a custom extension
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://example.com/contexts/mycontext.jsonld"
  ],
  "id": "http://example.com/credentials/4643",
  "type": ["VerifiableCredential", "CustomExt12"],
  "issuer": "https://example.com/issuers/14",
  "issuanceDate": "2018-02-24T05:28:04Z",
  "referenceNumber": 83294847,
  "credentialSubject": {
    "id": "did:example:abcdef1234567",
    "name": "Jane Doe",
    "favoriteFood": "Papaya"
  },
  "proof": { ... }
}
```

这个例子展示了以无权限和分散的方式扩展可验证凭证数据模型。所展示的机制还确保了以这种方式创建的可验证凭证提供了一种防止命名空间冲突和语义模糊的机制。

像这样的动态可扩展性模型确实增加了实施负担。为这种系统编写的软件必须根据应用的风险状况来决定是否可以接受带有扩展的可验证凭证。有些应用程序可能只接受某些扩展，而高度安全的环境可能不接受任何扩展。这些决定是由这些应用的开发者决定的，特别是不属于本规范的范围。

开发者被敦促确保扩展JSON-LD上下文是高度可用的。不能获取上下文的实现将产生错误。确保扩展JSON-LD上下文始终可用的策略包括为上下文使用内容地址的URL，将上下文文档与实现捆绑在一起，或启用积极的上下文缓存。

建议实现者密切关注本规范中的扩展点，如§4.7证明（签名）、§4.9状态、§5.4数据模式、§5.5刷新、§5.6使用条款和§5.7证据。虽然本规范没有定义这些扩展点的具体实现，但可验证凭证扩展注册处[VC-EXTENSION-REGISTRY]提供了一个非官方的、经过整理的扩展列表，开发人员可以从这些扩展点中使用。

#### 5.3.1 语义互操作性

本规范确保 "纯 "JSON和JSON-LD语法在语义上兼容，而不要求JSON实现使用JSON-LD处理器。为了达到这个目的，本规范对这两种语法提出了以下附加要求。

- 基于JSON的处理器必须处理@context键，确保预期的值按照被处理的证书类型的预期顺序存在。这个顺序很重要，因为在凭证中使用的键，是使用与@context相关联的值来定义的，是使用 "先定义的赢 "机制来定义的，改变顺序可能会导致不同的键定义 "赢"。
- 当JSON-LD上下文重新定义活动上下文中的任何术语时，基于JSON-LD的处理器必须产生一个错误。改变现有术语定义的唯一方法是引入一个新术语，在该新术语的范围内清除活动上下文。对该功能感兴趣的作者应该阅读JSON-LD 1.1规范中的@保护功能。

任何寻求互操作性的实现者都应该发布一个人可读的文档，描述 @context 属性的预期值顺序。寻求互操作性的JSON-LD实现者预计将在@context属性中指定的URL上发布一个机器可读的描述（即一个正常的JSON-LD Context文档）。

上述要求保证了JSON和JSON-LD之间对于@context机制定义的术语的语义互操作性。虽然JSON-LD处理器将使用所提供的特定机制，并能验证所有术语是否正确指定，但基于JSON的处理器隐含地接受同样的术语集，而不测试它们是否正确。换句话说，对于JSON和JSON-LD来说，数据交换发生的上下文是通过使用相同的机制来明确说明的。对于基于JSON的处理器，这是以轻量级的方式实现的，无需使用JSON-LD处理库。

### 5.4 数据模式

当对给定的数据集合实施特定结构时，数据模式是有用的。本规范考虑的数据模式至少有两种类型。

- 数据验证模式，用于验证可验证凭证的结构和内容是否符合发布的模式。
- 数据编码模式，用于将可验证凭证的内容映射到另一种表示格式，如零知识证明中使用的二进制格式。

需要理解的是，数据模式的作用与@context属性不同，@context属性既不强制执行数据结构或数据语法，也不能将任意编码定义为替代的表示格式。

本规范为数据模式的表达定义了以下属性：

**credentialSchema**

credentialSchema属性的值必须是一个或多个数据模式，这些数据模式为验证者提供足够的信息，以确定所提供的数据是否符合所提供的模式。每个credentialSchema必须指定其类型（例如，JsonSchemaValidator2018），以及一个id属性，该属性必须是一个识别模式文件的URI。每个数据模式的精确内容由具体的类型定义决定。

> 注
>
> credentialSchema 属性提供了对类型定义进行注释或将其锁定为词汇的特定版本的机会。可验证凭证的作者可以使用 credentialSchema 包含他们词汇的静态版本，该版本被锁定为某些内容完整性保护机制。credentialSchema属性还可以对凭证进行语法检查，并使用JSON Schema[JSON-SCHEMA-2018]验证机制。

```json
EXAMPLE 18: Usage of the credentialSchema property to perform JSON schema validation
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "id": "http://example.edu/credentials/3732",
  "type": ["VerifiableCredential", "UniversityDegreeCredential"],
  "issuer": "https://example.edu/issuers/14",
  "issuanceDate": "2010-01-01T19:23:24Z",
  "credentialSubject": {
    "id": "did:example:ebfeb1f712ebc6f1c276e12ec21",
    "degree": {
      "type": "BachelorDegree",
      "name": "Bachelor of Science and Arts"
    }
  },
  "credentialSchema": {
    "id": "https://example.org/examples/degree.json",
    "type": "JsonSchemaValidator2018"
  },
  "proof": { ... }
}
```

在上面的例子中，发行人指定了一个credentialSchema，它指向一个[JSON-SCHEMA-2018]文件，该文件可以被验证者用来确定可验证凭证是否形成良好。

> 注
>
> 关于与JSON模式[JSON-SCHEMA-2018]或其他可选验证机制的联系，请参见《可验证凭证实施指南》[VC-IMP-GUIDE]文档。
>

数据模式也可用于指定到其他二进制格式的映射，例如用于执行零知识证明的格式。关于在零知识证明中使用 credentialSchema 属性的更多信息，请参阅第 5.8 节零知识证明。

```json
EXAMPLE 19: Usage of the credentialSchema property to perform zero-knowledge validation
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "id": "http://example.edu/credentials/3732",
  "type": ["VerifiableCredential", "UniversityDegreeCredential"],
  "issuer": "https://example.edu/issuers/14",
  "issuanceDate": "2010-01-01T19:23:24Z",
  "credentialSubject": {
    "id": "did:example:ebfeb1f712ebc6f1c276e12ec21",
    "degree": {
      "type": "BachelorDegree",
      "name": "Bachelor of Science and Arts"
    }
  },
  "credentialSchema": {
    "id": "https://example.org/examples/degree.zkp",
    "type": "ZkpExampleSchema2018"
  },
  "proof": { ... }
}
```

在上面的例子中，发行人指定了一个指向零知识包装的二进制数据格式的凭证Schema，它能够将输入的数据转化为一种格式，然后验证者可以使用这种格式来确定可验证凭证提供的证明是否有效。

### 5.5 刷新

系统可以手动或自动刷新过期的可验证凭证，这很有用。关于过期的可验证凭证的更多信息，请参阅第 4.8 节过期。本规范定义了一个 refreshService 属性，它使发行人能够包含一个到刷新服务的链接。

如果可验证凭证的对象是核验人或持有人（或两者），签发人可以将刷新服务作为一个元素包含在可验证凭证中，如果只针对持有人，则可以将其包含在可验证演示中。在后一种情况下，这使持有人能够在创建可验证演示与验证人共享之前刷新可验证凭证。在前一种情况下，将刷新服务包含在可验证凭证中，使持有人或核验人能够对凭证进行未来的更新。

只有当凭证已过期或签发人不公布凭证状态信息时，才会使用刷新服务。建议签发人不要将 refreshService 属性放在不包含公开信息的可验证凭证中，或者其刷新服务没有受到某种保护。

> 注
>
> 在可验证凭证中放置一个refreshService属性，使其可供核验人使用，可以解除持有人的控制和同意，让可验证凭证直接发给核验人，从而绕过持有人。
>

**refreshService**

refreshService属性的值MUST是一个或多个刷新服务，它向接收者的软件提供足够的信息，以便接收者能够刷新可验证的凭证。每个refreshService值MUST指定其类型（例如，ManualRefreshService2018）和其id，即服务的URL。每个刷新服务的精确内容由具体的刷新服务类型定义决定。

```json
EXAMPLE 20: Usage of the refreshService property by an issuer
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "id": "http://example.edu/credentials/3732",
  "type": ["VerifiableCredential", "UniversityDegreeCredential"],
  "issuer": "https://example.edu/issuers/14",
  "issuanceDate": "2010-01-01T19:23:24Z",
  "credentialSubject": {
    "id": "did:example:ebfeb1f712ebc6f1c276e12ec21",
    "degree": {
      "type": "BachelorDegree",
      "name": "Bachelor of Science and Arts"
    }
  },
  "refreshService": {
    "id": "https://example.edu/refresh/3732"
    "type": "ManualRefreshService2018",
  },
  "proof": { ... }
}
```

在上面的例子中，发行人指定了一个手动刷新服务(manual refreshService)，可以通过引导持有人或验证人访问`https://example.edu/refresh/3732`。

### 5.6 使用条款

签发人或持有人可利用使用条款来传达签发可验证凭证或可验证展示的条款。签发人将其使用条款置于可验证凭证内。持有人将其使用条款置于可验证展示中。本规范定义了一个用于表达使用条款信息的 termsOfUse 属性。

termsOfUse 属性的值告诉核验人，如果它要接受可验证凭证或可验证展示，那么它需要执行（义务）、不允许执行（禁止）或允许执行（允许）哪些操作。

> 注
>
> 需要进一步研究，以确定非持有人的主体如何将使用条款放在其可验证凭证上。一种方法是主体可以要求签发人将使用条款放在已签发的可验证凭证中。另一种方式是主体将可验证凭证委托给持有人，并对委托的可验证凭证设置使用条款限制。
>

**termsOfUse**

termsOfUse 属性的值必须指定一个或多个使用条款政策，创建者根据这些政策发布凭证或展示。如果接受者（持有人或验证者）不愿意遵守指定的使用条款，那么他们要自己负责，如果违反了声明的使用条款，可能会承担法律责任。每个 termsOfUse 值必须指定其类型，例如 IssuerPolicy，并可指定其实例 id。每个使用条款的精确内容由具体的 termsOfUse 类型定义决定。

```json
EXAMPLE 21: Usage of the termsOfUse property by an issuer
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "id": "http://example.edu/credentials/3732",
  "type": ["VerifiableCredential", "UniversityDegreeCredential"],
  "issuer": "https://example.edu/issuers/14",
  "issuanceDate": "2010-01-01T19:23:24Z",
  "credentialSubject": {
    "id": "did:example:ebfeb1f712ebc6f1c276e12ec21",
    "degree": {
      "type": "BachelorDegree",
      "name": "Bachelor of Science and Arts"
    }
  },
  "termsOfUse": [{
    "type": "IssuerPolicy",
    "id": "http://example.com/policies/credential/4",
    "profile": "http://example.com/profiles/credential",
    "prohibition": [{
      "assigner": "https://example.edu/issuers/14",
      "assignee": "AllVerifiers",
      "target": "http://example.edu/credentials/3732",
      "action": ["Archival"]
    }]
  },
  "proof": { ... }
}
```

在上面的例子中，签发人(转让人)是禁止核验人(受让人)将数据存储在档案中。

```json
EXAMPLE 22: Usage of the termsOfUse property by a holder
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "id": "did:example:ebfeb1f712ebc6f1c276e12ec21",
  "type": ["VerifiablePresentation"],
  "verifiableCredential": [{
    "@context": [
      "https://www.w3.org/2018/credentials/v1",
      "https://www.w3.org/2018/credentials/examples/v1"
    ],
    "id": "http://example.edu/credentials/3732",
    "type": ["VerifiableCredential", "UniversityDegreeCredential"],
    "issuer": "https://example.edu/issuers/14",
    "issuanceDate": "2010-01-01T19:23:24Z",
    "credentialSubject": {
      "id": "did:example:ebfeb1f712ebc6f1c276e12ec21",
      "degree": {
      "type": "BachelorDegree",
      "name": "Bachelor of Science and Arts"
    }
    },
    "proof": { ... }
  }],
  "termsOfUse": [{
    "type": "HolderPolicy",
    "id": "http://example.com/policies/credential/6",
    "profile": "http://example.com/profiles/credential",
    "prohibition": [{
      "assigner": "did:example:ebfeb1f712ebc6f1c276e12ec21",
      "assignee": "https://wineonline.example.org/",
      "target": "http://example.edu/credentials/3732",
      "action": ["3rdPartyCorrelation"]
    }]
  },
  "proof": [ ... ]
}
```

在上面的例子中，持有人（转让人）同时也是主体，他表达了一个使用条款，禁止核验人（受让人）使用所提供的信息，利用第三方服务对持有人或主体进行关联。如果核验人要使用第三方服务进行关联，就会违反持有人创建展示的条款。

这一功能也有望被政府发行的可验证凭证用来指示数字钱包将其使用范围限制在类似的政府组织，以保护公民免受敏感数据的意外使用。同样，一些由私营行业发行的可验证凭证预计也会将使用范围限制在组织内部的部门内，或在工作时间内。促请实施者在《可验证凭证实施指南》[VC-IMP-GUIDE]文件的适当章节中阅读更多关于这一快速发展的特征。

### 5.7 证据

签发人可以列入证据，向核验人提供可验证凭证中的补充证明资料。核验人可利用这些证据来确定其对可验证凭证中的说法是否有信心。

例如，签发人可以在签发凭证之前检查主体提供的实物文件或进行一系列背景调查。在某些情况下，当确定依赖给定凭证的相关风险时，这些信息对核验人是有用的。

本规范定义了用于表达证据信息的证据属性。

**evidence**

证据财产的价值必须是一个或多个证据计划，提供足够的信息，使核查人员能够确定签发人收集的证据是否符合其依赖凭证的信任要求。每个证据方案由其类型标识。id 属性是可选的，但如果存在，则应包含一个 URL，该 URL 指向可以找到有关该证据实例的更多信息的地方。每个证据方案的精确内容由特定证据类型定义决定。

> 注
>
> 有关规范如何支持对凭证和非凭证数据的附件和引用的信息，请参见《可验证凭证实施指南》[VC-IMP-GUIDE]文档。

```json
EXAMPLE 23: Usage of the evidence property
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "id": "http://example.edu/credentials/3732",
  "type": ["VerifiableCredential", "UniversityDegreeCredential"],
  "issuer": "https://example.edu/issuers/14",
  "issuanceDate": "2010-01-01T19:23:24Z",
  "credentialSubject": {
    "id": "did:example:ebfeb1f712ebc6f1c276e12ec21",
    "degree": {
      "type": "BachelorDegree",
      "name": "Bachelor of Science and Arts"
    }
  },
  "evidence": [{
    "id": "https://example.edu/evidence/f2aeec97-fc0d-42bf-8ca7-0548192d4231",
    "type": ["DocumentVerification"],
    "verifier": "https://example.edu/issuers/14",
    "evidenceDocument": "DriversLicense",
    "subjectPresence": "Physical",
    "documentPresence": "Physical"
  },{
    "id": "https://example.edu/evidence/f2aeec97-fc0d-42bf-8ca7-0548192dxyzab",
    "type": ["SupportingActivity"],
    "verifier": "https://example.edu/issuers/14",
    "evidenceDocument": "Fluid Dynamics Focus",
    "subjectPresence": "Digital",
    "documentPresence": "Digital"
  }],
  "proof": { ... }
}
```

> 注
>
> 证据属性提供与证明属性不同的补充信息。证据属性用于表达与可验证凭证的完整性有关的证明信息，如文件证据。与此相反，证明属性用于表达与发行人的真实性和可验证凭证的完整性有关的机器可验证的数学证明。关于证明属性的更多信息，请参见§4.7证明（签名）。

### 5.8 零知识证明

零知识证明是一种密码学方法，在这种方法中，一个实体可以向另一个实体证明他们知道某个值，而不透露实际值。一个现实世界的例子是证明一所经认可的大学已经授予你一个学位，而不透露你的身份或学位上包含的任何其他个人身份信息。

零知识证明机制引入的关键能力是持有人能够：

- 将来自多个发行人的多个可验证凭证组合成一个可验证展示，而不向核验人透露可验证凭证或主体标识。这使核验人更难与任何一个签发人就签发的可验证凭证进行串通。
- 有选择地向核验人披露可验证凭证中的主张，而不需要签发多个原子可验证凭证。这使得持有人可以向核验人提供他们所需要的准确信息，而不是更多。
- 产生一个派生的可验证凭证，该凭证是根据核验人的数据模式而不是签发人的数据模式进行格式化的，而不需要在签发可验证凭证后让签发人参与。这就为持有人使用其签发的可验证凭证提供了很大的灵活性。

本规范描述了一个支持零知识证明机制的数据模型。下面的示例强调了如何使用该数据模型来发行、出示和验证零知识可验证凭证。

要使用零知识可验证凭证，签法人必须以使持有人能够以增强隐私的方式向核验人展示信息的方式发行可验证凭证。这意味着持有人可以在不透露被签署的值，或者只透露某些选定的值时，证明签发人签名的有效性。标准的做法是通过证明对签名的了解，而不透露签名本身。当可验证凭证要用于零知识证明系统时，对其有两个要求。可验证凭证必须包含一个。

- 凭证的定义，使用credentialSchema属性， 可以被各方使用，以执行各种加密操作 在零知识。
- 证明，使用证明属性，可以用来推导出可验证展示，在零知识中呈现原始可验证凭证中包含的信息。零知识可验证的呈现方式必须不透露任何非持有人有意透露的信息。

下面的例子展示了一种在零知识中使用可验证凭证的方法。它利用CL签名，通过使用选择性地披露可验证凭证值，以支持持有人和主体隐私的方式展示可验证凭证。

```json
示例 24：支持 CL 签名的可验证凭证
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "type": ["VerifiableCredential", "UniversityDegreeCredential"],
  "credentialSchema": {
    "id": "did:example:cdf:35LB7w9ueWbagPL94T9bMLtyXDj9pX5o",
    "type": "did:example:schema:22KpkXgecryx9k7N6XN1QoN3gXwBkSU8SfyyYQG"
  },
  "issuer": "did:example:Wz4eUg7SetGfaUVCn8U9d62oDYrUJLuUtcy619",
  "credentialSubject": {
    "givenName": "Jane",
    "familyName": "Doe",
    "degree": {
      "type": "BachelorDegree",
      "name": "Bachelor of Science and Arts",
      "college": "College of Engineering"
    }
  },
  "proof": {
    "type": "CLSignature2019",
    "issuerData": "5NQ4TgzNfSQxoLzf2d5AV3JNiCdMaTgm...BXiX5UggB381QU7ZCgqWivUmy4D",
    "attributes": "pPYmqDvwwWBDPNykXVrBtKdsJDeZUGFA...tTERiLqsZ5oxCoCSodPQaggkDJy",
    "signature": "8eGWSiTiWtEA8WnBwX4T259STpxpRKuk...kpFnikqqSP3GMW7mVxC4chxFhVs",
    "signatureCorrectnessProof": "SNQbW3u1QV5q89qhxA1xyVqFa6jCrKwv...dsRypyuGGK3RhhBUvH1tPEL8orH"
  }
}
```

上面的例子通过使用 credentialSchema 属性和一个可用于 Camenisch-Lysyanskaya 零知识证明系统的特定证明来提供可验证凭证定义。

下一个例子利用上面的可验证凭证来生成一个新的具有隐私保护证明的派生可验证凭证。然后将派生的可验证凭证放在一个可验证展示中，进一步证明整个断言是有效的。大多数可验证的呈现方式在零知识系统中使用时，有三个要求。

- 每个可验证展示中的派生可验证凭证 都必须有一个凭证结构属性。这允许派生的可验证凭证引用用于生成派生证明的凭证定义。
- 可验证演示必须不泄漏信息，使核验人能够在多个可验证展示中关联持有人。
- 可验证演示必须包含一个证明属性，使核验人能够确定可验证展示中的所有派生可验证凭证都是发给同一持有人的，而不会泄露持有人不打算分享的个人身份信息。

```json
例子25：支持CL签名的可验证展示
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "type": "VerifiablePresentation",
  "verifiableCredential": [
    {
      "@context": [
        "https://www.w3.org/2018/credentials/v1",
        "https://www.w3.org/2018/credentials/examples/v1"
      ],
      "type": ["VerifiableCredential", "UniversityDegreeCredential"],
      "credentialSchema": {
        "id": "did:example:cdf:35LB7w9ueWbagPL94T9bMLtyXDj9pX5o",
        "type": "did:example:schema:22KpkXgecryx9k7N6XN1QoN3gXwBkSU8SfyyYQG"
      },
      "issuer": "did:example:Wz4eUg7SetGfaUVCn8U9d62oDYrUJLuUtcy619",
      "credentialSubject": {
        "degreeType": "BachelorDegree",
        "degreeSchool": "College of Engineering"
      },
      "proof": {
        "type": "AnonCredDerivedCredentialv1",
        "primaryProof": "cg7wLNSi48K5qNyAVMwdYqVHSMv1Ur8i...Fg2ZvWF6zGvcSAsym2sgSk737",
        "nonRevocationProof": "mu6fg24MfJPU1HvSXsf3ybzKARib4WxG...RSce53M6UwQCxYshCuS3d2h"
      }
  }],
  "proof": {
    "type": "AnonCredPresentationProofv1",
    "proofValue": "DgYdYMUYHURJLD7xdnWRinqWCEY5u5fK...j915Lt3hMzLHoPiPQ9sSVfRrs1D"
  }
}
```

![](https://w3c.github.io/vc-data-model/diagrams/zkp-cred-pres.svg)

*图11 ZKP展示中凭证和派生凭证之间关系的直观例子。*

> 注
>
> 关于凭证定义的格式和证明的重要细节被故意省略，因为它们不在本文档的范围内。本节的目的是指导那些想要扩展可验证凭证和可验证展示以支持零知识证明系统的实施者。

### 5.9 争议

对于一个实体来说，如果想对签发人签发的凭证提出异议，至少有两种不同的情况需要考虑。

- 一个主体对签发人提出的要求提出异议。例如，地址属性不正确或过时。
- 一个实体对签发人对另一个主体作出的可能是虚假的声明提出异议。例如，一个冒名顶替的人声称是一个实体的社会安全号码。

除了 `DisputeCredential` 属性中的 `credentialSubject` 标识符是有争议的凭证的标识符之外，发行 `DisputeCredential` 的机制与普通凭证相同。

例如，如果一个标识符为`https://example.org/credentials/245` 的凭证存在争议，主体可以签发如下所示的凭证，并将其与争议凭证一起提交给核验人。

```json
例子26：一个主体对一个证书有争议。
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "id": "http://example.com/credentials/123",
  "type": ["VerifiableCredential", "DisputeCredential"],
  "credentialSubject": {
    "id": "http://example.com/credentials/245",
    "currentStatus": "Disputed",
    "statusReason": {
      "value": "Address is out of date.",
      "lang": "en"
    },
  },
  "issuer": "https://example.com/people#me",
  "issuanceDate": "2017-12-05T14:27:42Z",
  "proof": { ... }
}
```

在上述可验证凭证中，发行人称争议可验证凭证中的地址是错误的。

> 注
> 如果一项凭证没有识别符，可使用内容标示的识别符来识别有争议的凭证。同样，内容地址标识符也可用于唯一标识个别索赔。

> 注
> 这一研究领域正在迅速发展，有兴趣发布质疑其他凭证真实性的凭证的开发者，请阅读《可验证凭证实施指南》[VC-IMP-GUIDE]文件中有关争议的部分。

### 5.10 授权

本节是非规范性的。

可验证凭证旨在作为可靠识别主体的一种手段。虽然人们认识到基于角色的访问控制（RBAC）和基于属性的访问控制（ABAC）依靠这种识别作为授权主体访问资源的手段，但本规范并没有为RBAC或ABAC提供完整的解决方案。如果没有配套的授权框架，授权不是本规范的合适用途。

工作组在制定本规范的过程中确实考虑了授权的使用情况，并正在继续开展这项工作，作为建立在本规范之上的一个架构层。

## 6. 语法







## 7. 隐私方面的考虑

本节是非规范性的。

本节详细介绍了在生产环境中部署可验证凭证数据模型的一般隐私考虑因素和具体隐私影响。

### 7.1 隐私权的范围

本节是非规范性的。

重要的是要认识到隐私的范围，从假名到强烈的身份识别，不一而足。根据不同的使用情况，人们对他们愿意提供什么信息以及可以从所提供的信息中获得什么信息有不同的舒适度。

![单杠，左侧为红色，中间为橙色，右侧为绿色。 红色带有文本“高度相关（全局ID），例如政府ID，送货地址，信用卡号”。 橙色的文本为“ Correlatable ia collusion（个人身份信息），例如姓名，生日，邮政编码”。 绿色的文字为“不相关（假名），例如21岁以上”。](https://w3c.github.io/vc-data-model/diagrams/privacy-spectrum.svg)

*图12 从假名到完全识别的隐私谱。*

例如，大多数人可能希望在购买酒类时保持匿名，因为所需的监管检查仅仅基于一个人是否超过特定年龄。另外，对于医生为病人开出的医疗处方，要求履行处方的药店更强烈地识别医疗专业人员和病人的身份。因此，并不存在一种适用于所有用例的隐私方法。隐私解决方案是针对具体使用案例的。

> 注
>
> 即使对于那些想在购酒时保持匿名的人来说，仍然可能需要带照片的身份证明，以向商家提供适当的保证。商家可能不需要知道你的姓名或其他细节（除了你超过特定年龄），但在许多情况下，仅有年龄证明可能仍不足以满足规定。
>

可验证凭证数据模型努力支持整个隐私范围，并不对任何特定交易的正确匿名程度采取哲学立场。以下各节为希望避免出现不利于隐私的特定情况的实施者提供指导。

### 7.2 个人身份信息

本节是非规范性的。

与存储在 credential.credentialSubject 字段中的可验证凭证相关联的数据在与核验人共享时，容易受到隐私侵犯。个人识别数据，如政府颁发的标识符、送货地址和全名，可以很容易地用于确定、跟踪和关联一个实体。即使是看起来不能识别个人身份的信息，如出生日期和邮政编码的组合，也有非常强大的关联和去匿名化能力。

强烈建议实施者在分享具有这类特征的数据时警告持有人。强烈建议签发人在可能的情况下提供保护隐私的可验证凭证。例如，当核验人想确定一个实体是否超过18岁时，发行ageOver可验证凭证而不是出生日期可验证凭证。

由于可验证凭证通常包含个人身份信息 (PII)，因此强烈建议实施者在存储和传输可验证凭证时使用能够保护数据不被不应访问的人访问的机制。可以考虑的机制包括传输层安全(TLS)或其他在传输过程中对数据进行加密的手段，以及加密或数据访问控制机制，以保护可核查凭证中处于静止状态的数据。

### 7.3 基于标识符的相关性

本节是非规范性的。

可验证凭证的主体使用credential.credentialSubject.id字段进行识别。当标识符长期存在或在多个网络域中使用时，用于识别主体的标识符会产生更大的相关性风险。

同样，披露凭证标识符(credential.id)会导致多个核验人，或一个签发人和一个核验人合谋关联持有人的情况。如果持有人想减少相关性，他们应该使用可验证凭证方案，允许在可验证的展示过程中隐藏标识符。这种方案期望持有人生成标识符，甚至可能允许向发行人隐藏标识符，同时仍将标识符嵌入可验证凭证中并进行签名。

如果在可验证凭证系统中，强抗关联性是一项要求，那么强烈建议标识符要么。

- 绑定到一个单一的来源

- 一次性使用

- 完全不用，而是用短命的、一次性使用的不记名信物代替。

### 7.4 基于签名的相关性
本节是非规范性的。

可验证凭证的内容使用credential.proof字段进行保护。当相同的值在一个以上的会话或域中使用，且该值不会改变时，该字段中的属性会产生更大的相关性风险。例子包括verificationMethod、created、proofPurpose和jws字段。

如果需要强大的抗相关性属性，建议每次使用第三方配对签名、零知识证明或组签名等技术重新生成签名值和元数据。

> 注
>
> 即使使用反相关签名，信息仍然可能包含在一个可验证的凭证中，从而破坏了所使用的密码学的反相关特性。

### 7.5 基于标识符的长期相关性

本节是非规范性的。

可验证凭证可能包含长期存在的标识符，可用于关联个人。这些类型的标识符包括主体标识符、电子邮件地址、政府颁发的标识符、组织颁发的标识符、地址、医疗保健生命体征、可验证凭证特有的JSON-LD上下文，以及许多其他类型的长期标识符。

向持有人提供软件的组织应努力查明可核查凭证中含有可用于关联个人的信息的字段，并在共享这些信息时向持有人发出警告。

### 7.6 设备指纹

本节是非规范性的。

在可验证凭证之外，还有一些机制被用来跟踪和关联互联网和网络上的个人。这些机制包括互联网协议(IP)地址跟踪、网络浏览器指纹、evercookies、广告网络跟踪器、移动网络位置信息和应用内全球定位系统(GPS)API。使用可验证的凭证不能阻止这些其他跟踪技术的使用。此外，当这些技术与可验证凭证一起使用时，可能会发现新的相关信息。例如，生日与GPS位置相结合，可用于在多个网站上对个人进行强关联。

建议在使用可验证凭证时，尊重隐私的系统应防止使用这些其他跟踪技术。在某些情况下，可能需要在代表持有人传送可核查凭证的设备上禁用跟踪技术。

### 7.7 赞成抽象主张

本节是非规范性的。

为了使可验证凭证的接受者能够在各种情况下使用这些凭证，而不透露超过交易所需的PII，签发人应考虑将凭证中公布的信息限制在预期目的所需的最低限度。避免在凭证中放置PII的一种方法是使用一个抽象属性，以满足验证者的需求，而不提供主体的具体信息。

例如，本文档使用ageOver属性而不是具体的出生日期，后者构成的PII要强得多。如果特定市场中的零售商通常要求购买者的年龄大于某个年龄，那么在该市场中受信任的发行商可能会选择提供声称主体已满足该要求的可验证凭证，而不是提供包含声称具体出生日期的可验证凭证。这样，个人客户就可以在不透露具体的PII的情况下进行购买。

### 7.8 数据最小化原则

本节是非规范性的。

当在一种情况下泄露的信息泄露到另一种情况下，就会发生侵犯隐私的行为。防止此类侵犯隐私行为的公认最佳做法是将要求和接收的信息限制在绝对必要的最低限度。这种数据最小化的方法是多个司法管辖区的法规所要求的，包括美国的《健康保险便携性和责任法案》（HIPAA）和欧盟的《通用数据保护条例》（GDPR）。

对于可验证凭证，数据最小化对于发行人来说意味着将可验证凭证的内容限制在潜在验证者对预期用途的最低要求范围内。对验证者而言，数据最小化意味着限制获取服务所需的信息范围。

例如，包含驾驶员身份证号码、身高、体重、生日和家庭住址的驾驶执照是一个包含更多信息的凭证，这些信息超出了确定该人超过某一年龄的必要范围。

签发人最好的做法是将信息原子化，或使用允许选择性披露的签名方案。例如，驾照签发人可以签发包含驾照上每一个属性的可验证凭证，也可以签发一套可验证凭证，其中每个可验证凭证只包含一个属性，如一个人的生日。它也可以发行更抽象的可验证凭证（例如，一个只包含年龄超过属性的可验证凭证）。一个可能的适应性是，发行者提供安全的HTTP端点来检索一次性使用的不记名凭证，以促进可验证凭证的假名使用。实施者如果发现这样做不切实际或不安全，应考虑使用选择性披露方案，以消除在证明时对发行者的依赖，并减少发行者的时间相关性风险。

我们敦促验证者只要求提供对特定交易发生绝对必要的信息。这一点很重要，至少有两个原因：

- 减少验证者处理不需要的高度敏感信息的责任。

- 只要求提供特定交易所需的信息，从而提高了个人的隐私。

> 注意：
>
> 只询问特定交易所需的信息，从而提高个人隐私。虽然有可能实践最低限度披露原则，但可能无法避免在一次会议或多次会议上针对具体使用情况大力识别个人。本文件的作者强调，在现实世界的情况下满足这一原则是多么困难。

### 7.9 不记名凭证

本节是非规范性的。

不记名凭证是一种增强隐私的信息，如音乐会门票，它使不记名凭证的持有人有权使用特定资源，而不泄露持有人的敏感信息。不记名凭证通常用于低风险的使用情况，在这种情况下，共享不记名凭证并不令人担忧，也不会导致巨大的经济或声誉损失。

作为不记名凭证的可验证凭证是通过不指定主体标识符来实现的，该标识符使用id属性表示，该属性嵌套在credentialSubject属性中。例如，以下可验证凭证是不记名凭证：



```json
//例 33：发行人属性的使用
{
  “ @context”：[
    “ https://www.w3.org/2018/credentials/v1”，
    “ https://www.w3.org/2018/credentials/examples/v1”
  ]，
  “ id”：“ http://example.edu/credentials/temporary/28934792387492384”，
  “ type”：[“ VerifiableCredential”，“ UniversityDegreeCredential”]，
  “ issuer”：“ https://example.edu/issuers/14”，
  “ issuanceDate”：“ 2017-10-22T12：23：48Z”，
  “ credentialSubject”：{
    //请注意，未为承载凭证指定'id'属性
    “degree”：{
      “ type”：“ BachelorDegree”，
      “name”：“Bachelor of Science and Arts”
    }
  }，
  “proof”：{ ... }
}
```

虽然不记名凭证可以增强隐私性，但必须小心谨慎，以免意外泄露的信息超过不记名凭证持有人的预期。例如，在多个网站重复使用同一不记名凭证，使这些网站有可能串通起来，对持有人进行不正当的追踪或关联。同样，看似非识别性的信息，如出生日期和邮政编码，在同一不记名凭证或会话中同时使用时，也可以用来统计识别个人。

不记名凭证的签发人应确保不记名凭证提供的增强隐私的好处是： 

- 尽可能是一次性使用。

- 不包含个人识别信息。

- 不具有不适当的关联性。

如果发行或请求包含敏感信息的不记名凭证，或者在一个或多个会话中组合两个或多个不记名凭证时，存在相关风险，持证人应被其软件警告。虽然可能无法检测到所有的相关性风险，但有些风险肯定是可以检测到的。

核验人不应请求可用于对持有人进行不当关联的不记名凭证。

### 7.10 有效性检查

本节是非规范性的。

在处理可验证凭证时，核验人应执行附录§A.验证中列出的许多检查，以及各种具体的业务流程检查。有效性检查可能包括检查：

- 持证人的专业执照状态。
- 许可证更新或撤销的日期。
- 个人的分项资格。
- 如果持有人与试图与之互动的实体之间存在关系。
- 与持有人相关的地理位置信息。

执行这些检查的过程可能会导致信息泄露，从而导致侵犯持有人的隐私。例如，检查撤销名单等简单的操作就可以通知发行人，某个特定的企业很可能与持有人进行互动。这可能使发行人在个人不知情的情况下进行串通和关联。

我们敦促发行人在验证过程中不要使用可能导致侵犯隐私的机制，如每张凭证都是唯一的凭证撤销名单。向持有人提供软件的组织应在验证过程中，当凭证中包含可能导致侵犯隐私的信息时发出警告。核查人员应考虑拒绝那些产生侵犯隐私行为或导致不良隐私做法的凭证。

### 7.11 存储供应商和数据挖掘。

本节是非规范性的。

当持有者从签发人处收到可验证凭证时，需要将可验证凭证存储在某个地方（例如，在凭证库中）。要提醒持有人的是，可验证凭证中的信息具有敏感性和高度个性化的特点，是数据挖掘的高价值目标。那些标榜免费存储可验证凭证的服务实际上可能是在挖掘个人数据，并将其出售给希望建立个人和组织个性化档案的组织。

持有人需要了解其凭证存储库的服务条款，特别是对那些在服务提供商处存储其可验证凭证的人的关联性和数据挖掘保护措施。

对数据挖掘和剖析的一些有效缓解措施包括使用：

- 不向第三方出售你的信息的服务提供商。
- 对可验证凭证进行加密的软件，使服务提供商无法查看凭证的内容。
- 在你控制的设备上本地存储可验证凭证的软件，并且不会上传或分析你的信息，超出你的预期。

### 7.12 凭证的汇总

本节是非规范性的。

持有关于同一主体的两份信息，几乎总是比两份信息的总和更能揭示主体的信息，即使信息通过不同渠道传递。可验证凭证的聚合是一种隐私风险，生态系统的所有参与者都需要意识到数据聚合的风险。

例如，如果在多个会话中提供两个不记名凭证，一个是电子邮件地址，另一个是说明持有人年龄超过21岁的凭证，那么信息的验证者现在就有了该人的唯一标识符以及年龄相关信息。现在很容易为持有人创建和建立一个档案，这样随着时间的推移，越来越多的信息被泄露。凭证的聚合也可以在多个网站之间相互勾结进行，导致侵犯隐私。

从技术角度来看，防止信息聚合是一个非常难解决的隐私问题。虽然零知识证明等新的密码技术被提出来作为解决聚合和关联问题的方法，但由于长期存在的标识符和浏览器跟踪技术的存在，即使是最现代的密码技术也会被打败。

相关性或聚合的隐私影响的解决方案往往不是技术性的，而是政策驱动的。因此，如果持有人不希望有关他们的信息被聚合，他们必须在其传输的可验证的演示中表达这一点。

### 7.13 使用模式

本节是非规范性的。

尽管已尽最大努力确保隐私，但实际使用可验证凭证有可能导致去匿名化和隐私的丧失。这种相关性可能发生在以下情况下。

- 同样的可验证凭证被提交给同一个核验人不止一次。核验人可以推断出持有人是同一个人。

- 同一可验证凭证被提交给不同的核验人，而这些核验人串通一气，或者第三方可以获得两个核验人的交易记录。观察力强的人可以推断，在两个服务机构中，出示可验证凭证的人是同一个人。也就是说，这些账户是由同一个人控制的。

- 凭证的主体标识符指的是在多个出示者或验证者中的同一主体。即使呈现不同的凭证，如果主体标识符相同，核验人（以及能够访问核验人日志的人）也可以推断凭证的持有人是同一个人。

- 凭证中的基本信息可用于识别跨服务的个人。在这种情况下，利用其他来源的信息(包括持有人直接提供的信息)，核查人员可以利用凭证中的信息将个人与现有的档案联系起来。例如，如果持有人提供的凭证包括邮政编码、年龄和性别，验证人员就有可能将该凭证的主体与已建立的档案关联起来。更多信息，请参见 [DEMOGRAPHICS]。

- 将凭证的标识符传递给集中式撤销服务器。集中式服务器可以在不同的交互中关联凭证的使用情况。例如，如果一个凭证以这种方式用于年龄证明，集中式服务可以知道该凭证在任何地方被出示（所有酒类商店、酒吧、成人商店、彩票购买等）。

在一定程度上，可以通过以下方式来缓解这种去匿名化和隐私的损失。

- 使用一个全球唯一的标识符作为任何特定凭证的主体，并且永远不重复使用该凭证。

- 如果凭证支持撤销，则使用全球分布的服务进行撤销。

- 设计不依赖于提交凭证ID的撤销API。例如，使用撤销列表而不是查询。

- 避免将个人身份信息与任何特定的长期主体标识符关联。

据了解，这些缓解技术并不总是实用的，甚至不符合必要的使用。有时，关联性是一种要求。

例如，在一些处方药监测项目中，使用监测是一项要求。执法实体需要能够确认个人没有欺骗系统以获得多个受控物质的处方。这种法定的或监管的需要是为了关联使用情况，而不是为了个人隐私。

可验证凭证也将被用于有意地将个人与不同服务相关联，例如，当使用一个共同的角色登录到多个服务时，因此在每个服务上的所有活动都有意地与同一个人相关联。只要这些服务中的每一项都以预期的方式使用关联，这就不是一个隐私问题。

当凭证的呈现产生非预期或意外的关联时，凭证使用的隐私风险就会发生。

### 7.14 与错误的一方分享信息

本节是非规范性的。

当持有人选择与核验人分享信息时，核验人可能是在恶意行事，要求提供可能被用来伤害持有人的信息。例如，核验人可能会要求提供银行账号，然后与其他信息一起用于欺骗持有人或银行。

发行人应努力使尽可能多的信息符号化，这样，如果持有人不小心将凭证传送给错误的核验人，情况就不会是灾难性的。

例如，与其为检查个人银行余额而提供银行账号，不如提供一个令牌，使验证者能够检查余额是否超过一定数额。在这种情况下，银行可以向持有人发放一个包含余额查询令牌的可验证凭证。然后，持有人将把可验证的凭证包括在可验证的演示文稿中，并使用数字签名将该令牌与信用检查机构绑定。然后，验证机构可以将可验证的演示文稿包在他们的数字签名中，并将其交还给发行机构，以动态检查账户余额。

使用这种方法，即使持有人将账户余额令牌分享给错误的一方，攻击者也无法发现银行账号，也无法发现账户中的具体数值。而且考虑到反签名的有效期，不会获得超过几分钟的令牌使用权。

### 7.15 发放索赔的频率。

本节是非规范性的。

如第7.13节 "使用模式 "中所详述，使用模式可与某些类型的行为相关联。当持有人在发行人不知情的情况下使用可验证凭证时，这种关联性可以得到部分缓解。然而，发行人可以通过使其可验证凭证的有效期较短并自动更新的方式来破坏这种保护。

舉例來說，年齡超過可核實的憑證對進入酒吧很有用。如果发行商发行的这种可验证凭证的有效期很短，并且有自动更新机制，那么发行商就有可能将持有人的行为与之相关联，从而对持有人产生负面影响。

向持有人提供软件的组织应该警告他们，如果他们反复使用寿命很短的凭证，可能会导致行为相关性。签发人应避免以能够使其关联使用模式的方式签发凭证。

### 7.16 倾向于使用单一用途证书

本节是非规范性的。

一个理想的尊重隐私的系统将只要求持有人披露与核查员互动所需的信息。然后，核查人员将记录已满足披露要求，并忘记任何已披露的敏感信息。在许多情况下，诸如监管负担等相互竞争的优先事项阻碍了这一理想制度的采用。在其他情况下，长期存在的标识符妨碍了单一用途。然而，任何可验证凭证生态系统的设计都应尽可能地尊重隐私，尽可能地选择一次性使用的可验证凭证。

使用一次性使用的可验证凭证有几个好处。第一个好处是对验证者来说，他们可以确信可验证凭证中的数据是新鲜的。第二个好处是对持有者来说，他们知道如果可验证凭证中没有长期存在的标识符，那么可验证凭证本身就不能被用来在线追踪或关联他们。最后，攻击者没有任何东西可供窃取，使得整个可验证凭证的安全性得到保障。

### 7.17 私人浏览

本节是非规范性的。

在理想的私人浏览情况下，不会泄露PII。由于许多凭证包括 PII，因此向持有人提供软件的组织应警告他们，如果他们希望在私人浏览模式下使用凭证和演示，则可能会泄露这些信息。由于每个浏览器供应商对私人浏览的处理方式不同，有些浏览器可能根本不具备这一功能，因此实施者必须了解这些差异并实施相应的解决方案。

## 8. 安全方面的考虑

本节是非规范性的。

在处理本规范所述数据时，签发人、持有人和核验人应注意一些安全考虑因素。忽视或不理解本节的含义可能会导致安全漏洞。

虽然本节试图强调一系列广泛的安全考虑因素，但它并不是一个完整的清单。在使用本规范中概述的技术实施关键任务系统时，敦促实施者寻求安全和密码学专业人员的建议。

### 8.1 密码学套件和库

本节是非规范性的。

本规范中描述的数据模型的某些方面可以通过使用加密技术加以保护。对于实施者来说，了解用于创建和处理凭证和展示的密码学套件和库非常重要。实现和审计密码学系统通常需要大量的经验。有效的红队（渗透测试团队）也有助于消除安全审查中的偏见。

密码学套件和库有一个保质期，最终会受到新的攻击和技术进步的影响。生产质量系统需要考虑到这一点，并确保存在机制，以方便和主动地升级过期或损坏的加密套件和库，并使现有凭证失效和更换。定期监测对于确保处理凭证的系统的长期可行性非常重要。

### 8.2 内容完整性保护

本节是非规范性的。

可验证凭证通常包含到可验证凭证本身之外的数据的URL。存在于可验证凭证之外的链接内容，如图像、JSON-LD上下文和其他机器可读数据，通常不受保护，以免被篡改，因为这些数据居于可验证凭证上的证明保护之外。例如，以下突出显示的链接没有内容完整性保护，但可能应该受到保护。

```json
例子34：非内容完整性保护链接
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "id": "http://example.edu/credentials/58473",
  "type": ["VerifiableCredential", "AlumniCredential"],
  "credentialSubject": {
    "id": "did:example:ebfeb1f712ebc6f1c276e12ec21",
    "image": "https://example.edu/images/58473",
    "alumniOf": {
      "id": "did:example:c276e12ec21ebfeb1f712ebc6f1",
      "name": [{
        "value": "Example University",
        "lang": "en"
      }, {
        "value": "Exemple d'Université",
        "lang": "fr"
      }]
    }
  },
  "proof": { ... }
}
```

虽然本规范没有推荐任何特定的内容完整性保护，但建议希望确保内容链接受到完整性保护的文档作者使用强制执行内容完整性的URL方案。两个这样的方案是[HASHLINK]规范和[IPFS]。下面的例子改变了前面的例子，使用[HASHLINK]规范为JSON-LD上下文添加了内容完整性保护，并通过使用[IPFS]链接为图像添加了内容完整性保护。

```json
例子35：对外部数据链接的内容完整性保护
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1?hl=z3aq31uzgnZBuWNzUB",
    "https://www.w3.org/2018/credentials/examples/v1?hl=z8guWNzUBnZBu3aq31"
  ],
  "id": "http://example.edu/credentials/58473",
  "type": ["VerifiableCredential", "AlumniCredential"],
  "credentialSubject": {
    "id": "did:example:ebfeb1f712ebc6f1c276e12ec21",
    "image": "ipfs:/ipfs/QmXfrS3pHerg44zzK6QKQj6JDk8H6cMtQS7pdXbohwNQfK/image",
    "alumniOf": {
      "id": "did:example:c276e12ec21ebfeb1f712ebc6f1",
      "name": [{
        "value": "Example University",
        "lang": "en"
      }, {
        "value": "Exemple d'Université",
        "lang": "fr"
      }]
    }
  },
  "proof": { ... }
}
```

> 注
>
> 上面的JSON-LD Contexts是否需要保护是值得商榷的，因为生产实现预计会随重要的JSON-LD Contexts的静态副本一起发布。

虽然上面的例子是实现内容完整性保护的一种方式，但还有其他解决方案可能更适合某些应用。我们敦促实施者了解，没有内容完整性保护的外部机器可读内容的链接如何导致成功的攻击。

### 8.3 未签名的主张

本节是非规范性的。

本规范允许制作不包含任何种类的签名或证明的凭证。这些类型的凭证通常对中间存储或自我声明的信息有用，这类似于在网页上填写表格。实现者应该意识到，这些类型的凭证是不可验证的，因为作者身份不为人知或不可信任。

### 8.4 令牌绑定

本节是非规范性的。

核验人可能需要确保自己是可验证展示的预定接收者，而不是中间人攻击的目标。象令牌绑定[RFC8471]这样的方法可以保证协议的安全，这种方法将可验证展示的请求与响应联系起来。任何不安全的协议都容易受到中间人攻击。

### 8.5 捆绑附属主张

本节是非规范性的。

签发人将凭证中的信息原子化，或使用允许有选择地披露的签名方案，被认为是最佳做法。在原子化的情况下，如果签发人没有安全地进行原子化，持有人可能会以签发人不愿意的方式将不同的凭证捆绑在一起。

例如，一所大学可能会向一个人签发两个可验证的凭证，每个凭证都包含两个属性，这些属性必须合在一起才能指定该人在某个 "部门 "中的 "角色"，例如 "计算机系 "的 "工作人员 "或 "经济系 "的 "研究生"。如果将这些可验证的凭证进行原子化，使每个凭证只包含其中一个属性，那么大学就会给这个人颁发四个凭证，每个凭证都包含以下一个称号。"工作人员"、"研究生"、"计算机系 "和 "经济系"。然后，持有人可以将 "工作人员 "和 "经济系 "这两份可核实的证书转让给核实人，这两份证书合在一起就构成了一项虚假主张。

### 8.6 高动态信息

本节是非规范性的。

当为高度动态的信息签发可验证凭证时，实施者应确保适当设置过期时间。过期时间长于可验证凭证有效的时间范围，可能会产生可利用的安全漏洞。有效期短于可验证凭证所表达的信息有效的时间范围，会给持有人和验证者带来负担。因此，重要的是为可核查凭证设定与使用情况和可核查凭证所含信息的预期寿命相适应的有效期。

### 8.7 设备盗窃和冒名顶替

本节是非规范性的。

当可验证凭证存储在设备上，而该设备丢失或被盗时，攻击者可能会使用受害者的可验证凭证访问系统。减轻这类攻击的方法包括：

- 启用密码，引脚，图案，或生物识别屏幕解锁保护设备。
- 为凭证存储库启用密码、生物识别或多因素验证。
- 在访问加密密钥时启用密码、生物识别或多因素身份验证。
- 使用单独的基于硬件的签名设备。
- 以上所有或任意组合。



## 9. 无障碍考虑因素

本节是非规范性的。

在处理本规范中描述的数据时，实施者应注意一些可访问性方面的考虑。与任何网络标准或协议的实施一样，忽视可访问性问题会使大部分人无法使用这些信息。重要的是要遵循可访问性指南和标准，如[WCAG21]，以确保所有的人，无论能力如何，都能使用这些数据。这在建立利用密码学的系统时尤其重要，因为密码学在历史上曾给辅助技术带来问题。

本节详细介绍了在使用这种数据模型时需要考虑的一般无障碍性问题。

### 9.1 数据优先方法

本节是非规范性的。

当今使用的许多实物证书，如政府的身份证，其无障碍特征较差，包括但不限于小字体、依赖小尺寸和高分辨率的图像，以及没有为有视力障碍的人提供便利。

在利用该数据模型创建可验证的凭证时，建议数据模型设计者采用数据优先的方法。例如，如果选择用数据或图形图像来描述一个证书，设计者应该用机器可读的方式来表达图像的每一个元素，如机构名称或专业证书，而不是依靠浏览者对图像的解释来传达这些信息。使用数据优先的方法是首选，因为它提供了为不同能力的人建立不同界面的基础要素。

## 10. 国际化方面的考虑

本节是非规范性的。

建议实施者在发布本规范所述数据时，注意一些国际化的考虑。与任何网络标准或协议的实现一样，忽视国际化会使数据难以在不同的语言和社会中产生和使用，从而限制了本规范的适用性，并大大降低了其作为标准的价值。

强烈建议实施者阅读Strings on the Web: W3C国际化活动发布的《网络上的字符串：语言和方向元数据》[STRING-META]，该文件详细阐述了提供可靠的文本元数据以支持国际化的必要性。有关国际化考虑因素的最新信息，还敦促实施者阅读《可验证凭证实施指南》[VC-IMP-GUIDE]文档。

本节概述了在使用该数据模型时需要考虑的一般国际化因素，旨在强调网络上的字符串的特定部分。实施者可能有兴趣阅读的《网络上的字符串：语言和方向元数据》文件[STRING-META]的具体部分。

### 10.1 语言和基础方向

本节是非规范性的。

强烈鼓励数据发布者阅读《网络上的字符串》中关于跨语法表达的部分。语言和方向元数据文档[STRING-META]，以确保语言和基本方向信息的表达可以跨越多种表达语法，如[JSON-LD]、[JSON]和CBOR[RFC7049]。

一般的设计模式是在表达一个文本字符串时使用以下标记模板，该文本字符串被标记了语言和可选的特定基本方向。

```
例子36：自然语言字符串的设计模式
"property": {
  "value": "The string value",
  "lang": "LANGUAGE"
  "dir": "DIRECTION"
}
```

利用上面的设计模式，下面的例子将一本书的书名用英文表达出来，而不指定文本方向。

```
例子37：将自然语言文本表达为英文文本
"title": {
  "value": "HTML and CSS: Designing and Creating Websites",
  "lang": "en"
}
```

下一个例子使用类似的阿拉伯语标题，其基本方向为从右到左。

```
例子 38：阿拉伯文文本的基本方向为右向左。
"title": {
  "value": "HTML و CSS: تصميم و إنشاء مواقع الويب",
  "lang": "ar"
  "dir": "rtl"
}
```

> 注
> 如果没有明确的语言和方向表达，上面的文本很可能会被错误地呈现为从左到右，因为许多系统使用文本字符串的第一个字符来确定文本方向。

强烈建议使用JSON-LD的实现者扩展定义国际化属性的JSON-LD上下文，并使用JSON-LD的Scoped Context功能将@value、@language和@direction关键字分别别名为value、lang和dir。下面是一个JSON-LD上下文代码段的例子。

```
例子39：为语言信息指定范围内的别名。
"title": {
  "@context": {"value": "@value", "lang": "@language", "dir": "@direction"},
  "@id": "https://www.w3.org/2018/credentials/examples#title"
}
```

### 10.2 复杂语言标记

本节是非规范性的。

当在一个自然语言字符串中使用多种语言、基本方向和注释时，通常需要更复杂的机制。可以使用标记语言（如 HTML）来对具有多语言和基础方向的文本进行编码。也可以使用rdf:HTML数据类型在JSON-LD中准确编码这样的值。

尽管能够将信息编码为HTML，但强烈不鼓励实现者这样做，因为它。

需要某种版本的HTML处理器，这增加了处理语言和基本方向信息的负担。
增加了利用这种数据模型时的安全攻击面，因为盲目处理HTML可能会导致执行攻击者在数据生产过程中的某个时刻注入的脚本标签。
如果实施者认为他们必须使用 HTML 或其他能够包含可执行脚本的标记语言来处理特定的用例，建议他们分析攻击者如何使用标记对标记的消费者进行注入攻击，然后针对识别出的攻击部署缓解措施。



## A. 验证

## B. 基本情况

## C. 主体与持有人的关系

## D. IANA的考虑因素

## E. 鸣谢

## F. 参考资料
