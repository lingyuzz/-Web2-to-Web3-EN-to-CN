(Austin Griffith) 哟，大家好，我是 Austin Griffith。 今天是第 5 天。我和 Carlos 还有 Etta 在这里。今天我们要成为超级用户（Power Users）。 我们要进行一大堆交易，我们会做一些愚蠢的交易，我们会让它们失败，我们会向你展示所有那些你在使用 MetaMask 时会遇到的令人沮丧的时刻。

(Austin Griffith) Etta，你来共享屏幕吧？ 顺便说一下，我有 WalletConnect。也许我们稍后应该演示一下 WalletConnect，看看如何用 Rainbow 钱包连接并进行交易。

(Austin Griffith) 开始吧。我们来做一些 Sanford 的交易。 我们打开 MetaMask。我们可以直接在这里转账，或者去 OpenSea。 我们之前已经把 ETH 换成了 DAI。 Etta，你试试发 5 DAI 给 AustinGriffith.eth，然后我再发回来。这只是为了演示如何把代币转出钱包。

(Etta) 好的，输入 AustinGriffith.eth。它识别出了 ENS，显示了那个爵士乐风格的头像。 我要发 5 DAI，Gas 费大概是 3 美元。

(Austin Griffith) 这并不贵。Gas 现在还行。发送吧。 我们一如既往地去那个“中立的第三方” Etherscan 检查。 在这里，并没有真正的 ETH 在移动。我们是在与 DAI 的智能合约交互。如果你点开那个 Token Transfer 的箭头，你会看到本质上我们是告诉 DAI 合约：“把这边的余额减 5，那边的余额加 5”。 就像 Carlos 之前说的，代币不是在网线里飞，只是账本上的数字变了。

(Austin Griffith) 好了，现在我们来做一个糟糕的交易。 现在的 Gas 大概是 33 Gwei。 Etta，再给我发 5 DAI，但这次我们去“编辑 Gas 费”，点“高级（Advanced）”。 我们要把 Max Fee（最大费用） 设置为 10 Gwei。 这远低于当前的市场价（27-36 Gwei）。 这意味着我们在**内存池（Mempool）**里的出价太低了，矿工们都很贪婪，他们不会打包我们的交易。

(Austin Griffith) 我们把这笔交易“漂（Float）”进了内存池。 Etherscan 上显示预估时间：“超过 1 小时”。 这就是很多用户会遇到的情况：你想省钱，结果交易卡住了。 在这里必须讲一下 Nonce（随机数）。 以太坊为了防止重放攻击（Replay Protection），每笔交易都有一个序号。 如果你现在的这笔卡住的交易 Nonce 是 6。那么在你这笔交易完成之前，Nonce 为 7、8、9 的交易全部都不会执行。 就像排队一样，6 号没过，后面的都得等着。

(Austin Griffith) 怎么解决？加速（Speed Up）。 MetaMask 有个加速按钮。它本质上是发一笔新的交易，拥有相同的 Nonce（6），但是更高的 Gas 费（比如 31 Gwei）。 矿工会看到两笔 Nonce 为 6 的交易，他们会选钱多的那笔，丢弃钱少的那笔。 看，交易瞬间就成功了。

(Austin Griffith) 有时候 MetaMask 会彻底犯晕。这时候我们需要 重置账户（Reset Account）。 这听起来很吓人（红色的按钮），但它不会删除你的私钥或资金。它只是清空了 MetaMask 本地的交易历史记录（尤其是那些卡住的等待中的交易）。我们演示一下，看，钱还在，只是记录清空了。

(Austin Griffith) 接下来，取消交易（Cancel Transaction）。 MetaMask 有取消按钮，但我们要学点高级的：手动取消。 我们再发一笔低 Gas（10 Gwei）的必死交易（Nonce 7）。它卡住了。 现在，我们给自己发一笔 0 ETH 的交易。 在“自定义 Nonce”里填上 7。 把 Gas 费设高。 原理是：我们用一笔“转给自己 0 元”的高价交易，覆盖掉了那笔“转给 Austin 5 DAI”的低价交易。 这实际上就是“取消”的底层逻辑。 (Austin 吐槽：MetaMask 的 UI 甚至有时候不让我们这么做，太令人沮丧了。欢迎来到 Web3！)

(Austin Griffith) 好了，接下来我们去 Layer 2 (Optimism)。 为什么要用 L2？因为 L1（主网）太贵了。L2 更快、更便宜。 我们要用 桥（Bridge）。 我们去 Optimism Gateway。我们要把主网的 ETH 存入 Optimism。 这需要 1-2 分钟。这段时间最吓人：你的钱在 L1 没了，在 L2 还没到。

(Austin Griffith) 在等待的时候，我们需要在 MetaMask 里添加 Optimism 网络。 现在很多应用会自动添加，但我们手动搜一下 RPC 添加进去。 钱到了！现在我们在 Optimism 上了。 Etta，给我发 2 美元试试。 看！费用只要 0.31 美元，而且瞬间到账。这就是 L2 的体验。

(Austin Griffith) 我们去 Quixotic（Optimism 上的 NFT 市场）买个 Loogie（Austin 的 NFT 项目）。 花费 $37，Gas 费几乎可以忽略不计。瞬间买到。 我们甚至可以把它挂单拍卖。

(Austin Griffith) 接下来是 DeFi（去中心化金融）。 我们回到主网。去 Uniswap 或 Matcha。 如果你要把 ETH 换成 DAI，只需要一笔交易。 但是，如果你要把 DAI 换成 ETH（或者任何 ERC-20 代币换别的），你需要两笔交易：

Approve（授权）： 允许 Uniswap 合约动用你的 DAI。

Swap（交换）： 实际的兑换。 很多新手会忘了第一步，或者纳闷为什么要交两次钱。

(Austin Griffith) 我们再去 Aave 试试借贷。 我们可以存入 ETH 作为抵押品（Collateral），然后借出 DAI。 这就是超额抵押贷款。 (Austin 吐槽：Gas 费太贵了，存 $100 要花 $20 手续费，还是算了吧。在 L2 上做这些更有意义。)

(Austin Griffith) 最后，我们要设置一个 Gnosis Safe (现为 Safe) 多重签名钱包。 助记词是很脆弱的。如果丢了或者被偷了，钱就没了。 Multisig（多签）更加安全。 我们在 Optimism 上创建一个 Safe。设置 2-of-4 签名。 意味着我们 4 个人（Austin, Etta, Carlos, Carl）里，只要有任意 2 个人签名，就能动用资金。 如果 Sanford 的私钥丢了，我们其他几个人可以帮他把钱救出来。

(Austin Griffith) 我们往 Safe 里转点钱。 然后发起一笔交易。

Austin **提案（Propose）**并签名（这是链下的，不花钱）。

Etta 看到提案，**确认（Confirm）**并签名。

一旦凑齐 2 个签名，就可以执行（Execute）（这步上链，需要花 Gas）。 成功！我们用多签钱包转账了。

(Austin Griffith) 专家模式（Expert Mode）：WalletConnect 这真的非常酷。 Gnosis Safe 本身是一个智能合约地址。 我们可以通过 WalletConnect，把 Safe 连接到 Uniswap。 Uniswap 会以为我们是一个普通用户，但实际上我们是一个多签合约。 我们在 Uniswap 上点“交换”，它会把交易请求发回到 Safe 的界面里，等待我们多个人签名确认。 这展示了 可组合性（Composability） 的强大——一个智能合约（Safe）可以像人一样操作另一个智能合约（Uniswap）。

(Austin Griffith) 好了，第 5 天结束了。 我们今天经历了很多失败、卡顿和复杂的交互。 如果你还没有被 Web3 搞得心态爆炸，说明你用得还不够多！ 去使用它，去受挫，然后回来——帮我们修复它，建设未来。 下周见，我们要开始**写脚本（Scripting）**了！我们将学习如何用代码来编排这一切。
