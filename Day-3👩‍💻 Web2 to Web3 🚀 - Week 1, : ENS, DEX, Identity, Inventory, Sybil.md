(Austin Griffith) 大家好，我是 Austin Griffith。 我和 Carlos 还有 Etta 在这里，我们正在录制第一周的第三天课程：如何成为以太坊的超级用户，并学习如何在以太坊上进行构建。 今天，我们将使用钱包与一些 Web3 服务进行交互。我们将学习 身份（Identity），以及你的身份和你的 库存（Inventory，指资产） 是如何跟随你从一个服务流转到另一个服务的。所有的这些服务背后都是由智能合约支持的。我们会讲到智能合约以及它们是如何运作的。

(Austin Griffith) 我想最好的开始方式是让 Etta 在她的 MetaMask 里创建一个全新的账户，然后我给它转点 ETH。接着 Etta 注册一个 ENS（以太坊域名服务） 地址。我们开始吧？

(Austin Griffith) 上周我们设置了 MetaMask，学习了助记词和如何保护它。 现在我们要在现有的 MetaMask 里创建一个新账户。记住，一套助记词可以创建无限个账户。(Etta) 好的，我已经有几个账户了，我要创建一个新的。我们就叫它 “Zoom” 吧。不太有创意，但也行。我现在在主网（Mainnet）上。

(Austin Griffith) 你把那个账户地址发给我，我给你转点 ETH，这样你就不用自己付 Gas 费了。(Austin 切换屏幕) 我要发点 ETH。多亏了 EIP-1559 升级，现在发送 ETH 变得非常顺滑，Gas 费估算也很准确。除非遇到 NFT 发售（Drop），那时候 Gas 会飙升。

(Austin Griffith) 你看，Etta 发给我的地址是 0xAE9459... 这很难记。如果不小心输错了就麻烦了。所以一会儿我们会讲 ENS，给账户起个名字。 现在的 Gas 是 92 Gwei。我发 0.25 ETH 过去。我会把 Gas 费设置得比当前稍微低一点，比如 91 Gwei，看看能不能省点钱。这就像我们在竞价区块空间。

(Austin Griffith) 交易成功了！Etherscan 上已经显示 Austin 给 0x8a94... 转了 0.25 ETH。 现在交给你 Etta，我们来注册 ENS。

(Etta) 好的，钱到账了。现在我们去 ENS (app.ens.domains)。我们要给这串长长的地址起个好名字，就像 DNS 一样。

(Austin Griffith) Carlos，你想解释一下它和 DNS 的相似之处吗？ (Carlos) 当然。DNS 是为了让你不用去记服务器的 IP 地址。ENS 也是一样，你不用记 Etta 的长地址，只需要记住 etta.eth 这样简单的名字。而且它也支持子域名（Subdomains），比如 game.etta.eth。

(Austin Griffith) 子域名很强大。比如我有 punk.austingriffith.eth 专门用来放我的 CryptoPunk。 我们要给这个“Zoom”账户注册个名字。(Etta) 连接钱包。这里有个安全提示：MetaMask 会弹窗问你是否允许连接。这是为了保护隐私，网站不会直接知道你的地址，除非你点击连接。

(Austin Griffith) 我们叫它什么呢？Zoom.eth 肯定被注册了。 我们试试随机名字生成器吧。(Austin 搜索名字)"Sanford Stout"。这名字听起来不错，像是个周五会戴领结的绅士。 我们就注册 SanfordStout.eth。

(Austin Griffith) 注册 ENS 需要两步：

1.	提交（Commit）： 这是一个防抢注（Front-running）机制。如果我直接说“我要注册 SanfordStout.eth”，有人（或机器人）可能会看到这笔交易，然后用更高的 Gas 费抢先打包交易，把名字抢走。所以我们先提交一个哈希，等一分钟。

2.	揭示（Reveal）/ 注册（Register）： 一分钟后，我们要发送第二笔交易来正式注册。

(Austin Griffith) 现在我们发起了第一笔“提交”交易，大概花费 5 美元。 我们在跟智能合约交互。这是我们第一次直接调用智能合约的函数。 交易成功了。现在我们需要等待一分钟的保护期。

(Austin Griffith) 好了，一分钟到了。这名字归我们了。 点击“注册（Register）”。这笔交易会贵一点，因为我们实际上是在铸造一个 NFT，并写入更多数据到链上。 交易发送了。 我们在 Etherscan 上可以看到，我们调用了 registerWithConfig 函数。 成功！我们现在拥有了 Token ID 为巨大数字的 NFT，这代表了 SanfordStout.eth 的所有权。

(Austin Griffith) 现在，如果你在 Etherscan 上搜 SanfordStout.eth，它会解析出我们的地址。 如果在我的钱包里，我输入 SanfordStout.eth 给 Etta 转账，我也能直接识别出地址。这比复制粘贴那串乱码强多了。

(Austin Griffith) 还有最后一步：反向解析（Reverse Record）。 我们现在可以通过名字找到地址（正向）。但如果我们只知道地址，怎么知道名字呢？ 这就像你登录一个网站，网站只知道你的地址 0x...，它需要通过“反向解析”来查找并显示你的名字 SanfordStout.eth。 Etta，在 ENS 界面上设置一下“Primary ENS Name（主 ENS 名称）”。这需要再发一笔交易。

(Austin Griffith) 好了，身份搞定。我们现在是 Sanford Stout 了。 这个身份会跟随我们去任何 Web3 应用。 现在，Sanford Stout要去 Uniswap 换点代币。

(Etta) 打开 Uniswap.org。连接钱包。 看！右上角直接显示了 SanfordStout.eth。这就是身份的可移植性。两个完全不相关的服务（ENS 和 Uniswap），共享同一个身份。

(Austin Griffith) 我们要把 0.1 ETH 换成 DAI（一种稳定币）。 这里要讲一下 DEX（去中心化交易所） 和 CEX（中心化交易所） 的区别。

•	CEX (如 Coinbase): 这是一个订单簿（Order Book）系统，是个大数据库。有人挂单卖，有人挂单买。

•	DEX (如 Uniswap): 这是一个智能合约。它没有中心化服务器。它使用流动性池（Liquidity Pools）。合约里存着一堆 ETH 和一堆 DAI。

(Austin Griffith) 你可以把它想象成一个自动售货机。 你往里扔点 ETH，天平倾斜了，机器吐出一点 DAI，直到天平恢复平衡。 这就是自动做市商（AMM）。任何人都可以把自己的钱放进去提供流动性，并赚取交易手续费。

(Austin Griffith) 我们来换点 DAI。 DAI 是什么？它是一种与美元 1:1 挂钩的稳定币。 但这不像 USDC 那样银行里存着美元。DAI 是通过**超额抵押（Over-collateralized loans）生成的。 比如我在 MakerDAO 里锁仓 $100 的 ETH，然后借出 $60 的 DAI。因为锁住的价值（$100）远大于流通的价值（$60），所以它是安全的。如果 ETH 价格大跌，系统会自动清算（Liquidate）**你的抵押品来偿还债务。 这比那些依靠算法（Mint/Burn）维持稳定的代币（Austin 暗示了类似 Terra/Luna 的死亡螺旋案例）要安全得多。

(Austin Griffith) 我们完成了交换。现在我们有 ETH 和 DAI 了。 但是 MetaMask 默认看不到 DAI，我们需要手动添加代币显示，或者... 我们去另一个“中立第三方”网站：Zapper.fi。

(Austin Griffith) 在 Zapper 上，我们甚至不需要连接钱包。 只要在搜索框输入 SanfordStout.eth。 看！它显示了我们所有的资产：$237 的 ETH 和 $200 的 DAI。 这再次证明了：你的身份（ENS）和你的库存（Inventory/资产）是跟随着你的。 你去任何 Web3 网站，它们都能读取这些公开数据。

(Austin Griffith) 最后聊聊 女巫攻击（Sybil Attack）。 我们刚刚凭空创造了一个叫 Sanford Stout 的“人”。他有名字，有资产，看起来像个真人。 如果在“一人一票”的治理投票中，我只要创建 1000 个 Sanford Stout 就能控制投票，这就是问题所在。 所以现在很多项目（如 Gitcoin Passport）在研究**“人格证明（Proof of Personhood）”**，通过分析你的链上行为（是否投过票？是否签过多签？是否持有老资格的 NFT？）来给你的“真人程度”打分。

(Austin Griffith) 总结一下： 今天我们成为了以太坊的超级用户。
1.	我们创建了新账户。
2.	我们注册了 ENS 域名（SanfordStout.eth），建立了链上身份。
3.	我们使用了 Uniswap（DEX）交换代币，体验了身份的跟随性。
4.	我们使用了 Zapper 查看资产，体验了库存的跟随性。
5.	我们通过钱包直接与智能合约进行了交互。
谢谢大家，下节课见！
________________________________________
译者注（关键概念补充）：
1.	Gwei: 以太坊 Gas 的计价单位。1 Gwei = 0.000000001 ETH。视频中 Austin 提到的 "Gray" 其实是 Gwei。
2.	Sybil (女巫攻击): 指一个人通过创建多个虚假身份（账号）来控制网络或操纵投票。Austin 在视频末尾提到的 "civil resistance" 其实是 "Sybil resistance"（抗女巫攻击）。这是 Web3 社区治理中非常重要的概念。
3.	DAI vs UST: Austin 提到的“死亡螺旋（Death Spiral）”是指算法稳定币（如 Terra 的 UST）在 2022 年的崩盘。他强调 DAI 这种“超额抵押”模式更安全，因为它是用真金白银（ETH等）超额担保出来的。

