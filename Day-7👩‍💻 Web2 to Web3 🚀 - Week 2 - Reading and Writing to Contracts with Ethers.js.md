Austin: 走起！大家好，我是 Austin。我和 Etta、Carlos 在一起。我们现在进入了第 2 周的第 2 天，正处于编写脚本的热潮中。我们正在学习提供者（Providers）、签名者（Signers）、处理助记词文件并将其加载到脚本中，甚至还在编写合约交互脚本。今天的主题是编写与智能合约交互的脚本。我们将了解到一切皆交易——关键在于调用数据（Call Data），对吧？如果你想与合约对话，并不是去“捅”一下 App，而是构建一个交易并发送它，当交易被打包进区块时，它最终会触发合约。

好了，Carlos，我要在本地启动我的环境以便跟上你的节奏。你先开始告诉我们怎么做，我也会在我的机器上同步操作并随时加入，好吗？

Carlos: 好的，没问题。让我分享一下屏幕。大家可以看到大海、陆地，还有 Sanford 和 Vitalik 的余额页面。

这就是我们到昨天为止的进展。我们创建了 Provider 文件和 Wallet 文件，做了些调用和测试。镜头外我唯一做的是把这些文件放进了 day1 文件夹，因为今天我们要创建 day2 文件夹。我还初始化了 Git 项目并提交了现有内容。

Austin: 那个仓库公开了吗？我们可以抓取代码吗？

Carlos: 之后会公开的。在家观看的同学可以轻松 fork。现在我们先现场演示。开始前，我想先回顾一下昨天的内容。

我们将一直使用 Provider、Wallet 和 Signer。所以我们可以创建一个 工具文件（Utility file），把所有 Provider 和 Signer 的设置都放进去，然后从其他脚本中导入。这样我们就不用每次都去实例化钱包了。

Austin: 没错。我本地有 30 个项目，每个项目基本都有一个专门生成的本地助记词文件。脚本把助记词加载到钱包，我给它转点钱，然后编写交互逻辑。有一个工具文件能帮我们处理这些杂活，让我们能专注于核心的合约交互代码。

Carlos: 好的，先创建 day2 文件夹和 utils.js 文件。

首先导入 ethers。我敢打赌每个脚本都是从导入 ethers 开始的。

Carlos: 昨天我们学习了 Provider。现在写一个 getProvider 函数。我们会设置一个 mainnet 标志位，默认值为 false。如果调用时不传参数，它默认返回 Rinkeby 测试网的 Provider；如果传 true，则返回主网（Mainnet）Provider。

Austin: 这样很好。我们要确保通过环境文件（.env）加载 API Key。如果你不使用环境文件，而是把助记词或私钥直接写在代码里，那非常容易意外发布到 GitHub 上。

即使使用 .env 文件也有点可怕，你应该只在里面放测试网的 ETH。如果它是真正的主网脚本，必须放在非常安全的地方。如果你的 .env 文件被提交到了 GitHub，你的钱就全没了。所以第一件事就是：引入环境文件，并在 .gitignore 中忽略它。 否则你会输得很惨。

Carlos: 昨天我们已经创建了 .gitignore 来忽略 node_modules 和 .env。现在测试一下 getProvider，通过 getNetwork 看看我们是否连上了正确的网络（主网 ID 是 1，Rinkeby 是 4）。好的，正常工作。

接下来是生成新钱包的函数 generateWallet。我们可以使用 ethers.Wallet.createRandom()。

Austin: 理论上你可以自己生成 64 位的十六进制私钥，但 Rick Moo（Ethers.js 作者）在 createRandom 里加入了一些特殊的随机性处理，这样更安全。

Carlos: 我们可以把生成的助记词保存到文件里。为了演示，我会在镜头外把新生成的私钥复制到 .env 文件中。

好了，现在我们已经有了一个新地址，且没有在镜头前泄露私钥。接下来在工具文件里写一个 getSigner 函数。

Austin: 我的拼写太差了。

Carlos: getSigner 需要一个 Provider 和私钥。默认连接到 Rinkeby，但也可以通过标志位连接主网。

Austin: 展示 Signer 和 Provider 的区别非常重要。它们互不干扰，但可以随时连接。你可以把你的 Signer 连接到不同的网络（测试网、L2 或以太坊主网），因为它们都是 EVM 兼容的，除了链 ID（Chain ID）和速度，从我们的视角看，工作原理是一样的。

Etta: 我一直把 Signer 看作是“身份验证”部分。你用你的地址签署交易，别人就能知道是谁发的。

Austin: 没错。Signer 就是你生成的私钥，它是隔离的；Provider 是你与网络的连接。你在本地签名，然后通过网络发送去挖矿。

Carlos: 我们要导出这些函数。因为我们在 package.json 里设置了 "type": "module"，所以我们可以直接用 ES6 的 export 语法。

现在，让我们用刚才写的工具函数重写昨天的“发送 ETH”脚本。

Austin: 那个工具文件能发给我们吗？我写了一半，但 Infura 的端点没打对。

Carlos: 没问题，发在聊天框了。

现在在 send_eth.js 里，我们可以直接用 getProvider 和 getSigner。我们要给 Sanford 的地址转余额的 10%。

Austin: 注意，在文件系统中创建助记词，然后又把私钥贴进常用的 MetaMask 是有风险的。如果你系统上的私钥泄露了，你 MetaMask 里的钱也就危险了。建议专门准备一个开发用的 MetaMask 账号。

Carlos: 没错。谁能给我转点 Rinkeby 测试币？我的地址发在聊天框了。

Austin: 我给你转 0.5 个。如果大家在家练习时没币，可以去搜 Rinkeby Faucet（水龙头）。测试网不如以太坊主网安全，经常会受到攻击或关停。

Carlos: 收到币了。现在我们来运行脚本。首先通过主网 Provider 解析 sanfordstout.eth 得到地址，然后用 Rinkeby Signer 发送交易。

Austin: 这里的重点是：你的 App 可能需要一个主网 Provider 来解析 ENS 身份，同时需要另一个 Provider 来处理实际业务（比如在 L2 或测试网上发交易）。

Carlos: 交易已经发送到内存池（Mempool）。记住，交易哈希是确定的，即使交易还没被挖出来，你也可以预先推导出它的哈希。

Austin: 第 15 行代码在等待交易进入内存池，第 22 行在等待交易被矿工打包。

Carlos: 交易确认了！Sanford 收到了 10% 的余额。这就是可编程货币的魅力。你可以设置定时任务（Cron Job）让它自动运行。

Austin: 好了，我的环境也配好了。接下来是不是该聊聊智能合约了？

Carlos: 对。先尝试从合约中读取（Read）数据，然后再写入（Write）。我们拿上周创建的 Sanford Stout NFT 合约来练手。

在 Ethers 中，实例化一个合约对象需要三个要素：地址（Address）、ABI、以及 Signer 或 Provider。

Austin: 如果你只是读取余额，用 Provider 就够了（只读连接）；如果你要发送交易，就需要一个连接了 Provider 的 Signer（写入连接）。

Carlos: 这个 NFT 合约部署在 Rinkeby。我们要去 Etherscan 当一回区块链侦探，找到这个合约的地址。我们在 Sanford 的 Rinkeby 交易记录里找到了那个 mint 函数调用，点进去就看到了合约地址。

Carlos: 接下来是核心内容：ABI。它告诉我们合约有哪些函数、参数是什么。

Austin: 当你部署合约后，Etherscan 上默认只能看到字节码（Bytecode），那是一堆十六进制乱码。只有当开发者“验证”了合约，上传了源代码，Etherscan 才会显示 ABI。有了 ABI，任何人都能通过脚本与该合约交互。

Carlos: 我们把 ABI 复制下来，存成一个单独的 abi/SanfordNFT.json 文件，并导出它。

现在我们来读一下铸造价格 mintPrice。记得它返回的是 BigNumber，我们需要用 formatEthers 转换成 ETH。运行一下…… 价格是 0.01 ETH。

接下来，我们要尝试在脚本里**铸造（Mint）**一个 NFT。

Austin: 复制读取脚本，把它改成写入脚本。这次我们需要 getSigner。

Carlos: 查一下合约代码或 ABI。mint 函数不接受参数，但它是 payable（可支付的）。

如果我们直接调用 mint() 而不付钱，会发生什么？

Austin: 我们会得到一个错误。Web3 的错误信息 99% 都是没用的废话。

Carlos: 但如果你仔细看，会看到 insufficient ETH amount（ETH 金额不足）。这是因为合约代码里有一个 require 判断。

Austin: 这里的重点是交易的解剖：包含 to（发给谁）、from（谁发的）、value（随笔带了多少钱）和 data（调用什么功能）。

Etta: payable 函数对我来说很新鲜。它看起来不接受输入参数，但它需要通过原生支付层转账。

Austin: 合约也有自己的地址。它像一个大型多人在线游戏里的玩家，可以接收和发送 ETH。如果你写合约忘了写提现函数（Withdraw），钱就会永远锁在合约里。

Carlos: 在 Ethers 里发送 value 很简单，在函数调用的最后一个参数里传一个对象即可：{ value: mintPrice }。

Austin: 记住，如果你是手动输入金额，一定要用 parseEthers("0.01") 转成大数。

Carlos: 好了，铸造交易已发出！在 Etherscan 上可以看到，16 秒前调用了 mint 方法。

我们来看一下 调用数据（Call Data）。

这里有一个方法 ID：0x1249c58b。它是 mint() 这个字符串经过 Keccak-256 哈希后取前 4 个字节得到的。

Austin: 没错。合约就是通过这 4 个字节的“函数选择器”知道你想调用哪个函数的。一切皆交易。

Carlos: 我们甚至可以不用 Ethers 的合约助手，直接写一个原始交易（Raw Transaction）。手动指定 to 地址、value 和这串 data。

Austin: 原始交易非常强大。部署合约时没有 to 地址，data 字段里就是合约的字节码。

Carlos: 这种手工打造交易的感觉很棒。我们还可以手动设置 Nonce 和 Gas Price。

比如，我们先用一个极低的 Gas Price（1000 wei）发送交易。它会卡在内存池里。然后，我们提交一个 Nonce 相同但 Gas Price 更高的交易。

Austin: 这就是 MetaMask 里“加速（Speed Up）”按钮的原理：用相同的 Nonce 提交一个更高出价的交易，覆盖掉旧的。

Carlos: 运行脚本…… 成功了！我们证明了可以手动加速交易。

Austin: 好了，现在轮到 Etta 了。我们要挑战一个更高难度的任务：在**主网（Mainnet）**上发送 DAI（一种稳定币）。

Etta: 好的。我先克隆代码，安装依赖。

Austin: 别忘了根据 README 配置 .env 文件。生成一个新的助记词，给它转一点钱。

Carlos: 记住 Opsec（操作安全）：为每个新脚本生成新地址，只转入刚好够用的钱。别把存有全副家当的私钥贴进来。

Etta: 好的。我写了一个 get_address.js 来获取我的主网地址。

Austin: 我给你转 10 美元的 DAI，再转点 ETH 当 Gas 费。在以太坊主网上，发送 10 美元的 DAI 居然要花 8 美元的 Gas 费，真疯狂。

Etta: 余额到账了。现在我们要与 DAI 合约交互。首先去 Etherscan 复制 DAI 的 ABI。

Austin: DAI 合约里锁了价值 5 亿美元的代币，因为很多人意外地直接把币转给了合约地址，而合约没有提现功能。

Carlos: 导入 ABI，实例化合约。注意，DAI 的余额查询函数叫 balanceOf（驼峰命名）。

Etta: 运行脚本…… 成功读取，我有 10 美元的 DAI。

Austin: 现在的目标是：发送 10% 的 DAI 给 Sanford。

Etta: 我们需要调用 transfer 函数。这需要一个主网 Signer。

Austin: 这里的架构很有意思：你有一个专门用于“读”的 Provider（可能连的是 Alchemy），还有一个用于“写”的 Signer（连的是另一个 RPC）。这种读写分离能让 App 响应更快。

Carlos: 调用的参数是：目标地址和金额。金额也要用 parseEthers 转成大数。

Etta: 交易已发送！Gas 费花了 11.5 美元，比转账金额还贵，但这为了科学！

Austin: 我们去 Etherscan 看一下。在“ERC-20 Token Transfers”选项卡里可以看到这笔转账。

来看一下这笔交易的 Call Data。

方法 ID 是 0xa9059cbb，这是 transfer(address,uint256) 的哈希前缀。参数 0 是地址，参数 1 是那 5 美元的大数十六进制。

Austin: 我们做到了！通过编写脚本，我们解析了 ENS 地址，然后调用 DAI 合约完成了转账。

Carlos: 今天的重点是：理解 Provider 和 Signer 的区别，学会处理环境文件，掌握大数运算，并理解如何与合约进行读写交互。

Austin: 所有的脚本交互本质上都是交易。明天我们会深入探讨更多自动化和调用数据的玩法。下期见！

Carlos & Etta: 拜拜！
