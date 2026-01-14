
**Austin:** 嘿，我是 Austin，这里还有 Etta 和 Carlos。我们现在进入了从 Web2 到 Web3 课程的第二周。本周的主题是**脚本编写（Scripting）**。我们将深入研究如何通过编写脚本与区块链对话；我们会学习提供者（Providers）、签名者（Signers）、Ethers.js 库，以及 `formatEthers` 和 `parseEthers` 等开发者经常会遇到的工具。如果你还没接触过这些，我们将带你入门。

希望你们已经完成了第一周的内容，并成为了一名以太坊高级用户（Power User）。你们肯定在钱包、Gas 费等方面经历过很多令人沮丧的时刻。在有 MetaMask 之前我们是怎么做的？我们用 Etherscan 查看信息，用 Uniswap，注册 ENS 域名，甚至在 Aave 上借过款，还讨论了 DeFi 生态。我们还接触了多签钱包（Multisig），对吧？希望第一周的内容能让你自如地使用以太坊，度过那些难熬的时刻。

现在进入第二周，讨论脚本。说实话，如果我们只有 1 小时，我们会让你直接去学 Solidity 编写智能合约。但既然我们有更多时间，我们就慢慢来，扫清尽量多的盲点。Carlos，Etta，准备好开始第二周了吗？

**Carlos:** 我准备好了！我喜欢“由下而上”的方法。我喜欢先调用东西，从中理解逻辑。有些人可能喜欢先理解理论和生态，但对我来说，先动手（Get your hands dirty），然后再构建。这是目前我最喜欢的一周。

**Etta:** 我也很兴奋。这些是非常基础的内容，但平时很少被深入探讨，所以过一遍非常有意义。

**Carlos:** 好的，那我们开始吧。最好的起点应该是从头开始——创建一个空项目。

**Austin:** 好的，你能共享屏幕吗？我也会在我的机器上同步操作。我们可能 Node 版本不同。我的 Node 版本是……

**Carlos:** 你能看到我的终端和 IDE 吗？我创建了一个空的 `ethers-scripts` 文件夹。首先是环境要求，我们需要 **Node.js**。安装教程网上很多，这里不细说了。我推荐使用 **n**，它是一个 Node 版本管理器，类似于 **nvm**。它可以让你在不同项目所需的版本间秒切。我现在用的是 Node 16。

**Austin:** 我也是 16。

**Carlos:** 完美。开始前，Austin 或 Etta 能解释一下什么是 **Ethers.js** 吗？

**Austin:** 它就是一个帮助你与以太坊通信的 JavaScript 库。当你和以太坊对话时，它会返回一些东西，比如“大数（Big Numbers）”。JavaScript 无法处理以太坊中那么大的数字，所以我们创建了一个特殊对象来追踪它们。Ethers.js 提供了很多助手函数来格式化数据、与合约对话、发送资产、创建签名者和钱包。它是一个依赖项极少的轻量级库。

**Carlos:** 还有一个更老的替代方案叫 **Web3.js**，也是一个 JavaScript SDK。但现在大多数人都在用 Ethers，所以我们选它。首先，用 `npm init` 初始化项目。我们需要在一个特定文件夹里操作，对吧？

**Austin:** 对，创建一个目录，进入后执行 `npm init`。

**Carlos:** 好的，现在我要做一点个人偏好设置。默认情况下，Node 程序使用 `require`（CommonJS），但我喜欢切换到 **ES6 import** 模式（`import`）。这样做是为了和前端（如 React）保持一致，代码可以跨端复用。你只需要在 `package.json` 里加一个属性 `"type": "module"`。

**Austin:** 太棒了。这样脚本代码以后可以方便地复制到前端脚手架里。顺便问下，你创建了 `test.js`，我创建了 `index.js`，文件名有要求吗？

**Carlos:** 没关系，因为我们会直接通过 Node 调用特定的文件名。现在我们安装依赖：执行 `npm install ethers`。你会看到 `package.json` 更新了，还生成了 `package-lock.json`。这个锁定文件非常重要，它记录了依赖的确切版本，确保别人克隆你的代码并安装时，环境和你的一模一样。

现在我们创建一个新文件 `providers.js`。我们从 **提供者（Providers）** 开始。

Austin 提到过，Ethers 提供了很多工具，而核心概念就是 **Provider** 和 **Signer**。如果你有 Web2 开发背景，你可以把 Provider 想象成第三方服务（比如 Firebase）的 API Key。你需要它来访问服务并读写数据。在 Web3 中，为了保持去中心化并访问以太坊区块链，我们需要一个 Provider。

你可以选择不同的 Provider。网络中任何运行中的、能与其他节点进行点对点通信的节点都可以是 Provider。

**Austin:** 没错。通常大家在运行自己的节点前，会使用像 **Infura** 或 **Alchemy** 这样的服务。它们是中心化公司。但你随时可以像我身后这样设置自己的节点。

这是我的一套节点设备。它包含信标链（Beacon Chain）、验证者节点和执行层节点（Layer 1）。它与网络中其他节点进行 P2P 通信，同步了整个区块链的状态。我可以作为一个 Provider 问它：“这个地址余额多少？”或者“合约里这个变量是多少？”我的脚本会通过 HTTP 请求发给这个 RPC 接口，它就会返回结果。这种方式你不需要信任任何人，因为那是你自己的节点。

**Carlos:** 实例化 Provider 最快的方法是 `getDefaultProvider()`，但这只用于测试，因为它内部使用的是公共 API，如果你请求太频繁就会报错。通常你会去 Infura 注册一个 API Key。Infura 每天提供一定数量的免费请求。

**Austin:** 随着应用接近生产阶段，你可能需要付费版，以免在达到限额时挂掉。

**Carlos:** 实例化 Infura Provider 时，我们通常使用 `JsonRpcProvider`。为了安全，不要把 API Key 直接写在代码里并上传到 GitHub。我们要用 `.env` 文件来管理环境变量。安装 `dotenv` 库，创建一个 `.env` 文件存放 Key，并在 `.gitignore` 里把这个文件排除掉。

现在我们连接上了 Provider。第一件事通常是获取**当前块号（Block Number）**。这能让你知道链有多长，以及你的节点是否在同步。

**Austin:** 获取块号可以验证你是否“活着”且保持同步。

**Carlos:** 这里有个小坑：`getBlockNumber()` 返回的是一个 **Promise**。如果你是编程新手，直接运行会看到输出了一个 Promise 对象而不是数字。我们需要使用 `await`。这也是我喜欢 ES6 模块的原因，它支持顶层 `await`（Top-level await）。

**Austin:** 好的，看看块号。我们可以去 Etherscan 核对一下，确保它是同步的。

**Carlos:** 接下来是 **ENS（以太坊域名服务）**。Ethers 可以解析域名。比如调用 `provider.resolveName("atg.eth")` 就能得到地址。这其实是去跟 ENS 的智能合约对话。

**Austin:** 没错，这很方便。反过来也可以，叫 `lookupAddress`（反向解析），通过地址找域名。

**Carlos:** 记住，Provider 只能**读取（Read）**区块链数据。你不能发送交易或改写数据，那需要 **Signer（签名者）**。现在我们来查余额。查查 Vitalik（以太坊创始人）的余额，他肯定比我们有钱。

调用 `provider.getBalance(nameOrAddress)`。这里又有个坑：返回的不是普通的数字，而是一个 **BigNumber** 对象。

**Austin:** 开发者看到输出 `BigNumber { _hex: ... }` 时可能会懵。别担心，这是因为数字太大了。怎么把它变成人类能看懂的样子？

**Carlos:** Solidity 不处理浮点数是为了避免逻辑复杂化，所以它把所有数字都扩大  倍（以 wei 为单位）。Ethers 提供了 `formatEthers` 助手函数，把 wei 转换成以 ETH 为单位的字符串。

**Austin:** 天呐，Vitalik 的账户里有这么多 ETH。我们去 Etherscan 验证一下。

**Carlos:** 如果我们要发送资产，就需要 `parseEthers`。比如 `parseEthers("1.5")` 会把它转换成对应的大数 wei。

总结一下：**`formatEthers` 用于显示（大数转字符串），`parseEthers` 用于输入（字符串转大数）。**

如果你需要对这些大数做数学运算，千万不要把它们转回 JavaScript 的普通数字，因为会溢出。你应该直接用大数对象的方法。比如 `balance.add(amount)`。

**Austin:** 我们刚才尝试把 Sanford 的余额加 5000 ETH，结果出错了。原来是因为我们加的是 5000 wei，而不是 5000 ETH。应该先用 `parseEthers("5000")` 转换后再相加。

**Carlos:** 没错，解决了。现在我们来看看 **钱包（Wallets）**。
上周我们用 MetaMask 创建钱包，还要备份助记词，挺繁琐的。在代码里非常简单：`ethers.Wallet.createRandom()` 就能生成一个随机钱包。你可以打印它的地址、私钥和助记词。

**Austin:** 打印私钥时心跳都会漏一拍，这在家里千万别随便乱做（指公开私钥）。

**Carlos:** 你可以从助记词衍生出多个账号（HD Wallet）。通过改变路径（path）中的索引号，一个助记词可以对应无数个地址。这和你在 MetaMask 里点击“创建新账号”的原理是一样的。

你也可以通过私钥直接导入钱包：`new ethers.Wallet(privateKey)`。同样，私钥要放在 `.env` 里。

**Austin:** 那么 **Signer** 和 **Provider** 的区别是什么？

**Carlos:** 钱包（Wallet）就是一个 Signer。你可以在不联网的情况下用它签名消息（`signMessage`）。比如你签一个“Hello”，别人可以通过你的签名和原文恢复出你的地址，从而证明是你发的。这不需要 Provider。

但如果你要发送交易或查余额，就需要把 Signer **连接（connect）**到一个 Provider。

最后，我们来实战一下：在 **Rinkeby 测试网**发送一笔交易。我们要从测试网水龙头（Faucet）领一点测试币，然后写脚本把它发送给 Sanford。

**Austin:** 真正的发送交易！

**Carlos:** 调用 `signer.sendTransaction({ to: ..., value: ... })`。这里有个细节：`await` 这个方法只代表交易被发送到了内存池（Mempool），不代表它被矿工打包了。如果你想等待交易确认，需要调用 `tx.wait()`。

刚才我们尝试发给 `sanford.eth` 失败了，因为我们在 Rinkeby 测试网上，而 ENS 解析通常在主网（Mainnet）。所以我们需要两个 Provider：一个连接主网查 ENS，一个连接测试网发交易。

**Austin:** 这对新手来说是个很好的教学案例。你的 App 往往需要连接主网来处理身份（ENS），同时连接到你实际部署的 L2 或测试网。

**Carlos:** 成功了！交易已发出并在区块中确认。Sanford 收到钱了。

**Austin:** 在结束前，我想展示一下连接本地节点的速度。刚才 Carlos 用 Infura 查信息时有明显的延迟。看我的：我连接的是自己身后的物理节点，查询块号和余额几乎是瞬时的。如果你要处理成千上万的数据，拥有自己的节点是巨大的优势。

**Carlos:** 这种“预告”很棒，以后大家也会学会运行自己的节点。感谢今天的脚本编写入门。

**Etta:** 我学到了很多，尤其是那个主网和测试网混合使用的坑，非常有启发。

**Austin:** 所有的坑和奇怪的报错都是财富。作为开发者，你要亲自去试，去覆盖那些盲点。本周我们还会进入智能合约的测试阶段。下期见！

