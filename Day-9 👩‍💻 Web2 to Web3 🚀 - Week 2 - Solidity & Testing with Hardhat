这是为您整理的第二周第四天（Day 9）关于 Solidity 基础与实践的完整中文翻译稿。

2026年01月13日 15:45 发言人：Austin Griffith, Carlos, Etta

第一部分：Solidity 探索与环境介绍
Austin: 嘿！我是 Austin Griffith。今天我和 Carlos、Etta 在一起。我甚至不记得今天是第几天了，大概是第二周的第四天，也是我们这一系列课程的第九天左右。

今天，我们要让大家在鼓捣（tinkering）Solidity 时充满信心。我们所说的“鼓捣”是什么意思？就是：写一点代码，部署它，戳戳它（测试功能），看看它是如何工作的，然后不断重复。这是一个不断迭代和摸索的过程。我先占用一下屏幕，展示一下下周我们要讲的 Scaffold-ETH，因为它能让这种摸索变得极其简单。

之后我们会缩小视角，看看其他的摸索方式，然后 Carlos 会重点展示只使用 Hardhat 的摸索方法。我先展示一下 Scaffold-ETH，特别是里面的“Solidity 示例”。

（分享屏幕）

Austin: 这是 Scaffold-ETH。现在这里东西很多，先别担心。我想展示的是：当你修改智能合约（比如我改了一个字符串），保存并部署，它就会立即在前端显示出来。你可以直接在前端戳戳点点。

我们要看的第一件事是原始数据类型。作为一个程序员，当你入门时，首先要理解语法和原始类型。我们从整数（int）和无符号整数（uint）开始。我从“Solidity by Example”网站抓取一个 uint，粘贴到代码里。我们不需要原来的那些代码，只写一个简单的计数器（counter），然后写一个递增函数 increment，代码就是 counter++。

对我来说，这就是“鼓捣”。写点代码，部署，然后在前端看到它，点击按钮让数字加 1。如果改成 counter += 2 呢？或者记录是谁调用的？我们可以加一个 address public boss，然后在函数里设置 boss = msg.sender。msg.sender 是 Solidity 中的全局变量，代表调用函数的人。

部署后，只要我点一下递增，boss 就会变成我的地址。这种即时反馈就是学习 Solidity 的最佳方式。接下来，让 Etta 给我们展示一下 Remix，这是另一种很棒的在线摸索方式。

第二部分：Remix 在线编辑器
Etta: 好的，我来分享屏幕。Remix 是一个基于浏览器的 IDE，你不需要安装任何东西，直接访问 remix.ethereum.org。它提供了一些基础合约，你可以直接在浏览器里编译和部署。

Austin: 里面有哪些默认合约？

Etta: 它通常带有一个存储合约（storage.sol）。在这里你可以看到结构体（structs）、数组（arrays）和映射（mappings）。最酷的一点是你可以直接连接你的 Metamask 钱包进行部署。

Austin: 目标很简单：如果你懂编程，Solidity 的语法会很容易上手。你可以用 Scaffold-ETH、Remix，或者在本地使用 Hardhat。Carlos，接下来请展示一下在本地如何操作。

第三部分：Hardhat 本地开发流程
Carlos: 好的。Scaffold-ETH 确实很难被超越，因为它自带 UI。而 Hardhat 是“硬核模式”，更适合极客，因为它更底层，你需要通过脚本与合约交互。此外还有 Foundry，它是用 Rust 写的，速度甚至比 Hardhat 还快。

现在我们创建一个 Day 4 文件夹，再次安装 Hardhat。我的电脑里到处都是 node_modules 文件夹，占了几百个 G。我们选择创建一个示例项目（sample project），它会自动配置好依赖、测试和脚本。

Austin: 让我们看看一个 Solidity 合约由什么组成。首先是 pragma 版本声明，这非常重要。它告诉编译器使用哪个版本。比如 0.8 版本之后，编译器内置了溢出检查，我们不再需要 SafeMath 库了。

Carlos: 然后是合约声明（contract关键字）。在 Java 或 PHP 里，类属性通常存在内存中，但在 Solidity 中，这些属性是状态变量，它们存储在区块链上（Storage）。

Austin: 没错。你部署合约后，这个变量会存在于成千上万台机器上。这也是为什么存储数据很贵的原因。

第四部分：函数类型与可见性
Carlos: 接下来是函数。有 读取（Read） 和 写入（Write） 之分。

View 函数： 只读不写。读取是免费的（如果是通过客户端调用），因为它不需要矿工打包交易。

Pure 函数： 既不读也不改状态，完全确定性。

Austin: 关于可见性：public、private、internal、external。 重要提示： 区块链上的一切都是公开透明的。标记为 private 只是防止其他合约访问，并不代表人类看不见这个值。

Carlos: 如果我试图在 view 函数里修改状态变量，编译器会报错。

第五部分：编写计数器合约与测试
Carlos: 我们来写个计数器。代码非常简单：一个 uint256 count，一个 increment，一个 decrement。

Austin: 这种代码很无聊，对吧？但当它跑在成千上万台机器上，而且有人愿意花钱去改这个数字时，它就变得有趣了。

Carlos: 现在我来编译（npx hardhat compile）。编译会将 Solidity 转为字节码（Bytecode）。我们可以看看 artifacts 文件夹里的 JSON 文件，里面有 ABI（接口说明）和字节码。这就是真正存留在链上的东西。

Carlos: 我们再写一个简单的测试脚本。部署合约，调用 increment，然后断言（expect）结果等于 1。

Austin: 在 Hardhat 里，你必须通过写测试脚本来“戳”合约，这比在前端点按钮要慢一些。但这是专业的做法，当你有了最终版本，你需要编写详尽的测试用例。

第六部分：构造函数与全局变量
Carlos: 我们还可以加一个 构造函数（Constructor）。它只在部署时运行一次，可以接收参数。比如我们设置初始值。

Austin: 还有 地址（Address） 类型。我们引入“老板（Owner/Boss）”的概念。 boss = msg.sender。msg.sender 是最常用的全局变量。

Carlos: 我们来测试一下：部署者是否就是 boss？Hardhat 提供了一组确定性的账户（Signers），第一个通常是 0xf39...。

Austin: boss 这个词不是关键字，只是我们起的名字。你可以叫它 admin 甚至 Carlos。

第七部分：Require 语句与修改器 (Modifiers)
Austin: Solidity 最强大的地方在于 require 语句。它设定了一条规则：必须为真，否则整笔交易回滚，就像从未发生过一样。

Carlos: 比如，我们规定：任何人都可以递增，但只有“老板”可以递减。 代码：require(msg.sender == boss, "Sorry, not the boss");

Austin: 如果有很多函数都需要这个检查，该怎么办？

Carlos: 这就是 修改器（Modifier） 的用途。 我们写一个 modifier onlyBoss()。语法里那个奇怪的 _ ;（下划线分号）代表：“运行完检查后，再执行原函数的代码”。

Carlos: 这样我们只需要在函数声明后面加上 onlyBoss 即可。

第八部分：实战：创建一个数字货币 (Token)
Austin: 虽然数字货币有时声誉不佳，但我们是为了技术。让我们做一个“Sanford Token”。

Carlos: 我们需要：

映射（Mapping）： mapping(address => uint256) balances。这就像一个字典，记录每个地址有多少钱。

总量（Total Supply）： 设定一个上限，比如 1000 个。

发行（Mint）： 一个 create 函数，只有老板能调用，且不能超过总量。

Austin: 映射的一个特点是不可遍历。你不能循环查看所有持币人的余额，除非你额外用一个数组去记录地址。

Carlos: 接着是 转账（Transfer）。代码其实就是：发件人减去金额，收件人加上金额。 balances[msg.sender] -= amount; balances[to] += amount; 得益于 Solidity 0.8，如果余额不足减成负数，交易会自动回滚。

第九部分：Payable 函数与发送以太币
Carlos: 如果我们想让别人买代币呢？我们需要 payable 关键字。

Austin: msg.value 是另一个全局变量，代表用户发送了多少以太币。我们可以设一个 mintPrice。 require(msg.value == mintPrice, "Wrong price");

Carlos: 这里有个坑：发给合约的钱会存在合约地址里。如果没有 提现（Withdraw） 函数，这些钱就永远锁死在里面了。

Austin: 关于发送以太币，有三个方法：send、transfer 和 call。 职业建议： 永远使用 addr.call{value: amount}("")。虽然语法有点丑，但它是目前最安全、最推荐的方法，可以避免 Gas 限制导致的问题。

第十部分：事件 (Events)
Austin: 最后我们要讲的是 事件（Events）。

Austin: 状态变量（Storage）很贵。如果你只想记录历史记录（比如谁买了代币），供前端显示，而不是供其他合约读取，那就用事件。 事件被存储在日志（Logs）里，其他合约无法读取，但前端可以非常轻松地订阅和查询。这是一种低成本的链上存储方案。

Carlos: 在 buy 函数里加上 emit Buy(msg.sender, amount);。

结语
Austin: Solidity 速成班结束！今天我们讲了数据类型、构造函数、映射、Require、修改器、代币逻辑、以太币交互和事件。

大家可以去“Solidity by Example”继续深钻。多尝试，多重写，多测试。无论是用 Remix 还是 Hardhat，重点是动起手来。

下周我们会进入 Scaffold-ETH，让一切可视化。谢谢 Carlos 和 Etta！下周见！
