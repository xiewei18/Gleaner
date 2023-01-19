# 放下 Jupyter Notebook，准备战斗
Save From : [放下 Jupyter Notebook，准备战斗](https://mp.weixin.qq.com/s/MxtBjyKTRSZEAfVIkAH-CA) 

## Content
从今天起：  

> 开始使用 GitHub；
> 
> 开始使用 git；
> 
> 减少使用 Jupyer notebook.

这是我 jupyter notebook 某个文件夹现在的样子：![](https://mmbiz.qpic.cn/mmbiz_png/m3WnZnGIHMia4EE6j4iaaasZiblTOvLbruW13icpMjia8YDaTKhzCpDykSibwwiaFRcb8tr158JBUCrjaawNZRMPLUSmg/640?wx_fmt=png)

两个周前，因为在一个新方向苦苦探索了好久没有任何突破，我打算接着三个月前的工作继续做。但是当我回去的时候，人都麻了。首先我找不到出某个图的代码了。然后就是如上图所示，我跟所有看这个图的人一样，不知道哪个版本是我需要的。还有就是，即便找着了代码，有些代码已经不是很能理解了。里面各种报错信息也是满满的，当时无所谓，因为有时候只是一些测试报错，运行的时候跳过即可。考虑到我还只是在读博的开始阶段，这简直就是灾难。

曾经的我，因为发现了 notebook 这种代码 + markdown 的模式，激动不已，感觉科研已经站在风口，随时准备起飞。就在两个周前，看到同事们都喜欢用 IDE，还很是不解。但现在，notebook 似乎成了一个阻碍。首先 Notebook 是很方便的工具，但是也存在很多问题，比如无法调用另一 notebook 中的函数，这就导致我需要不停地 duplicate。其他问题包括：![](https://mmbiz.qpic.cn/mmbiz_png/m3WnZnGIHMia4EE6j4iaaasZiblTOvLbruWiaQX3kPibLBpx8IGedOOO0XdrFjr4A1LLExhgvibCpVYgE2uXDBySVKnA/640?wx_fmt=png)

以上的 slides 来自我这周参加的所里组织的 **Good Scientific Code** 的 workshop。

以下是该 workshop 的简介：

> Scientific code is notorious for being hard to read and navigate, difficult to reproduce, and badly documented. One reason leading to this situation is that curricula that traditionally train scientists do not explicitly treat writing good code, and during the scientific life there is little time for the individual to practice this on their own. In this intensive two-day-block-workshop we will change that and teach you all you need to know to write code that is **Clear, Easy to understand, Well-documented, Reproducible, Testable, Reliable, Reusable, Extendable, and Generic**.

简单理解，就是教科研工作者，如何用软件工程的思维，提高工作效率。这实在是久旱甘霖。这个 workshop 目前 slides 在 GitHub 上已经开源，后续录屏也会上线。

**GitHub 网址**：https://github.com/JuliaDynamics/GoodScientificCodeWorkshop.git

The workshop is divided into the following six blocks:

*   **Version control**: retraceable code history using git
    
*   **Clear code**: write code that is easy to understand and reason for
    
*   **Software developing paradigms**: write your code like a software developer
    
*   **Collaboration & publishing code**: modern team-based development on GitHub
    
*   **Documenting software**: documentation that conveys information efficiently and intuitively
    
*   **Scientific project reproducibility**: publish reproducible papers
    

感兴趣的同学可以直接去看 slides，实际上，他把 slides 当成字幕的。所以我不会复述这个 workshop 讲了什么，下面我罗列一些我仍然印象深刻的点：

首先是 version control with git。解决的痛点就是 duplication。像我上面的 jupyter notebook，文件名很像的文件中，有很大一部分是我打算尝试一些新的东西，又不想把原代码毁掉。所以就复制一个，然后修改这个复制版本。git 的理想是，一个 repository 中有一个多个 branch，其中只有一个 main branch。main branch 可以看作是你的确定版本，如果不想这个版本被修改，就新建一个 branch，然后在这个 branch 中做修改，等到觉得没有问题了，再并入 main branch。当然，这只是我浅显的理解。git 的教程网上很多，以下是一个简单的开始：

* * *

> 首先，想把一个文件夹变成一个可以追踪历史修改的 repository，只需在 command line 中 `cd` 到这个文件夹，然后 `git init`. 当然，用之前，需要确保 git 已经安装。

> 在 git 中，一个文件有三种状态：modified，staged，committed。在上面建好 init 之后的文件夹中做一些修改，比如新建 README.txt，随便敲一些内容，这时候，可以用 `git status` 查看文件的状态，这时候文件应该是属于 modified 状态，需要用 `git add README.txt` 将状态转变味 staged。然后用 `git commit -m "created the README.txt"` 将文件状态转变为 committed，并用 message tag 这次修改。这时候可以用 `git log` 查看修改历史。此外，git 还有一些修改 commit 的命令，如 `git amend`, `git reset` 等，可以自行查看。

> 当然有些文件我们不想被 git 追踪，否则就会有 10w + 修改，可以将其添加到.gitignore 文件中。

> 接下来就是我们前面提到的 branch，现在我们默认是在 main branch 中，新建一个 branch `git branch name_of_the_branch`. 然后你想要跳转到这个 new branch：`git checkout name_of_the_branch`. 当然这两步可以合并为 `git checkout -b name_of_the_branch`. 在这个 new branch 中做的修改，将仅保留在这个 branch 中，当然这个修改可以 merge 到其他 branch（当然包括 main branch）中。例如使用 `git rebase the-name-of-the-branch-you-want-to-merge-from`.

上文提到的命令行对于理解 git 非常帮助，实际上，如果你使用 IDE，git 已经集成到里面了。比如 vs code，在左边的栏中有 git 的 logo，点击就可以使用。也有专门的 git 软件。![](https://mmbiz.qpic.cn/mmbiz_png/m3WnZnGIHMia4EE6j4iaaasZiblTOvLbruWn2Dr5sT9KktMFTibvwAZLqQxh7ib5yDX1ro9mVxUuWSxVuicejZJ6eNUQ/640?wx_fmt=png)

但愿上面简单的命令可以让你对 git 提起兴趣。提到 git 就不得不说 GitHub. 今天仅是我正式接触 GitHub 的第三天。所以不敢多讲。但是可以接着上面对 git 的简单介绍，再用一个简单的例子介绍两个怎么联系起来。

> 上文我们用 `git init` 将一个文件夹转换成一个 repository。当然你的工作可以直接从 GitHub 某个云端的 repository 开始。首先你需要 fork 一个 Origin repository，就是说，将这个 repository 拷贝为您个人的 repository，然后通过 `git clone some-git-code-address` copy 这个 repository 到本地。code address 可以在下图中看到。
> 
> ![](https://mmbiz.qpic.cn/mmbiz_png/m3WnZnGIHMia4EE6j4iaaasZiblTOvLbruWfr8lqjltQ7b9LgicNibQyXOfsUqiafHkSfMA4TegZmOu8r9utbB3oKBOA/640?wx_fmt=png)

> 现在 `cd` 到这个新 clone 的文件夹，就可以直接调用上文提到的 git 命令，添加新 branch，做一些修改等。
> 
> 修改完成之后，通过 `git push` 可以直接将修改同步到 GitHub。

GitHub 一个重要的操作是 **pull request**。我的理解是，当你对这个 repository 做了一些修改之后，你也想对 community 做一些贡献，所以发起一个 pull request，请求这个 repository 的实际发起人接受你的修改。这个网址可以做一个简单的小练习：https://docs.github.com/en/get-started/quickstart/contributing-to-projects

让我印象深刻的点不止是 git，实际上 git 只是开始，GitHub 只是其中的一个 block。比如给变量和函数等正确命名，使每一个函数尽量简单，所有的代码块都应该是 1-level，代码应该区分 source code （src）和 scripts，GitHub 公开等。都使我受益匪浅。感兴趣又恰好有这方面烦恼的人，可以去 GitHub 看一看 slides。
## Note