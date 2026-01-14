第一部分：欢迎来到以太坊速通（Speedrun Ethereum）
Austin: 大家好，我是 Austin。今天我和 Etta、Carlos 在一起。我们进入了第三周，是时候真正开始构建应用了！

在第一周，我们介绍了如何使用以太坊并成为高级用户；第二周，我们学习了脚本编写以及 Hardhat 和 Solidity 的基础知识。现在，是时候把这些知识结合起来，开始构建去中心化应用（DApp）了。而开始这一切最好的地方就是 speedrunethereum.com。

Austin: 这是我们经过无数次黑客松总结出的课程体系。你会学习到哪些工具是有用的，哪些是坑。 在开始挑战之前，建议你先拉取 Scaffold-ETH 并在本地玩熟上一周讲过的概念：原始类型、全局变量、映射、结构体、修改器、事件、继承、以太币发送等。

一旦你准备好了，第一步就是挑战 0（Challenge 0）。它会手把手教你如何配置环境、理解临时钱包（Burner Wallets）以及如何部署到公共网络。今天 Etta 将带我们演示这个过程。

第二部分：挑战 0——你的第一个 NFT 收藏品
Etta: 好的，我来分享屏幕。我已经克隆了挑战 0 的仓库并完成了安装。

Austin: 这里的超级权力在于：Scaffold-ETH 的每个分支结构都是一样的。永远是 yarn install、yarn chain、yarn start 和 yarn deploy。只要学会了一个，你就学会了 2000 多个基于此的分支。

Etta: 1. yarn chain：启动本地硬帽节点。 2. yarn start：启动前端。 3. yarn deploy：部署 NFT 合约。

现在前端已经跑起来了。我们可以看到多了一个“Collectibles（收藏品）”标签页。我点击“Mint（铸造）”，我得到了一头水牛！这些画都是 Austin 以前画的。

Austin: 如果你是个程序员但不是艺术家，没关系，这里有现成的艺术品供你测试。 Etta: 我们开一个无痕窗口（模拟另一个用户）。你可以把水牛从绿色的钱包发给粉色的钱包。如果粉色钱包想发出去但没有钱，它会提示 Gas 错误，这时你就得去水龙头（Faucet）领钱。

Carlos: 即使这个挑战不涉及写代码，我也建议大家读读 Solidity 代码。看看它如何继承 ERC-721 标准，看看前端是如何从 IPFS 读取数据的。

Austin: 没错！IPFS 是内容寻址存储。如果你把水牛改名成野牛再上传，哈希值（Hash）就会完全改变。这种不可变性是 NFT 的核心。

第三部分：部署到公共测试网 (Rinkeby)
Austin: 在本地玩够了，下一步就是把应用发布到公共网络，让全世界都能看到。 我们需要两步：

部署合约到 Rinkeby 测试网。

将前端部署到 Surge 或 GitHub Pages。

Austin: 部署到公共网络时，你不能再用 Hardhat 的预设账户了。你需要生成自己的账户： yarn generate

Etta: 这一步生成了一个新的地址。 Austin: 好的，我用我手机上的 Punk Wallet 扫描你屏幕上的二维码，给你发点 Rinkeby 测试币。

Austin: 钱到账后，运行： yarn deploy --network rinkeby

Etta: 部署成功了！我们可以在 Rinkeby Etherscan 上查到这个合约地址。 Austin: 别忘了，现在的测试网环境变化很快，Rinkeby 可能很快会被 Goerli 或 Sepolia 取代，但操作逻辑是一样的。如果你要做 NFT，一定要部署到 OpenSea 支持的测试网上。

第四部分：发布前端并连接世界
Austin: 合约上链了，现在把前端也指过去。 在 App.jsx 中，将目标网络从 localhost 改为 rinkeby。

Etta: 好了。现在我的前端已经连上 Rinkeby 了。你可以看到通知系统也变得更高级了（使用了 Blocknative）。

Austin: 最后一步，打包前端并发布。运行： yarn build 接着运行： yarn surge

Etta: 自动生成了一个网址：moaning-anger.surge.sh。

Austin: （接过屏幕）好的，我访问这个网址。我用我的真实 Metamask 钱包连接。它提示我需要切换到 Rinkeby 网络。切换后，我点击“Mint”，成功了！我铸造了一头属于我自己的水牛。

Austin: 这就是挑战 0。你的目标是拥有一个可以分享给朋友的网址，让他们也能在你的应用上铸造 NFT。 快去 speedrunethereum.com 开始你的挑战吧！

Austin: 谢谢大家。祝你好运！
