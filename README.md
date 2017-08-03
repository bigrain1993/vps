
<!-- vim-markdown-toc GFM -->
* [VPS是什么]

     * [1. 不知道也不重要]
     * [2. 非要简单说的话就是一台虚拟的永不关机的电脑]
     * [3. VPS维基百科][虚拟专用服务器][1]
        
* [重建软件环境](#重建软件环境)

    * [开发环境恢复](#开发环境恢复)
        * [oh-my-zsh](#oh-my-zsh)
        * [space-vim](#space-vim)
        * [spacemacs](#spacemacs)
        * [Java 与 Python](#java-与-python)
        * [其他](#其他)
        
    * [日常使用软件](#日常使用软件)

<!-- vim-markdown-toc -->

近来由于 Mac 出了点小问题一直没有解决，加上用了已经有好长一段时间，一直想清理一下(精神洁癖作祟)，所幸重装了事。没有使用 TimeMachine，所以需要先行将一些觉得尚有价值的文件拷贝下来。

写下这篇文章，也是为了以后再次遇到问题能够有章可循，不至于胡乱一通重装。本文也会持续更新，欢迎大家分享更好的使用技巧与经验。

## 重装 macOS

在线恢复系统实在太慢，进行在 Windows 下制作 Mac U盘启动盘重装系统.  额外所需的物理设备为 U 盘一个，8G 及以上为宜。

#### 1. 准备软件与镜像

- 下载软件 TransMac
[TransMac官网下载地址](http://www.acutesystems.com/scrtm.htm)，有 15 天试用期。

- 下载镜像文件
如果身边有 Mac, 可以直接从 app store 进行下载，如果没有也可以自行搜索从网盘进行下载。这里是我使用的镜像文件: 链接: https://pan.baidu.com/s/1eRXmcMI 密码: s5u6.  版本不重要，安装成功以后更新即可。

#### 2. 制作mac的U盘启动盘

1.  将U盘接入电脑，打开 TransMac，在左侧窗口找到 U盘。

2. 将U盘格式化为 Mac 下的格式：选中U盘 >> 右键选择 `Format Disk for Mac`。以前版本的 TransMac 可能在这个时候还会出现一些选项让你进行选择，现在的最新版本已经没有了。

3. 格式化完成后，选中 U盘 >> 右键选择 `Restore with Disk Image` 选项，选择刚刚下载的 macOS 镜像文件(.dmg).

4. 时间可能会有点久，耐心等待 TransMac 将镜像文件写入U盘。大概需要20分钟。

#### 3. 使用制作好的 U盘安装 macOS

1. 将制作好的 U盘接入 Mac 并启动，按住 option 键，系统显示可用启动盘后选择 U盘并进入。

2. 选择 `Install OS X`，接下来的操作都很简单，一看就知道怎么做。

3. 耐心等待安装完成。

**注意事项!!!**

在革命即将取得胜利的时候，很可能会遇到这样的问题：

>安装 OS X Yosemite”应用程序副本不能验证，可能下载过程中有损坏之类的问题出现导致安装终止。

这个问题导致我重装两次失败，浪费了很多时间，最后在v2ex发帖有位朋友给出了知乎的链接：打开终端输入：`date 062614102014.30`, 这里是 [解决方案的知乎链接](https://www.zhihu.com/question/19812727).

## 重建软件环境

系统重装好以后就是安装软件。软件大致可分为两类，一是普通用户日常所需的一些软件，二是程序员身份所对应的开发环境。

先来恢复开发环境，因为使用的 homebrew 的 `brew cask` 可以帮助安装一些常用软件。

在恢复开发环境之前，有一些问题可能还是必须要先解决的，比如网络问题(翻墙)，不翻墙邮箱连 Gmail 等没法使用。

- Shadowsocks
我使用 shadowsocks，所以需要手动下载 ShadowsocksX 软件，然后配置完成翻墙功能。这部分就不多说了。

- chrome
我以前试过使用 brew cask 进行安装 Chrome，不过可能由于墙的原因，始终无法下载。故采用手动下载安装。能够翻墙以后，在 Chrome 安装完成后登录 Google 账号就会自动恢复你的书签，插件等等，十分方便。

- 输入法
如果要输入中文，要么在 `系统偏好设置` >> `键盘` >> `输入源` >> 左下`+`号添加`简体拼音输入源`。要么自行下载输入法，比如常用的搜狗输入法, 或者可以待会儿使用 `brew cask install sogouinput` 进行安装。

- xcode
  xcode 的 command line tool 在后续操作中用到，先安装整个 xcode 吧，有备无患， `App Store`  >> `xcode`。Xcode 动辄 4 到 5 个 G，网速不快的话这里还是挺闹心的。

  安装完成后，记得要先打开一次完成 components 的安装, 否则 homebrew 可能无法顺利安装。

- 使用习惯
  我习惯将左上触发角设置为 Launchpad, `系统偏好设置` >> `Misson Control` >> 左下`触发角` >> 左上`Launchpad` >> `好`, 同样设置左下触发角为`桌面`。

  将 F 键区设置为标准功能键， `系统偏好设置` >> `键盘` >> 选中`将F1、F2 等键用作标准功能键`。

  移除 Docker 中能够移除的所有图标，这样 Docker 中显示的就都是已经打开的应用程序。

### 开发环境恢复

首先安装 [homebrew](http://brew.sh/):

```sh
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`
```

 - `brew install`安装命令行软件

 - `brew cask install`安装GUI软件

`brew info APP` 可以查看有哪些安装选项。目前 `brew cask` 更新软件可能没那么优雅，很多 APP 会自动检测更新，也可先手动卸载再重新安装`brew cask uninstall APP && brew cask install APP`, 更多用法可自行搜索。

安装好 brew 以后，有一些软件是必备品，比如 git, wget. 我把 dotfiles 放在了 Github 上，里面维护了一个 `brew_for_new.sh` 放置 brew 的部分安装清单, 这里是我的 [dotfies](https://github.com/liuchengxu/dotfiles). 因此执行下面的命令即可安装brew必备的一些软件：

```sh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/liuchengxu/dotfiles/master/brew_for_new.sh)"`
```

顺便再将 dotfiles 克隆到本地：

```sh
git clone https://github.com/liuchengxu/dotfiles.git ~/dotfiles
sh ~/dotfiles/bootstrap.sh
```

#### [oh-my-zsh](http://ohmyz.sh/)

```sh
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

#### space-vim

我有一个 vim 配置 [space-vim](https://github.com/liuchengxu/space-vim) 放在 Github 上，执行安装命令即可一键安装。不过首先需要安装 vim:

```sh
brew install vim --with-lua --with-override-system-vi --with-python3
brew install macvim --with-lua --with-override-system-vim --with-python3
# YouCompleteMe prerequisites
brew install cmake
```

安装 powerline fonts, space-vim 与 [powerline fonts](https://github.com/powerline/fonts) 搭配效果更佳：

```sh
git clone https://github.com/powerline/fonts.git ~/.fonts && bash ~/.fonts/install.sh
```

#### [spacemacs](https://github.com/syl20bnr/spacemacs)

安装 emacs:

```sh
brew tap d12frosted/emacs-plus
brew install emacs-plus
brew linkapps emacs-plus 
```

克隆 spacemacs repo:

<pre class="language-bash">
git clone https://github.com/syl20bnr/spacemacs ~/.emacs.d
</pre>

#### Java 与 Python
`brew cask install java` 会安装最新版本的 Java. 如果需要指定版本，自行搜索具体做法即可。

`brew cask install anaconda`, 所安装的版本为 anaconda3. 如果需要 anaconda2, 需要自行从[continum.io](https://www.continuum.io/downloads#osx)下载.

非常推荐大家使用 anaconda 安装 python 环境，里面的很多工具都非常好用，比如 Jupyter Notebook. 如果下载太慢，尝试开启全局 ss.

#### 其他

```sh
# sourcetree
brew cask install sourcetree

# sublime text
brew cask install sublime-text

# iterm2
brew cask install iterm2

# r语言
brew cask install r-gui
```

使用 brew cask 的其中一个好处便是有些图形软件 brew 会自动帮你创建一个链接可以从 terminal 中启动，比如可以使用 `subl` 从命令行启动 sublime text.  

iterm2 安装完成后克隆终端主题进行美化，毕竟默认主题选择性不多，且item2，系统自带 terminal 都可以用。

在用户目录下新建一个 GitHub 目录，以后从 GitHub 克隆的 repo 都可以放到这里：

```sh
cd ~/GitHub && git clone https://github.com/mbadolato/iTerm2-Color-Schemes.git
```

为 iterm2 设置一个类似 Guake 的功能:

1. `iTterm2` >> `Profiles`, 添加一个叫做 Guake 的 profile >> `Window` >> `Style` 选择 `Fullscreen`.
2. 设置 iTerm2 的热键，`iTerm2` >> `Keys` >> `Hotkey`, 我习惯将 Hotkey 设置为 <kbd>F12</kbd>.

这样一来，只要按 <kbd>F12</kbd> 即可唤出 terminal.

![iTerm2 Fullscreen](http://upload-images.jianshu.io/upload_images/127313-0d882e9a09b82706.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![Guake Hotkey](http://upload-images.jianshu.io/upload_images/127313-e7b9597b0bcb5a4f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### 日常使用软件

使用 brew cask 安装软件时，有时不是一个安装命令就能搞定，还需要一些额外的操作。下面是一些常用软件列表:

```sh
# qq
brew cask install qq

# alfred
brew cask install alfred

# 搜狗输入法
brew cask install sogouinput

# 欧陆词典
brew cask install eudic

# macdown
brew cask install macdown

# cheatsheet
brew cask install cheatsheet

# mactex
brew cask install mactex
```

- 搜狗输入法:

  安装搜狗输入法时，brew 会有提示:

  ```
  To complete the installation of Cask sogouinput, you must also run the installer at  '/usr/local/Caskroom/sogouinput/3.7.0.1459/安装搜狗输入法.app'
  ```

  因此，我们需要在终端中执行 `open /usr/local/Caskroom/sogouinput/3.7.0.1459/安装搜狗输入法.app` 才能进一步完成安装。

  我喜欢将候选词个数设置为最大。

- 欧陆词典:

  我买了一个欧陆的注册码，因为它的很多词库很好用。另外因为词典比较常用，给它设置一个快捷键 `Ctrl + 1`，`欧陆词典` >> `偏好设置` >> `快捷键` >> `显示|隐藏《欧陆词典》窗口` >>按`Ctrl + 1`. 以后只要 `Ctrl + 1`， 就可唤出词典。我还将`翻译选中内容`的快捷键设置为`Ctrl + T `。默认的`激活 Light Peek`快捷键与 Alfred 冲突，去除。

  ![Eudic](http://upload-images.jianshu.io/upload_images/127313-ae3f953d2603cd74.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

  ![Eudic](http://upload-images.jianshu.io/upload_images/127313-ae3f953d2603cd74.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- [MenuMeters](http://member.ipmu.jp/yuji.tachikawa/MenuMetersElCapitan/)
  可以在顶部状态栏显示网速，CPU 占用等信息。
