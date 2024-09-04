# 写在前面
这个文档是简单介绍一下如何使用Github，学院并不会有人主动教你如何使用Github，上网检索起来也会比较繁琐。但是在学习过程中，你会发现Github是一个非常好用的工具。这个文档会帮助你快速上手Github。
# 关于注册
貌似现在只需要校园网就能注册，暂时不需要VPN。记得准备两个邮箱，一般就一个是QQ邮箱，另一个是校园邮箱。验证校园邮箱可以领取免费的Github Copilot等一些学生福利。这一部分就不过多赘述了。一些简单的信息检索还是需要锻炼的。
# 关于使用Github仓库
一般来说，会下载大佬的开源项目并且在本地成功跑起来已经非常棒了！当你能够成功按照你的需求检索项目，缝合一些小项目，在一些计算机课程取得A的绩点就会变得轻松简单。

那么如何新建一个自己的仓库，并且进行版本管理发扬互联网的开源精神呢？详见下文，也可以参考官方文档[使用SSH链接仓库](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/about-ssh)。
## 需要准备的工具
1. Git
2. 本地的一个项目（只要是一个文件夹就行）
3. Github账号名下的一个仓库-Repository
4. 本地ssh密钥

### Git
Git是一个分布式版本控制系统，可以帮助你更好的管理你的代码。在这里我们只需要Git的命令行工具，不需要安装Git GUI。Git的安装可以参考[Git官网](https://git-scm.com/)。

安装好git之后，记得设置你的用户名和邮箱，这些信息会包含在每次提交中，以便识别提交者：
```shell
git config --global user.name "你的用户名"
git config --global user.email "你的邮箱"
```
### 本地的一个项目
初始化本地Git仓库：打开终端，导航到你的项目文件夹。
输入以下命令初始化Git仓库：
```shell
git init
```
将项目文件添加到Git仓库：输入以下命令将所有文件添加到Git仓库：
```shell
git add .
```
输入以下命令提交更改：
```shell
git commit -m "Initial commit"
```
### Github账号名下的一个仓库-Repository
这个建立起来非常简单。

登录GitHub，点击右上角的“+”图标，然后选择“New repository”。
输入仓库名称和描述，选择仓库的可见性（Public或Private），这里我们一般建立空仓库，也就是上什么都需要勾选，然后点击“Create repository”。这个页面我们称为GitHub仓库页面，应该就会有几行命令行提示你如何使用http或者shh链接本地仓库，我们这里选择shh链接仓库，后续将本地仓库连接到GitHub仓库会用到。

回到Github主页，点击个人信息设置，找到SSH and GPG keys，点击New SSH key，将你的本地ssh密钥复制进去，点击Add SSH key。本地SSH密钥的在哪里呢？详见下文。

### 本地ssh密钥
安装好Git之后，我们需要生成一个ssh密钥，这样我们就可以在本地和Github之间建立一个安全的连接。在你的项目目录下打开cmd，在命令行中输入以下命令：
```shell
ssh-keygen -t rsa -b 4096 -C "你的github注册邮箱"
```
按提示操作，生成的密钥对会保存在~/.ssh目录下。

使用以下命令查看本地的密钥存放路径：
```shell
ls ~/.ssh
```
使用记事本或者VSCode打开路径中的id_rsa.pub这个文件，复制内容。粘贴到Github的SSH key中。

使用以下命令测试是否连接成功：
```shell
ssh -T git@github.com
```
如果出现Hi xxx! You've successfully authenticated, but GitHub does not provide shell access.这样的提示，说明连接成功。
### 将本地仓库连接到GitHub仓库
在GitHub仓库页面上，复制仓库的HTTPS或SSH URL。在终端中，输入以下命令将本地仓库连接到GitHub仓库：
```shell
git remote add origin <your-repository-URL>
```
或者直接复制GitHub给出的SSH连接提示命令行，格式同上。

输入以下命令将本地仓库推送到GitHub：
```shell
git push -u origin main
```
这样你的本地仓库就和GitHub仓库连接起来了。

### 如果你使用的是VSCode
在VSCode中，你可以直接使用Git的功能，不需要在终端中输入命令。在VSCode中，打开你的项目文件夹，点击左侧的源代码管理，然后点击初始化仓库，然后点击推送到远程仓库，输入GitHub仓库的URL，然后点击推送。这样你的本地仓库就和GitHub仓库连接起来了。

但是需要记得，每次提交需要添加消息，否则由于VSCode的bug会一直卡着提交的进度条。