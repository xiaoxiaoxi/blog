# Java实现简单的区块链

2019-11-18阅读 6360

**1.  概述**

本文中，我们将学习[区块链技术](https://cloud.tencent.com/product/tbaas?from=10680)的基本概念。也将根据概念使用 Java 来实现一个基本的应用程序。

进一步，我们将讨论一些先进的概念以及该技术的实际应用。

## **2.  什么是区块链？**

因此，让我们首先了解到底什么是区块链...

它的起源可以追溯到2008年 Satoshi Nakamoto 在比特币上发布的白皮书。

区块链是一个分散的信息分类账。它由通过使用密码学连接的数据块组成。它属于通过公共网络连接的节点网络。当我们稍后尝试构建一个基本教程时，我们会更好地理解这一点。

有一些我们必须要明白的重要属性，所以让我们来看看它们：

- Tamper-proof [ 加密摘要 ]：首先也是最重要的，**数据作为块的一部分是防篡改的。**每个块都由加密摘要引用，通常称为哈希，使块防篡改。
- Decentralized [ 分散化 ]：**整个区块链是完全分散**在网络上的。这意味着没有主节点，网络中的每个节点都有相同的副本。
- Transparent [ 透明的，显而易见的 ]：每个参与网络的节点都**通过与其他节点的协商一致来验证并向其链添加一个新块**。因此，每个节点都具有完整的数据可视性。

## **3.  区块链如何工作？**

现在，让我们了解区块链如何工作。

区块链的基本单位是块。一个块能封装多个事务或者其它有价值的数据：

![img](https://ask.qcloudimg.com/http-save/6667215/osdakrpufr.jpeg?imageView2/2/w/1620)

我们用哈希值表示一个块。**生成块的哈希值叫做“挖掘”块**。挖掘块通常在计算上很昂贵，因为它可以作为“工作证明”。

块的哈希值通常由以下数据组成：

- 首先，块的哈希值由封装的事务组成。
- 哈希也由块创建的时间戳组成
- 它还包括一个 nonce，一个在密码学中使用的任意数字
- 最后，当前块的哈希也包括前一个块的哈希

**网络中的多个节点可以同时对数据块进行挖掘**。除了生成哈希外，节点还必须验证添加到块中的事务是否合法。先挖一个街区，就赢了比赛！

### **3.2.  添加块到区块链**

当挖掘一个块在计算上很昂贵时，**验证块是否合法相对来说十分简单**。所有在网络上的节点都参与验证新挖掘的块。

![img](https://ask.qcloudimg.com/http-save/6667215/vhhjfq4929.jpeg?imageView2/2/w/1620)

因此，在节点协商一致时**将新挖掘的块添加到区块链**中。

现在，我们可以使用几种共识协议进行验证。网络中的节点使用相同的协议来检测链的恶意分支。因此，即使引入了恶意分支，大多数节点也会很快拒绝它。

## **4.  Java 中的基本区块链**

现在我们已经有了足够的上下文来开始用 Java 构建一个基本的应用程序。

我们这里的简单**示例将演示我们刚才看到的基本概念**。生产级应用程序包含许多超出本教程范围的考虑因素。不过，我们稍后将讨论一些高级主题。

### **4.1.  实现块**

首先，我们需要定义一个简单的 POJO 来保存块数据：

```javascript
public class Block {
    private String hash;
    private String previousHash;
    private String data;
    private long timeStamp;
    private int nonce;
    public Block(String data, String previousHash, long timeStamp) {
        this.data = data;
        this.previousHash = previousHash;
        this.timeStamp = timeStamp;
        this.hash = calculateBlockHash();
    }    // standard getters and setters}
```

让我们来看看我们在这里打包了什么：

- 前一个块的哈希，构建链的重要部分
- 实际数据，任何有价值的信息，如合同
- 块创建的时间戳
- nonce，是密码学中使用的任意数字
- 最后，块的哈希，根据其它数据计算

### **4.2.  计算哈希**

现在，我们如何计算块的哈希？我们使用方法  *calculateBlockHash* ，但是还没有看到实现。在实现这个方法之前，值得花时间了解一下哈希是什么。

哈希是哈希函数的输出。**哈希函数将任意大小的输入数据映射到固定大小的输出数据**。哈希对输入数据中的任何更改都非常敏感，不管这些更改有多小。

此外，仅从它的哈希中获取输入数据是不可能的。这些属性使得哈希函数在密码学中非常有用。

那么，让我们看看如何在  Java 中生成块的哈希：

```javascript
public String calculateBlockHash() {
    String dataToHash = previousHash       + Long.toString(timeStamp)       + Integer.toString(nonce)       + data;
    MessageDigest digest = null;
    byte[] bytes = null;
    try {
        digest = MessageDigest.getInstance("SHA-256");
        bytes = digest.digest(dataToHash.getBytes(UTF_8));
    } catch (NoSuchAlgorithmException | UnsupportedEncodingException ex) {
        logger.log(Level.SEVERE, ex.getMessage());
    }
    StringBuffer buffer = new StringBuffer();
    for (byte b : bytes) {
        buffer.append(String.format("%02x", b));
    }
    return buffer.toString();
}
```

这里发生了很多事情，让我们来详细了解一下：

- 首先，我们将块的不同部分连接起来，生成一个哈希
- 然后，我们从  *MessageDigest* 中获取  SHA-256 哈希函数的一个实例
- 然后，我们生成输入数据的哈希值，它是一个字节数组
- 最后，我们将字节数组转换为十六进制字符串，哈希通常表示为32位十六进制数字

### **4.3.  我们挖好了吗?**

到目前为止，一切听起来都很简单和优雅，除了我们还没有挖掘过块。那么究竟需要挖掘一个块，这已经吸引了开发人员一段时间的幻想！

因此，**挖掘一个块意味着为块解决一个计算上复杂的任务**。虽然计算块的哈希值比较简单，但是找到以5个0开头的哈希值就不那么简单了。更复杂的是找到一个以10个0开头的哈希，我们得到了一个大致的概念。

那么，我们到底该怎么做呢？老实说，这个解决方案没有想象中的那么好！我们是用蛮力来达到这个目标的。我们在这里使用 nonce：

```javascript
public String mineBlock(int prefix) {
    String prefixString = new String(new char[prefix]).replace('\0', '0');
    while (!hash.substring(0, prefix).equals(prefixString)) {
        nonce++;
        hash = calculateBlockHash();
    }
    return hash;
}
```

让我们看看我们要做的是：

- 我们首先定义要查找的前缀
- 然后我们检查是否找到了答案
- 如果没有，则增加 nonce 并在循环中计算哈希
- 循环一直持续到我们中头奖

我们从 nonce 的默认值开始，并将其递增1。但是，在实际应用程序中，有更多**复杂的策略来启动和增加  nonce**。此外，我们没有验证我们的数据，这通常是一个重要的部分。

### **4.4.  运行示例**

现在我们已经定义了块及其函数，我们可以使用它来创建一个简单的区块链。我们将它存储在一个 *ArrayList*  中:

```javascript
List<Block> blockchain = new ArrayList<>();
int prefix = 4;
String prefixString = new String(new char[prefix]).replace('\0', '0');
```

此外，我们定义了一个前缀为4，这实际上意味着我们希望哈希以4个零开始。

让我们看看如何在这里添加一个块：

```javascript
@Test
public void givenBlockchain_whenNewBlockAdded_thenSuccess() {
    Block newBlock = new Block(
        "The is a New Block.",
        blockchain.get(blockchain.size() - 1).getHash(),
        new Date().getTime()
    );
    newBlock.mineBlock(prefix);
    assertTrue(newBlock.getHash().substring(0, prefix).equals(prefixString));
    blockchain.add(newBlock);
}
```

### **4.5.  区块链验证**

节点如何验证区块链是否有效？虽然这可能相当复杂，但让我们考虑一个简单的版本：

```javascript
@Test
public void givenBlockchain_whenValidated_thenSuccess() {
    boolean flag = true;
    for (int i = 0; i < blockchain.size(); i++) {
        String previousHash = i==0 ? "0" : blockchain.get(i - 1).getHash();
        flag = blockchain.get(i).getHash().equals(blockchain.get(i).calculateBlockHash())
        && previousHash.equals(blockchain.get(i).getPreviousHash())
        && blockchain.get(i).getHash().substring(0, prefix).equals(prefixString);
        if (!flag) break;
    }
    assertTrue(flag);
}
```

所以，这里我们对每个块进行三次特定检查：

- 存储的当前块的哈希实际上是它计算的内容
- 当前块中存储的前一个块的哈希是前一个块的哈希
- 当前区块已被开采

## **5.  一些先进的概念**

虽然我们的基本示例展示了区块链的基本概念，但它肯定不完整。要将这项技术投入实际应用，还需要考虑其他几个因素。

虽然不可能全部详细说明，但让我们来看看其中一些重要的：

### **5.1.  事务验证**

计算块的哈希并找到所需的哈希仅仅只是挖掘的一部分。块由数据组成，通常以多个事务的形式存在。在成为块体的一部分并进行开采之前，必须对其进行验证。

区块链的一个典型实现是**对一个块中可以包含多少数据做了限制**。它还**设置了如何验证事务的规则**。网络中的多个节点参与验证过程。

### **5.2.  备用共识协议**

我们看到的一致性算法如“工作证明”，被用来挖掘和验证块。但是，这并不是唯一可用的一致性算法。

还有**几种其它一致性算法以供选择**，如股权证明、权威证明和权重证明。所有这些都有其优缺点。使用哪一个取决于我们打算设计的应用程序的类型。

### **5.3.  挖掘报酬**

区块链网络通常由自愿节点组成。现在，为什么有人想要为这个复杂的过程做出贡献并保持其合法性并不断增长？

这是因为**节点因验证事务和挖掘块而获得奖励**。这些奖励通常以硬币的形式与应用程序相关联。但是应用程序可以决定奖励是任何有价值的东西。

### **5.4.   节点类型**

区块链完全依赖于网络来进行操作。理论上，网络是完全分散的，每一个节点都是相等的。然而，在实践中，网络由多种类型的节点组成。

虽然**完整节点具有完整的事务列表，但轻型节点仅具有部分列表**。此外，不是所有的节点都参与验证和确认。

### **5.5.  安全通信**

区块链技术的标志之一是其开放性和匿名性。但它如何为内部交易提供安全保障？这**基于加密和公钥基础结构**。

事务创始人使用私钥来保护它并将其附加到收件人的公钥。节点可以使用参与验证事务的公钥。

## **6.  区块链的实际应用**

因此，区块链似乎是一项令人兴奋的技术，但它也必须证明是有用的。这项技术已经存在一段时间了，不用说，它已经在许多领域被证明是具有破坏性的。

它在许多其他领域的应用正在积极进行。让我们了解最流行的应用程序：

- **货币**：由于比特币的成功，这是迄今为止最古老、最广为人知的区块链应用。它们向全球人民提供安全、无摩擦的资金，不需要任何中央政府或政府干预。
- **身份**：数字身份正迅速成为当今世界的常态。但是，这会因安全问题和篡改而陷入困境。区块链在彻底改变这一领域是不可避免的，具有完全安全和防篡改的身份。
- **医疗保健**：医疗保健行业充斥着数据，大多由中央政府处理。这会降低处理此类数据的透明度、安全性和效率。区块链技术可以提供一个没有任何第三方提供急需信任的系统。
- **政府**：这或许是一个很容易被区块链技术破坏的领域。区块链能够建立更好的政府与公民的关系。政府通常是几个公民服务机构的中心，这些机构往往充斥着低效和腐败。

## **7.  行业工具**

虽然我们这里的基本实现有助于引出概念，但是从头开始在区块链上开发产品是不现实的。值得庆幸的是，这个领域现在已经成熟了，我们确实有一些非常有用的工具可以开始使用。

让我们来看一些在这个领域工作的流行工具：

- Solidity：Solidity 是**一种静态类型和面向对象的编程语言**，专为编写智能合约而设计。它可以用来在像 Ethereum 这样的各种区块链平台上编写智能合约。
- Remix IDE：Remix 是一个使用 solidity  **编写智能合约的强大开源工具**。这使用户可以直接从浏览器编写智能合约。
- Truffle Suite：Truffle 提供了**大量工具来帮助开发人员开始开发**分布式应用程序。
- Ethlint/Solium：Solium 允许开发人员确保他们**写在 Solidity 上的智能合约没有风格和安全问题**。同时，Solium 也有助于处理这些问题。
- Parity：Parity 有助于**设置在 Etherium 上智能合约的开发环境**。它提供一种快速及有效的方法与区块链进行交互。

## **8.  结论**

总而言之，本节中，我们了解了区块链技术的基本概念。我们了解网络如何挖掘并在区块链中添加新区块。此外，我们用 Java 来实现了基本概念。我们还讨论了一些与之相关的先进概念。

最后，我们总结了区块链的一些实际应用以及可用的工具。

一如既往，代码可以在 GitHub 上找到。 

●[死磕并发：Java内存模型](https://mp.weixin.qq.com/s?__biz=Mzg3NDA4MjYyOQ==&mid=2247484110&idx=1&sn=8d3958f69eb969465335ce44b72069c8&chksm=ced77ae4f9a0f3f24219606334228c14773f58c1b9778cdbaf1583b6a1600006eb32499a58c6&scene=21#wechat_redirect)

●[Java内存模型详解(一)](https://mp.weixin.qq.com/s?__biz=Mzg3NDA4MjYyOQ==&mid=2247484083&idx=1&sn=02db9a9b4800c12808fc25807222041f&chksm=ced77a99f9a0f38f6cc35af49e3053662a0a9677a63aac8b540eb02157b4b6b7760f634311af&scene=21#wechat_redirect)

●[如何使用Arrays工具类操作数组](https://mp.weixin.qq.com/s?__biz=Mzg3NDA4MjYyOQ==&mid=2247484069&idx=1&sn=2e8555e00782dd2a2272a1374069b1bb&chksm=ced77a8ff9a0f399c8e319e46aa6e45af07e6f24966518fdf8eeab96f0391e78edd648cc010b&scene=21#wechat_redirect)

●[ThreadLocal可以解决并发问题吗](https://mp.weixin.qq.com/s?__biz=Mzg3NDA4MjYyOQ==&mid=2247484097&idx=1&sn=53ca2293af54366ab41e88ea5b2ae62c&chksm=ced77aebf9a0f3fd7f399c48e90f1e1f5fe1d43152903859f8d883176b5244581842044b9732&scene=21#wechat_redirect)