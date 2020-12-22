# 可验证凭证实施指南1.0

原文地址：https://w3c.github.io/vc-imp-guide/

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



## 8. 使用 JWT aud claim

JWT aud claim 指的是(即确定)可验证的展示的预期受众(即核验人)。因此，这是上述链接数据证明方法的一种替代方法。它让持有人指明它允许哪些验证者来验证可验证的演示。任何未在 aud 中标识的符合 JWT 的验证者都必须拒绝 JWT（见 RFC 7519）。

RFC 7519 将 aud 定义为 "大小写敏感的字符串数组，每个数组包含一个 StringOrURI 值"。对于在可验证演示中的使用，我们强烈建议将其限制为一个单一的URI值，等于预期验证者的URI。

数据模型规范没有提供指导，说明如何将这个 JWT 要求转化为可验证的呈现方式的属性，反之亦然。我们强烈建议将审计JWT要求映射到可核查演示的核查器属性。

例子 4.使用 verifier 属性的目标可验证展示示例 一个使用验证器属性的可验证的目标展示示例

```
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2019/credentials/v1.1"
  ],
  "type": "VerifiablePresentation",
  "verifiableCredential": [" ... "],
  "holder": "did:example:ebfeb1f712ebc6f1c276e12ec21",
  "verifier": "https://some.verifier.com"
}
```

例子5。使用JWT aud claim进行有针对性的可验证展示的JWT实例。

```
{
  "iss": "did:example:ebfeb1f712ebc6f1c276e12ec21",
  "jti": "urn:uuid:3978344f-8596-4c3a-a978-8fcaba3903c5",
  "aud": "https://some.verifier.com",
  "nbf": 1541493724,
  "iat": 1541493724,
  "exp": 1573029723,
  "nonce": "343s$FSFDa-",
  "vp": {
    "@context": [
      "https://www.w3.org/2018/credentials/v1",
      "https://www.w3.org/2018/credImpGuide/v1"
    ],
    "type": "VerifiablePresentation",
    "verifiableCredential": [" ... "]
  }
}
```



## 9. 扩展

本节是非规范性的。

可验证凭证数据模型是围绕着一个开放世界的假设设计的，这意味着任何实体都可以对另一个实体说任何话。这种方法可以实现无许可的创新；没有集中的登记处或权威机构，扩展作者必须通过它们注册自己或他们创建的具体数据模型和词汇表。

相反，凭证数据模型作者要通过使用[LINKED-DATA]来使用机器可读词汇表。本实施指南提供了如何使用一种被软件开发人员和网页作者所欢迎的名为[JSON-LD]的数据格式来表达数据模型的例子。这种数据格式提供了一些功能，使作者能够用习惯的JSON来表达他们的数据模型，同时也确保他们的词汇术语能够被明确理解，即使是没有实现JSON-LD处理的软件也能理解。

可验证凭证数据模型还使用了基于图的数据模型，它允许作者对描述单个实体的一个或多个属性的简单关系和复杂的多实体关系进行建模。

本节其余部分将介绍如何编写基于可验证凭证数据模型的扩展。

### 9.1 创建新的证书类型

我们期望对可验证凭证数据模型最常见的扩展是新的凭证类型。每当有人对一个或多个实体有话要说，并且希望他们的作者身份是可验证的，他们就应该使用可验证凭证。有时，可能有一个别人创建的现有凭证类型，可以重复使用，以做出他们想要做出的声明。然而，在某些情况下，往往需要新的凭证类型。

新的凭证类型可以通过以下几个步骤来创建。本指南还将指导您创建一个新的凭证类型示例。在高层次上，要遵循的步骤是。

1. 设计数据模型。
1. 创建一个新的JSON-LD上下文。
1. 选择一个发布位置。
1. 在发布新凭证时使用新的JSON-LD上下文。

那么，让我们来逐步创建一个新的凭证类型，我们将把它称为ExampleAddressCredential。这个凭证的目的将是表达一个人的邮政地址。

#### 设计数据模型

首先，我们必须为我们的新凭证类型设计一个数据模型。我们知道，我们需要能够表达邮政地址的基本内容，比如一个人的城市、州和邮编。当然，这些项目是相当以美国为中心的，所以我们应该考虑将这些术语国际化。但是在我们进一步发展之前，因为我们使用的是[LINKED-DATA]词汇表，所以很有可能一些常见的概念已经有了别人创造的词汇表，我们可以利用它。

如果我们要使用别人的词汇表，我们要确保它是稳定的，不太可能发生任何重大变化。甚至可能会有一些技术，我们可以利用这些技术来存储我们可以参考的不可改变的词汇表，但这些不是这个例子的重点。在这里，我们将借助于网络上一个非常流行的词汇--schema.org的惯性。事实证明，这个词汇正是我们所需要的，它已经对邮政地址进行了建模，甚至还有如何使用JSON-LD表达的例子。

请注意，schema.org的开发是渐进式的，这意味着今天的术语定义可能与未来的定义不同，甚至被删除。尽管schema.org开发者鼓励使用最新版本，如结构化数据应用中简单的非版本schema.org URL，如`http://schema.org/Place`，但在某些时候，更精确的版本是很重要的。Schema.org还提供了每个版本的日期快照，包括schema.org核心词汇的人类和机器可读定义。这些都是在发布页面上链接的。例如，你可以使用版本化的URI `https://schema.org/version/3.9/schema-all.html#term_Place`，而不是未版本化的URI `http://schema.org/Place`。此外，schemaVersion属性已经被定义，为文档提供了一种方式来表明schema.org定义的具体预期版本。

使用schema.org词汇和JSON-LD，我们可以这样表达一个人的地址：

例子6: 示例 schema.org 地址

```
{
  
  "@context": [
    "http://schema.org"
  ],
  "type": "Person",
  "address": {
    "type": "PostalAddress",
    "streetAddress": "123 Main St."
    "addressLocality": "Blacksburg",
    "addressRegion": "VA",
    "postalCode": "24060",
    "addressCountry": "US"
  }
}
```

注意上面JSON中的@context键。这个@context指的是一个机器可读文件（也用JSON表示），它提供了术语定义[JSON-LD]。术语定义将JSON中使用的一个键或类型，如地址或PostalAddress，映射到一个全球唯一的标识符：URL。

这确保了当软件看到@context `http://schema.org` 时，它将以全球一致的方式解释JSON中的键和类型，而不需要开发人员在JSON中或可能遍历它的代码中使用完整的URL。只要软件知道所使用的具体的@context（或者如果它使用JSON-LD处理将其转换为其他已知的@context），那么它将理解JSON的编写背景和意图。使用@context还可以像上面的例子一样，将@type等[JSON-LD]关键字别名为更简单的类型。

注意，如果我们想避免使用@context，我们也可以使用完整的URL来表达JSON。下面是我们这样做的例子：

例子7: schema.org地址与完整的URL的例子。

```
{
  "@type": "http://schema.org/Person",
  "http://schema.org/address": {
    "@type": "http://schema.org/PostalAddress",
    "http://schema.org/streetAddress": "123 Main St."
    "http://schema.org/addressLocality": "Blacksburg",
    "http://schema.org/addressRegion": "VA",
    "http://schema.org/postalCode": "24060",
    "http://schema.org/addressCountry": "US"
  }
}
```

虽然这种形式是一种可以接受的表达信息的方式，使其毫不含糊，但许多软件开发人员更愿意使用更习惯的JSON。使用@context可以在不失去全局一致性的情况下实现习惯性的JSON，并且不需要一个集中的注册表或权威机构来创建扩展。请注意，@context也可以有一个以上的值。在这种情况下，一个JSON数组被用来表达多个值，其中每个值都会引用定义术语的另一个上下文。利用这种机制，我们可以先引入可验证凭证数据模型规范中定义的术语，然后再引入schema.org定义的术语：

例子8: 带schema.org上下文的地址凭证示例。

```
{
  
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "http://schema.org"
  ],
  ...
  "credentialSubject": {
    "type": "Person",
    "address": {
      "type": "PostalAddress",
      "streetAddress": "123 Main St."
      "addressLocality": "Blacksburg",
      "addressRegion": "VA",
      "postalCode": "24060",
      "addressCountry": "US"
    }
  },
  ...
}
```

但请注意，每个上下文可能对同一术语有不同的定义，例如，JSON键地址可能在每个上下文中映射到不同的URL。默认情况下，[JSON-LD]允许@上下文中的术语使用最后一个术语胜出的顺序重新定义。虽然这些变化可以通过使用JSON-LD处理安全地处理，但我们希望降低可验证凭证消费者的负担。我们希望消费者软件只需要读取和理解与@context键相关联的字符串值，就能够对术语的含义做出假设。我们不希望他们担心术语会以意想不到的方式被重新定义。这样他们的软件就可以只检查@context的值，然后被硬编码来理解术语的含义。

为了防止术语重新定义，[JSON-LD]@protected特性必须应用于@context中的术语定义。核心可验证凭证@上下文中的所有术语都已经以这种方式受到保护。唯一允许重新定义现有术语的情况是，新定义的范围是在上下文中定义的另一个新术语之下。这符合开发者的期望，并确保消费者软件对它所处理的数据的语义有很强的保证；它可以被写成永远不会对术语的定义感到困惑。请注意，消费者必须确定自己的风险状况，以确定如何处理其软件处理的任何包含其不理解的术语的凭证。

#### 创建一个新的JSON-LD上下文

鉴于上述情况，我们不想使用schema.org上下文的原因至少有一个：它被设计得非常灵活，因此没有使用@protected特性。不过我们想要创建自己的[JSON-LD]上下文还有几个原因。首先，schema.org上下文没有定义我们的新凭证类型。ExampleAddressCredential. 其次，它不是通过安全协议（例如，https）提供服务，而是使用http。请注意，这并不像看起来那样令人担忧，因为建议所有可验证凭证消费软件都对它所理解的@context值进行硬编码，而不是伸向Web来获取它们。最后，它是一个非常大的上下文，包含了更多的术语定义，而不是我们所需要的。

所以，我们将创建我们自己的[JSON-LD]上下文，它只表达我们新的凭证类型所需要的那些术语定义。请注意，这并不意味着我们必须新建URL；我们仍然可以重用schema.org词汇。我们所做的只是创建一个更加简洁和有针对性的上下文。下面是我们在上下文中需要的东西。

例子9: 地址凭证上下文示例

```
{
  "@version": 1.1,
  "@protected": true,

  "ExampleAddressCredential":
    "https://example.org/ExampleAddressCredential",

  "Person": {
    "@id": "http://schema.org/Person",
    "@context": {
      "@version": 1.1,
      "@protected": true,

      "address": "http://schema.org/address"
    }
  },
  "PostalAddress": {
    "@id": "http://schema.org/PostalAddress",
    "@context": {
      "@version": 1.1,
      "@protected": true,

      "streetAddress": "http://schema.org/streetAddress",
      "addressLocality": "http://schema.org/addressLocality",
      "addressRegion": "http://schema.org/addressRegion",
      "postalCode": "http://schema.org/postalCode",
      "addressCountry": "http://schema.org/addressCountry"
    }
  }
}
```

上面的上下文为我们的新凭证类型ExampleAddressCredential定义了一个术语，将其映射到URL `https://example.org/ExampleAddressCredential`。我们也可以选择像urn:private-example:ExampleAddressCredential这样的URI，但如果我们愿意的话，这种方法将不允许我们提供一个网页来描述它。该上下文还定义了Person和PostalAddress类型的术语，将它们映射到它们的schema.org词汇URL上。此外，当使用这些类型时，它还通过一个范围上下文为它们中的每一个类型定义了受保护的术语，将地址和 streetAddress 等术语映射到它们的 schema.org 词汇 URL 中。关于如何编写JSON-LD上下文或作用域上下文的更多信息，请参见[JSON-LD]规范。

#### 选择发布位置

现在我们有了一个[JSON-LD]上下文，我们必须给它一个URL。从技术上讲，我们可以只使用URI，例如，一个私有的URN，如urn:private-example:my-extension。然而，如果我们希望人们能够在网络上阅读和发现它，我们应该给它一个URL，比如`https://example.org/example-address-credential-context/v1`。

当这个URL被derefer引用时，它应该默认返回application/ld+json，以允许JSON-LD处理器处理上下文。然而，如果用户代理请求HTML，它应该返回人类可读的文本，向人类解释术语定义是什么以及它们映射到什么。由于我们正在重用一个现有的词汇，schema.org，我们也可以简单地通过他们的网站链接到我们的类型和术语的意义定义。如果我们创建了自己的新词汇，我们会在自己的网站上对它们进行描述，最好也包括机读信息。

### 发出新凭证时使用新的JSON-LD上下文

现在，我们已经准备好了我们的上下文，可以让任何希望发行一个ExampleAddressCredential的人使用。

例子10: 使用schema.org上下文的地址凭证示例

```
{
  
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://example.org/example-address-credential-context/v1"
  ],
  "id": "https://example.org/credentials/1234",
  "type": "ExampleAddressCredential",
  "issuer": "https://example.org/people#me",
  "issuanceDate": "2017-12-05T14:27:42Z",
  "credentialSubject": {
    "id": "did:example:1234",
    "type": "Person",
    "address": {
      "type": "PostalAddress",
      "streetAddress": "123 Main St."
      "addressLocality": "Blacksburg",
      "addressRegion": "VA",
      "postalCode": "24060",
      "addressCountry": "US"
    }
  },
  "proof": { ... }
}
```

需要注意的是，编写这种新的凭证类型不需要任何人的许可，你必须只遵守上述参考标准。

### 9.2 扩展 JWTs

可验证凭证数据模型1.0规定了一套最低限度的JWT权利要求名称，用于表示可验证凭证及其凭证主体的属性。实现者可能希望用一些新的属性（例如，drivingLicenseNumber，mySpecialProperty）或已经在IANA注册为JWT声明名的属性（例如，given_name.phone_number_verified.PersonalProperty）来扩展可验证凭证。

正如 Verifiable Credentials Data Model 1.0 所述，此类扩展属性最好直接放在 JWT vc claim 或 vc claim 的 credentialSubject 属性中（视情况而定），尽管它们可以直接放在自己的 JWT claim 中。

如果实现者希望为这些扩展使用 JWT 权利要求名称，建议采取以下步骤。请注意，有三种类型的 JWT 权利要求名称：公共的，用 URI 命名；私有的，用本地名称命名；以及在 IANA 注册。

1. 首先，向 IANA (`https://www.iana.org/assignments/jwt/jwt.xhtml)`检查 JWT 要求名是否已经存在。
2. 如果它不存在，实现者可能希望给它一个公共名称（即URI），给它一个本地名称（即任何字符串），或者向IANA注册。
3. 一旦 JWT 权利要求名称存在，定义编码/解码转换规则，将可验证的凭证属性或 credentialSubject 属性转换为 JWT 权利要求。
  - 编码。从可核查的凭证中删除属性，根据定义的规则对其进行编码，并将其放入JWT权利要求中。
  - 解码。从JWT索赔中删除该值，根据所定义的规则对其进行解码，并将其放入新的可核查凭证JSON对象中，酌情作为可核查凭证或凭证主体的属性。

### 9.3 人文可读性

JSON-LD上下文声明机制被实现者用来向消费应用程序发出数据传输发生的上下文信号。

例子11: 使用@context机制

```
{
  
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "id": "http://example.edu/credentials/1872",
  
```

我们敦促扩展作者在上下文URL上发布两种类型的信息。第一类信息是为机器提供的，是机器可读的JSON-LD上下文。第二类信息是给人看的，应该是HTML文档。建议默认的操作模式是服务于机器可读的JSON-LD上下文，因为这是URL的主要用途。如果支持内容协商，对文本/html的请求应该产生一个人可读的文档。人可读的文档至少应该包含扩展的使用信息，例如与@context属性相关联的URL的预期顺序，详细说明扩展的规格，以及扩展的典型使用示例。



## 10. 证明格式

本节是非规范性的。

可验证凭证数据模型的设计与证明格式无关。本规范不规范地要求任何特定的数字证明或签名格式。虽然数据模型是可验证凭证或可验证演示的规范表示，但这些的证明机制往往与双方传输文档时使用的语法相联系。因此，每个证明机制都必须指定证明的验证是根据传输时文档的状态计算，还是根据转换后的数据模型计算，还是根据其他形式计算。在发布时，至少有两种证明格式正在被实现者积极利用，工作组认为，记录这些证明格式是什么以及如何使用这些格式将对其他实现者有利。

本指南在JWTs的优点和JSON-LD和LD-Proofs的优点两节中提供了表格，比较了三种语法和证明格式的生态系统：JSON+JWTs、JSON-LD+JWTs和JSON-LD+LD-Proofs。

由于 "可验证凭证数据模型 "是可扩展的，并且与任何特定的证明格式无关，因此支持对其他证明格式的规范和使用。

10.1  JWTs 的好处

可验证凭证数据模型旨在与各种现有的和新兴的语法和数字证明格式兼容。每种方法都有好处和缺点。下表旨在总结这些原生权衡的一些情况。

下表比较了三种语法和证明格式的生态系统：JSON+JWTs、JSON-LD+JWTs和JSON-LD+LD-Proofs。

|                           Feature                            | JSON + JWTs | JSON‑LD + JWTs | JSON‑LD + LD‑Proofs |
| :---------------------------------------------------------- | :---------: | :------------: | :-----------------: |
|PF1a。证明格式支持零知识证明。	|✓ |✓ |✓|
|PF2a. 证明格式支持工作证明、时间戳证明、利害关系证明等任意证明。	|✓ |✓ |✓|
|PF3a。基于现有的官方标准。	|✓ |✖ |✖|
|PF4a。设计为小尺寸。	|✓ |✖ |✖|
|PF5a. 离线支持，无需进一步处理。	|✓ |✖ |✖|
|PF6a.在其他现有标准中广泛采用。在其他现有标准中广泛采用。	|✓ |✓ |✖|
|PF7a. 无类型歧义。	|✓ |✖ |✖|
|PF8a. 广泛的图书馆支持。	|✓ |✖ |✖|
|PF9a。易于理解签署的内容。	|✓ |✓ |✖|
|PF10a。能够作为 authn/uthz 令牌与现有系统一起使用。	|✓ |✓ |✖|
|PF11a. 不需要额外的规范化。	|✓ |✖ |✖|
|PF12a. 不需要互联网PKI。	|✓ |✖ |✖|
|PF13a. 无需解决外部文件。	|✓ |✖ |✖|

> 注
>
> 上表中列出的一些特征是值得商榷的，因为一个特征总是可以添加到特定的语法或数字证明格式中。该表旨在确定每个组合的本机特征，从而不需要额外的语言设计或扩展来实现所确定的特征。为了简洁起见，所有语言都提供的特征，如表达数字的能力，没有包括在内。在下一节中查找有关不同证明格式的更多信息。

