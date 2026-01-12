(Austin Griffith) Boom！我们开始第 4 天了。 我是 Austin，还有 Etta 和 Carlos。今天是 NFT 日，成为以太坊超级用户第一周的第 4 天。 今天我们要买一些 NFT，发送一些 NFT，学习什么是非同质化代币（Non-Fungible Tokens）。 Etta，分享你的屏幕吧。我们的角色 Sanford Stout 已经拥有一个 NFT 了，因为他注册的 ENS 域名本身就是一个 NFT。

(Austin Griffith) 那是 Sanford 的钱包，我们有 $230 美元的 ETH。 我们现在去 OpenSea。 这又是 Web3 服务的一个例子：OpenSea 是一个 NFT 市场。我们的身份和库存跟随我们来到了这里。看，它已经显示了我们的第一个 NFT：以太坊域名服务（ENS）。 如果你把这个 ENS NFT 发给别人，他们就拥有了这个名字的所有权，可以控制它的解析。

(Austin Griffith) 咱们去买个 CryptoPunk 吧？（开玩笑，买不起）。 在深入代码之前，我们先体验一下。NFT 是数字所有权。 这其中有**链上出处（On-chain Provenance）**的概念。艺术家铸造了一个系列，每个人都能在链上看到是那个特定的艺术家铸造的。如果我有样学样铸造了一个“假”的，市场会立刻分辨出来，因为它不是来自原始合约。 这赋予了它价值（当然也有很多垃圾，这是一个无许可的环境）。

(Austin Griffith) 我们在 OpenSea 上可以看到各种属性（Properties）。 有些 NFT 有效用（Utility），比如代币门槛（Token Gating），你需要持有 NFT 才能进入聊天室或投票。 或者像 Chicken Derby 这种游戏，你需要买 NFT 才能玩。 还有那些显示在 Polygon 链上的（紫色 ETH 图标），那是侧链/L2，我们今天先专注在以太坊主网。

(Austin Griffith) 与其在 OpenSea 上大海捞针，不如去支持一个我们要支持的朋友。 Carlos 提到了 MetaAvatar。这是一组链上（On-chain） NFT。 这里要区分一下：

链下存储（Off-chain/IPFS）： 大多数 NFT 只是链上的一个哈希，指向存储在 IPFS 上的文件（清单）。

链上存储（On-chain）： 像 MetaAvatar，智能合约直接进行渲染，生成 SVG 代码。所有数据都在链上。

(Etta) 我们在这个项目的官网上。 注意，有些 Web3 网站做得不够好，没能识别出我们的 ENS 名字（Sanford Stout），只显示了地址。但这不影响功能。 我们点击 Mint（铸造）。

(Austin Griffith) 我们要把钱发给一个智能合约 0x8a0...。 我们可以点击这个地址去 Etherscan 查看。 Web3 的美妙之处在于开源。我们可以看到智能合约的代码。虽然作为普通用户你可能不会每行都看，但我们要展示这一点：你可以去验证它。 我们支付 0.0x ETH 加上 Gas 费。交易发送。

(Austin Griffith) 铸造成功！我们拥有了一个 MetaAvatar。 现在我们去 Zapper 看看。Zapper 的索引器可能还没刷新出来，但这需要时间。 再去 Rarible（语音识别误为 rabo）看看。Rarible 是另一个市场。 这里有个有趣的现象：Rarible 没有显示我们的 ENS，也没有立刻显示我们的新 NFT。这其实有点像 Web2 式的审查——平台决定显示什么。在 Web3 原则中，只要符合标准，它就应该显示出来。 我们去 Foundation 看看？也是一样，他们策展（Curate）得很严格。

(Austin Griffith) 但这不影响所有权。只要符合标准，我们在哪里都能买卖。 现在我们来深入技术一点。 Sanford 可以铸造一个基于 IPFS 的 NFT 吗？ Carlos 部署了一个测试合约。我们可以直接通过 Etherscan 来铸造。

(Austin Griffith) 这让我想起 Loot。 Dom Hofmann 创建了 Loot NFT。它没有前端网站，你必须去 Etherscan 上直接调用合约来铸造。它只有黑底白字的文本（比如“神圣长袍”），但这激发了极大的可组合性（Composability），社区基于这些文字构建了游戏和生态。

(Carlos) 这是我部署在 Rinkeby 测试网上的合约。 我们可以看代码：

totalSupply = 100：总供应量限制。

require(counter < totalSupply)：如果你想铸造，必须还没卖完。

ownerMint：作为所有者，我可以免费铸造。

(Austin Griffith) 大家可以看到代码里并没有 setTotalSupply 这种后门函数，所以即使是所有者也不能凭空增发超过 100 个。这就是代码即法律的信任基础。 我们在 Etherscan 的 "Write Contract" 页面，连接钱包（切换到 Rinkeby），调用 ownerMint。

(Austin Griffith) 铸造成功。现在我们去 "Read Contract"（读合约）。 我们查 balanceOf（余额）：是 1。 我们查 tokenURI(1)（元数据链接）：返回了一个 ipfs://... 的链接。

(Austin Griffith) IPFS（星际文件系统） 与 内容寻址（Content Addressable）。 智能合约说：“代币 #1 属于 Sanford，它的数据在 IPFS 的这个哈希地址。” 我们去 IPFS 网关查看这个哈希。它是一个 JSON 文件（元数据），里面有名字 "Bison" 和一张图片的 IPFS 哈希。 再去查图片的哈希，我们看到了图片。

(Austin Griffith) (Austin 切换屏幕演示 IPFS 原理) 看这个 Buffalo（水牛）的元数据。 如果我把名字改成 "Bison"，它的哈希值就变了。 这就是内容寻址。如果内容变了，地址就变了。 这意味着，当你买 NFT 时，如果是指向 IPFS 的，你可以确信元数据是不可篡改的。 反之，如果 NFT 指向的是一个中心化服务器（如 api.game.com/token/1），开发者随时可以把那把“屠龙刀”换成“木棍”。那就是被 Rug（撤资/跑路） 的风险。

(Austin Griffith) 我们再看一眼代码，比较 Fungible (ERC-20) 和 Non-Fungible (ERC-721) 的区别。

Fungible (同质化): 就像一个大数组 mapping(address => uint256) balance。我们只跟踪余额。我有 50 个，你有 50 个，它们是一样的。

Non-Fungible (非同质化): 我们跟踪的是每个 ID 的拥有者 mapping(uint256 => address) ownerOf。代币 #1 属于 Alice，代币 #2 属于 Bob。

(Carlos) 这对我来说是个顿悟时刻：代币并不是在网线里飞来飞去。 它只是一个巨大的、异步的数据库（账本）。 当我发送 NFT 给 Etta 时，并不是文件传给了她，而是所有的节点都在账本上把“所有者”从 Carlos 改成了 Etta。

(Austin Griffith) 最后展示一个 完全链上（On-chain） 的 NFT：Loogies（语音识别误为 lugi）。 在这个合约里，tokenURI 不是返回一个链接，而是通过代码（base64 encode）直接生成 JSON。 颜色、形状、属性都存储在合约变量里。 这意味着其他智能合约可以直接读取这些属性（比如颜色），并以此构建游戏（例如：只有红色 Loogies 才能进入某关卡）。这就是链上数据带来的可组合性。

(Austin Griffith) 还有 版税（Royalties）。 你可以在合约里写一行代码：每次转售时，10% 的钱发给艺术家地址。这是智能合约赋予创作者的强大能力。

(Austin Griffith) 好了，NFT 日结束了！ 我们买了一个 NFT，我们通过 Etherscan 铸造了一个 NFT，我们学习了 IPFS 和链上数据的区别。 去挖掘那些垃圾堆里的创新吧，这就是 Web3 有趣的地方。 谢谢大家！

译者注（关键概念补充）：
IPFS (InterPlanetary File System): 一个去中心化的文件存储网络。它的核心特点是内容寻址（通过文件的哈希值来找文件，而不是通过文件名或服务器地址）。这保证了 NFT 数据的不可篡改性。

ERC-721: 以太坊上最通用的 NFT 标准。视频中 Austin 简化的代码演示了其核心逻辑：ownerOf[TokenID] = UserAddress。

Loot: 2021 年现象级的 NFT 项目。它完全没有任何图片，只有 8 行文字描述装备。这种“最小化”设计让社区可以随意在其之上构建游戏界面、故事情节等，是 Web3 可组合性（Composability） 的典范。

On-chain SVG: 指图片数据不是作为文件存储，而是作为代码（SVG 标签）直接写在智能合约里。浏览器读取合约数据后直接渲染出图片。优点是永久存在区块链上，不依赖 IPFS 节点，缺点是部署非常昂贵。
