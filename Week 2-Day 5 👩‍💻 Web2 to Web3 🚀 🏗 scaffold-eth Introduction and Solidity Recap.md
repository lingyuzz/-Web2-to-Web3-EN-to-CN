第一部分：Scaffold-ETH 入门与安装
Austin: 大家好，我是 Austin。今天我和 Etta、Carlos 在一起。今天是第二周的第5天，也是我们连续开发的第10天。今天我们要重新温习 Solidity 的基础知识。昨天我们讲了 Hardhat 以及如何编写测试，今天我们将使用 Scaffold-ETH 这个工具，它能让你对合约有更深入的洞察，并提供更强的鼓捣（tinkering）能力。

Scaffold-ETH 安装起来比较费时（大约10分钟），所以 Etta，能不能先展示一下你的屏幕，从零开始展示克隆仓库和安装的过程？之后我再切换回我这边已经装好的版本进行演示。

Etta: 好的。基本操作就是搜索“Scaffold-ETH”，去 GitHub 克隆代码。我现在克隆到桌面，命名为“zoom”。

Austin: （接回屏幕）克隆之后，你需要运行 yarn install。接下来有三个核心命令：

yarn chain：启动本地 Hardhat 节点。

yarn start：启动 React 前端。

yarn deploy：部署合约。

Scaffold-ETH 和纯 Hardhat 的区别在于它更加直观（Visceral）。你可以修改一行代码（比如多加几个感叹号），然后 yarn deploy，前端会立即热更新（Hot Reload），显示出新的合约地址和内容。

第二部分：Scaffold-ETH 中的即时摸索 (Tinkering)
Austin: 让我们来试一下全局变量（Globals），比如 block.timestamp。 我写一个读取函数 timey，返回这个时间戳。部署之后，在前端点击一下就能立即看到结果。这种即时反馈非常适合学习和测试假设。

接着，我们从“Solidity by Example”网站搬运代码。把布尔值（bool）、无符号整数（uint256）、地址（address）这些原始类型直接粘贴进合约，部署，然后在前端戳戳点点。

Austin: 顺便说一下钱包。Scaffold-ETH 会自动生成“临时钱包（Burner Wallets）”。你开一个无痕窗口，就会得到一个全新的地址。你可以直接从页面上的水龙头（Faucet）领取测试币，不需要频繁操作 Metamask。

第三部分：深入理解 Payable 和价格曲线
Austin: 智能合约就像自动售货机。让我们把合约改成任何人都可以通过付钱来修改“Purpose”。 我们加入 require(msg.value >= price, "Not enough")。

在前端，Scaffold-ETH 会自动识别出 setPurpose 函数现在是 payable（可支付的），并显示出一个金额输入框。 这里有个坑：单位转换。1 ETH = 10^18 Wei。Scaffold-ETH 会强制你手动输入这个转换过程，让你习惯 Wei 的概念。

Austin: 更有趣的是，我们可以写一个财务机制：每当有人修改 Purpose，价格就上涨 1%。 price = (price * 101) / 100; 虽然 Solidity 没有小数，但通过这一行代码，我们就创造了一个自动涨价的“售货机”。

第四部分：映射（Mapping）与事件（Events）
Austin: 接着说映射。映射是地址到数据类型的对应关系。 mapping(address => uint8) public yourCount; 每次有人调用函数，我们就给他的地址计数加 1。

Carlos: 别忘了加上 public，否则前端不会自动生成读取框。

Austin: 没错。我们在无痕窗口模拟多个“坏人”互相操作，你会发现映射能完美记录每个地址的独立状态。

Austin: 然后是事件（Events）。由于在链上存储数据非常昂贵，我们通常使用事件来驱动前端。 在 Scaffold-ETH 中，有一个专门的“Events”标签页，会实时监听并显示合约抛出的所有事件。这比手动去翻日志要方便得多。

第五部分：继承与 OpenZeppelin
Carlos: 昨天我们手写了“老板（Boss）”模式，即 require(msg.sender == boss)。但其实有更专业的成熟方案。

Austin: 没错，这就是继承（Inheritance）。我们直接导入 OpenZeppelin 的 Ownable 合约。 代码：contract YourContract is Ownable { ... }

Austin: 继承之后，我们的合约自动拥有了 onlyOwner 修改器，以及转移所有权的功能。这比自己手写要安全得多，因为 OpenZeppelin 的代码已经经过了无数人的审计。

Carlos: 我们还可以在构造函数中直接设置初始所有者：_transferOwnership(0x...)。

第六部分：合约间交互与重入攻击 (Reentrancy)
Austin: 这是最硬核的部分：合约调用合约。 我们建立一个“银行”合约（Bank），允许存取款。然后建立一个“中间人/攻击者”合约去调用它。 这里的核心概念是 msg.sender 和 tx.origin。

msg.sender：当前消息的直接发送者。如果 A 调用 B，B 调用 C，那么对 C 来说，msg.sender 是 B。

tx.origin：整个交易链条的最初发起人。对 C 来说，tx.origin 是 A。

[Image illustrating the difference between msg.sender and tx.origin in a multi-contract call]

Austin: 重入攻击（Reentrancy） 是价值数千万美元的教训。 如果你的取款逻辑是：

检查余额。

发送以太币给用户。

余额清零。

攻击者可以利用第2步的回调函数，在余额被清零之前，再次调用取款函数，从而无限循环把银行搬空。

Austin: 修复方案（检查-效果-交互模式）：

记录余额副本。

立即将余额清零（状态更新）。

最后再发送以太币。

即使攻击者重入，由于第2步余额已清零，他将无法再次取款。

结语
Austin: 今天我们全方位展示了如何利用 Scaffold-ETH 快速摸索 Solidity。我们讲了数据类型、映射、事件、继承、以及如何防范重入攻击。

下周，我们将进行“以太坊速通（Speedrun Ethereum）”。我们将默认你已经掌握了语法，重点探讨你能用智能合约构建出什么样强大的去中心化应用。

祝贺大家完成第10天的挑战！下周见！
