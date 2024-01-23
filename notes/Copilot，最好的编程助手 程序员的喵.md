# Copilot，最好的编程助手 | 程序员的喵
今天下午我解决一个小问题的时候，在 Copilot 的帮助下快速给出了修复，这个工具似乎有些超过期望了，所以突然想写篇文章分享这个目前我最愿意付费的 AI 工具。

Copilot 价格是每个月 10 美金，但我至今还没付费过，感谢微软支持开源，从测试阶段就邀请我试用，到现在还一直在免费使用。Github 应该有些政策，比如如果你持续给一些 star 数比较多的开源项目做贡献，就可以免费使用 Copilot：

![](https://catcoding.me/images/ob_pasted-image-20240120212918.png)

我会给出日常碰到过的一些具体的实际案例截图，以方便你更直观地感受到这个工具准确度。

### [](#Manual-类查询 "Manual 类查询")Manual 类查询

我们在编程过程中经常会碰到一些命令的参数记不太清楚，这种问题很适合问 Copilot。这比自己去 Google 的感受好很多，因为他几乎能完全理解用户说的自然语言，而且给出的答案简介明了：

![](https://catcoding.me/images/ob_pasted-image-20240120224637.png)
  
比 Google 更好的地方在于上下文的交谈，比如我继续基于上面的问题说我的想法，他就能继续给出反馈，比如我说大概有个类似 `--exact` 的参数，Copilot 会继续给出使用案例。

Copilot 非常善于回答对这种 manual 类的问题，因为这是有标准答案的，并且我作为用户对这些是有判断的，只是我们细节上记不清楚了。

还有一次我发现跑测试的时候挂了，分析下来是这个命令行失败了（但既然 CI 是过的，所以必然只是在 MacOs 下失败了)：

```
diff -u --strip-trailing-cr -r -q A_file.txt A_file.txt
```

这是在 diff 同一个文件，所以必然应该返回 0，但在 MacOS 下这个命令会报错：

```
✗ diff -u --strip-trailing-cr  -r -q ./x.py ./x.py
error: conflicting output format options.
blah blah 一大堆错误 
blah blah 一大堆错误 
```

我知道这里面肯定是有参数冲突了，但我具体不知道是哪两个冲突了，所以这时候我问 Copilot：  
![](https://catcoding.me/images/ob_pasted-image-20240120230403.png)

可以看到这个解释非常清楚，并且帮我找到了问题的根源，所以我就能很快地发 PR 修复这个问题，并且我 PR 里的描述基本都是从 Copilot 里来的：  
[Fix diff option conflict in UI test #109036](https://github.com/rust-lang/rust/pull/109036)

[](#给出示例代码 "给出示例代码")给出示例代码
--------------------------

我们在写代码的时候，经常会出现固定的 Pattern，不同的语言对固定的 Pattern 有一些相对固定的代码样式。我很喜欢找 Example 类的代码，然后在这个基础上再思考或者修改：

![](https://catcoding.me/images/ob_pasted-image-20240120230905.png)

对这种情况我们需要给 Copilot 足够的信息，他给出的 Rust 代码通常是可直接编译通过的，但当然这些示例代码需要进行仔细的修改，但这也比我自己翻 Doc 会快很多。

[](#辅助排查问题 "辅助排查问题")辅助排查问题
--------------------------

VSCode 上的 Copliot 更新很快，肉眼可见地体验越来越好，现在我们可以选择一段代码，然后就选择的代码来进行提问。

有时候我会选中一个函数，然后问这段函数能不能重构得更简单一些，或者我们能不能用其他方式实现。

今天让我有欲望写下这篇分享的文章是因为这个问题：  
[Missing request extension: Extension of type](https://github.com/nervosnetwork/ckb/issues/4309)

这是一个有非常明确的报错的繁琐 issue，应该就是 Server 端限制了 HTTP 的请求类型，客户端通过 curl 发 GET 请求的时候报错了，只是这个报错信息看起来很不友好，而且和老版本行为不同。所以我就选中代码中对应的函数，然后问这里为什么会有这个错：

![](https://catcoding.me/images/ob_pasted-image-20240120232057.png)
  
其实我对 Copilot 解决这个问题不怎么报有信心，只是好奇先试了试，没想到 Copilot 真的能理解我的代码，并且指出了问题所在。注意看它加的注释就是我代码中缺少的逻辑 (之前的代码只是在 `enable_websocket` 的条件下才加载了 stream_config 这个 Extension)：

![](https://catcoding.me/images/ob_pasted-image-20240120232121.png)

加上它建议的代码之后，那个错误信息没了，但是现在发 GET 请求是另外一个问题：

```
Connection header did not include 'upgrade'
```

这看起来是服务端期望客户使用 Websocket，但是客户端只是在通过 Curl 发一个 GET 请求，并没有按照这个期望来。所以我继续问 Copilot：

![](https://catcoding.me/images/ob_pasted-image-20240120232647.png)

他给的回复里的代码并没有直接修复问题，但里面的  
`you can separate the handlers for POST and GET requests`  
提示了我应该尝试对 HTTP endpoint 和 Websocket endpoint 的 handler 进行分开，所以我一下想到了修复方案：

![](https://catcoding.me/images/ob_pasted-image-20240120232901.png)

[](#总结 "总结")总结
--------------

如今使用 Copilot 已经成为我的一个编程习惯，就如同之前我严重依赖 Google 一样，但这个工具明显比搜索引擎高级了一个维度，当然现在我还是依赖搜索，但使用比率明显下降了不少，搜索引擎更像是成了一个书签的角色了。

我之前认为 Copliot 这种工具甚至是这辈程序员所不能体验到的东西，在我第一次尝试到 ChatGPT 居然可以理解一个函数，并且找出函数中的问题时，就感觉新的编程时代来临了。

前段时间 Redis 的创始人在文章 [LLMs and Programming in the first days of 2024](http://antirez.com/news/140) 中写到：

> 随着时间的推移，我们见证了框架、编程语言、各种库的大量涌现。这种复杂性通常是不必要的，甚至无法自圆其说，但事实就是如此。在这样的情况下，一个无所不知的“白痴”成了宝贵的助手。

> 这是一个事实：现今的编程大多是在微调同样的内容，只是形式略有变化。这种工作并不需要太高的推理能力。

Copilot 已经可以在一些具体的编码问题上给到我们很多帮助，甚至你把这个当作一个包含万物的文档查询工具都非常有效。

当然没有银弹，Copilot 并不能解决编程中的所有问题，比如理解大规模的程序，通过深入分析去找出 bug，或者做设计问题中的各种折中和取舍，这些都是不能取代人类的，这也是我认为编程中的乐趣还没有完全消失。

我会把繁琐和细节的问题抛给 Copilot，然后更开心地做重要和有趣的部分。