<p align="center"><a href="https://github.com/thecoder-001/MineColab"><img src="https://github.com/thecoder-001/MineColab/blob/master/Logo.png" alt="Logo" height="80"/></a></p>
<h1 align="center">MineColab</h1>
<p align="center">在 Google Colab 上开我的世界服务器(JE)</p>
<a href="https://colab.research.google.com/github/thecoder-001/MineColab/blob/master/MineColab.ipynb" target="_parent"><img align="right" src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"></a>

## :hear_no_evil:  首先，什么是 Google Colab?
正如官方常见问题解答所言，Colab 是 Google Research 的一款产品。Colab 允许任何人通过浏览器编写和执行任意的 Python 代码，尤其适合机器学习、数据分析和...。从技术上讲，Colab 是一个托管的 Jupyter Notebook 服务，不需要设置就可以使用，同时提供免费访问包括 GPU 在内的计算资源。简而言之，它是一个用于学习、运行 Python 代码、机器学习或通用目的的虚拟机。
## :moneybag:  真的*免费*吗
是的，Colab *目前*可以免费使用。但在我看来，有几点是应该牢记:
1. **colab 是免费的**，但至少不应该不分皂白地利用它。人们应该重视它是一种免费提供的资源，它可能会被耗尽或者限制。
2. 如果不是很明显，就不应该在上面运行关键任务服务(比如大型和重要的服务器/数据库/Python程序)。它的资源不是有保证的，也不是无限的，使用会有一定限制。此外，Notebook 的最大运行时间为12小时，超过12小时后，应手动重新启动。
3. 如果你需要经常使用它来完成密集的任务，可以考虑购买一台VPS服务器。服务器负载的大幅增加将迫使 Google 关闭这个可以*白嫖*的服务。

最后，这只是我个人的意见，可以忽略。问问你的心什么是对的，什么是错的。此外，请尽量将其作为**偶尔**使用的资源，而不是24小时不间断地使用，以便其他人也可以利用免费资源。(不要白嫖过度....)

## :page_with_curl: 食用指南
1. 在 Colab 中打开笔记本(.ipynb).
3. 读一读笔记本，大部分是可以看明白的。按需运行。
4. 运行第一个单元格。
5. 你有三个选择. 你可以使用 Ngrok, Playit.gg 和 Cloudflare 的 Argo(Cloudflared). Ngrok 很容易安装,不需要安装任何客户端,但它往往是很不可靠的. Argo没有这样的限制，但使用比较复杂(其实还行。) Playit.gg 的实现目前还没有完善(调试日志垃圾)，但提供了方便的静态子域。
  * Ngrok:
    Change `tunnel_service` variable and follow the prompts.
  * Cloudflare argo:
    1. After running the first cell,`Your free tunnel has started! Visit it <tunnel_address>` would be logged in the notebook console.
    2. Download [Cloudflared client](https://github.com/cloudflare/cloudflared/releases/) on all the client machines.
    3. Now on your local machine, launch the binary with `./cloudflared-linux-amd64 access tcp --hostname <tunnel_address> --url 127.0.0.1:25565`
    4. Finally, connect to `127.0.0.1:25565` from your minecraft client.
  * Playit.gg:
    Change `tunnel_service` variable, ignore the debug output _(todo:fix)_ and follow the prompts.

## :zap:  它到底是如何工作的呢?
Google Colab 是一个 Ubuntu 虚拟机，它可以很容易地开启 Minecraft 服务器。下面是开服步骤:
1. 更新 APT 缓存.
2. 通过 apt-get 安装 OpenJDK-16(Java).
3. Mount Google Drive to access the minecraft folder (Drive is used here to provide persistent storage).
4. Setup Argo/ngrok/playit Tunnel (Opening a tunnel at port 25565) depending on the `tunnel_service` variable.
5. Change directory to the minecraft-server folder on google drive ("Minecraft-server" is the default, located in the root directory of my Google Drive.)
6. List/Print the file list on the screen to indicate succesful directory change.
7. Startup the Minecraft server (with optimized JVM parameters from [Aikar's guide)](https://aikar.co/2018/07/02/tuning-the-jvm-g1gc-garbage-collector-flags-for-minecraft/)

## 🐛 有BUG吗?
Report report the bug by creating a new issue and use this helpful [issue template](https://github.com/thecoder-001/MineColab/issues/new?assignees=&labels=bug&template=bug_report.md&title=%5BBUG%5D).

Or suggest a new feature using this [template](https://github.com/thecoder-001/MineColab/issues/new?assignees=&labels=enhancement&template=feature_request.md&title=%5BFeature+Request%5D).

## 👍 歪比巴卜
- If something does not work, try using a VPN like [windscribe](https://windscribe.com) before opening an issue.
- Switch between the three different tunnel providers and see which works best for you.
- Make regular backups of your world.

[![ForTheBadge built-with-love](http://ForTheBadge.com/images/badges/built-with-love.svg)](https://github.com/thecoder-001)

