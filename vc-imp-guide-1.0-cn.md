# 可验证凭证实施指南1.0

**摘要**

本文件提供了可验证凭证的实施指南。

**本文件的状况**。

本节介绍了本文件出版时的状况。其他文件可能会取代本文件。W3C当前出版物和本技术报告的最新修订版清单可在W3C技术报告索引中找到：https://www.w3.org/TR/。

本文件的未来版本将由证书社区组更新和维护。请向该小组查询本文档的最新版本。

由于W3C程序和出版期限的限制，本文件的工作是在时间紧迫的情况下进行的。在这样的条件下，错误在所难免，这里提出的一些观点也不完整。工作组希望未来能够对W3C流程进行修订，以更好地支持标准工作的动态性，在不同的组别中以更一致的方式进行。

欢迎对本文档提出意见。请直接在GitHub上提交问题，或将问题发送到public-vc-comments@w3.org（订阅、存档）。

本文档由可验证主张工作组作为编辑草案发布。
讨论本规范时，首选GitHub Issues。另外，您也可以将意见发送到我们的邮件列表。请将意见发送到 public-vc-comments@w3.org（存档）。
作为编辑草案发布并不意味着W3C成员的认可。本文件是一份草案，可能随时被其他文件更新、替换或淘汰。不宜将本文档作为正在进行的工作以外的其他文件引用。

本文件由根据W3C专利政策运作的一个小组编写。W3C 维护着一份公开的清单，其中列出了与该小组可交付成果有关的任何专利披露；该网页还包括专利披露的说明。如果个人实际知道某项专利，并认为该专利包含基本权利要求，则必须根据W3C专利政策第6条披露该信息。
本文件受2019年3月1日W3C流程文件的约束。



## 1. 简介

本节是非规范性的。

本指南提供了一些实例和资源，用于实施利用核心规范以外的可验证凭证的协议。

首先熟悉官方用例文档可能会有所帮助，该文档提供了日常生活中可能出现的可验证凭证的简明示例，以及如何使用这些凭证。

数据模型规范包含有关可验证凭证的技术细节。但是，数据模型规格没有规定使用可验证凭证的任何协议，也没有规定此类协议可能依赖的任何证明格式或额外标识符。



## 2. 标识符

本节是非规范性的。

在表达关于特定实体（如个人、产品或组织）的声明时，往往需要为其提供一个标识符，以便其他人能够表达关于同一事物的声明。可验证凭证数据模型规范包含了许多例子，其中标识符是一个分散的标识符，也称为DID。DID的一个例子是`did:example:123456abcdef`。

目前有一个W3C去中心化标识符工作组的拟议章程，它将使DID成为W3C标准。

> 注
>
> 截至可验证凭证数据模型规范发布之时，DID对于可验证凭证的有用性并不是必需的。具体而言，可验证凭证不依赖于DID，DID也不依赖于可验证凭证。然而，预计许多可验证凭证将使用DID，实现数据模型规范的软件库将从了解如何解析DID中受益。基于DID的URL可以用来表达与主体、签发人、持有人、凭证状态列表、加密密钥以及其他与可验证凭证相关的机器可读信息相关的标识符。



## 3. 术语

…………



## 4. 核查

本节是非规范性的。

核验是指核验人或持有人在收到可验证展示或可验证凭证时执行的过程。核验包括根据核心数据模型检查所呈现的项目，也可能包括验证所提供的证明部分和检查项目的状态。

### 4.1 核心数据模型

处理可验证凭证的合规工具将确保在处理凭证时对核心数据模型进行验证。

### 4.2 特定的可验证凭证

有很多数据验证语言，下面的方法是一种应该适用于大多数用例的方法。

### 4.3 内容完整性

保护内容的完整性是核验的一个重要组成部分。核验人需要有信心，相信他们用来验证凭证的内容不会在他们不知情的情况下发生变化。这些内容可能包括数据模式、标识符、公钥等。

有许多方法可以提供内容完整性保护。下面将详细介绍其中的几种方法。

#### 4.3.1 散列链接

Hashlink URL可以用来为外部资源的链接提供内容完整性。

#### 4.3.2 可验证的数据注册表

可验证的数据注册表也可以提供内容完整性保护。提供内容完整性保护的可验证数据注册表的一个例子是分布式分类账。这是一种共享的交易记录，它提供了验证其存储内容的机制。这些机制包括共识协议、数字签名和可验证的数据结构，如Merkle树。这些机制提供加密保证，保证从分类账中检索到的内容没有被更改，而且是完整的。



## 5. 引用其他凭证

可验证凭证的使用通常需要引用其他凭证、嵌入或附加多个凭证，或以其他方式将它们绑定在一起。

### 5.1 引用没有完整性保护的凭证

一个凭证引用另一个外部凭证的最简单方法是通过使用其URI直接链接到它，或通过提供一个众所周知的ID间接链接到它（例如，一个模拟公司内部发票的凭证可以简单地通过PO号引用其母采购订单凭证，而PO号仅在这个特定企业的范围内相关）。

这种不使用完整性保护机制而链接到外部凭证的方法在某些用例中可能是可以接受的，例如当两个凭证都是由同一个实体签发的，核验人对签发人的安全和审计机制有很高的信任和信心，而且核验人的风险足够低。但是，实现者应该记住，尽管包含引用的凭证本身可能是受完整性保护的（通过加密签名或类似的证明机制），但核验人无法知道被链接的外部凭证没有被篡改，除非链接本身内置了内容完整性保护机制。

### 5.2 引用具有完整性保护的凭证

从可验证凭证中引用外部凭证的推荐方式是使用一种链接机制，将目标文档的内容与URI本身进行加密绑定。实现这一目标的一种方法是使用哈希林或等效的URI方案。另一种机制是在URI本身中编码目标凭证的全部内容，不过这种机制的使用要少得多，而且关于URI长度的实际限制的讨论也超出了本文档的范围。

### 5.3 附加证据

鼓励希望在可核查的凭证上附加额外证明信息的签发人使用证据属性。请注意，可以通过将相关证据信息嵌入凭证本身，或通过引用该信息(无论是否有完整性保护机制，如前所述)来实现。



## 6. 争议

如果一个实体想对发行人签发的凭证提出异议，至少有两种不同的情况需要考虑。

- 一个主体对发证者提出的要求提出异议。例如，地址属性不正确或过时。
- 一个实体对发证者对另一个主体作出的潜在虚假声明提出异议。例如，一个冒名顶替的人声称是一个实体的社会安全号码。

发行有争议凭证的机制与普通凭证相同，只是有争议凭证属性中的 credentialSubject 标识符是有争议的凭证的标识符。

例如，如果一个标识符为 `https://example.org/credentials/245` 的凭证有争议，实体可以发出下面所示的凭证之一。在第一个例子中，主体可以将其与有争议的凭证一起提交给核验人。在第二个例子中，实体可能会在公共场所发布DisputeCredential，以使人们知道该凭证是有争议的。

例子1: 一个主体对一个证书有争议

```json
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
      "@value": "Address is out of date",
      "@language": "en"
    },
  },
  "issuer": "https://example.com/people#me",
  "issuanceDate": "2017-12-05T14:27:42Z",
  "proof": { ... }
}
```

例子2：另一个实体对一个证书有争议
```json
{
  "@context": "https://w3id.org/credentials/v1",
  "id": "http://example.com/credentials/321",
  "type": ["VerifiableCredential", "DisputeCredential"],
  "credentialSubject": {
    "id": "http://example.com/credentials/245",
    "currentStatus": "Disputed",
    "statusReason": {
      "@value": "Credential contains disputed statements",
      "@language": "en"
    },
    "disputedClaim": {
      "id": "did:example:ebfeb1f712ebc6f1c276e12ec21",
      "address": "Is Wrong"
    }
  },
  "issuer": "https://example.com/people#me",
  "issuanceDate": "2017-12-05T14:27:42Z",
  "proof": { ... }
}
```

在上述可核查凭证中，签发人声称有争议的可验证凭证中的地址是错误的。例如，主体可能错误地声称与签发人的地址相同。

> 注
>
> 如果一项凭证没有识别符，可使用内容标示的识别符来识别有争议的凭证。同样，内容标示的识别符也可用于唯一识别个人主张。



## 7. 展示

可验证凭证可以通过使用可验证展示来向核验人出示。通过使用包含domain和challenge的关联数据证明，可验证展示可以针对特定的核验人。这也有助于防止核验人将可验证展示作为自己的展示重复使用。

domain 可以是任何字符串或URI，而challenge 应该是一个随机生成的字符串。

下面的可验证展示示例是用于验证一个网站，https://example.com。

例子3：有针对性的可验证展示

```json
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1"
  ],
  "type": "VerifiablePresentation,
  "verifiableCredential": { ... },
  "proof": {
    "type": "Ed25519Signature2018",
    "created": "2019-08-13T15:09:00Z",
    "challenge": "d1b23d3...3d23d32d2",
    "domain": "https://example.com",
    "jws": "eyJhbGciOiJFZERTQSIsImI2NCI6ZmFsc2UsImNyaXQiOlsiYjY0Il19..uyW7Hv
      VOZ8QCpLJ63wHode0OdgWjsHfJ0O8d8Kfs55dMVEg3C1Z0bYUGV49s8IlTbi3eXsNvM63n
      vah79E-lAg",
    "proofPurpose": "authentication"
  }
}
```
