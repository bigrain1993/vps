# VPS
VPS 从零开始

<!-- vim-markdown-toc GFM -->
* [VPS是什么]

     * [1. 你肯定已经知道了要不然你搜索什么]
     * [2. 简单说的话就是一台放在别处的，永不关机的电脑]
     * [3. 维基百科VPS] https://en.wikipedia.org/wiki/VPS
        
* [购买](#重建软件环境)

    * [介绍下我用过的一些简单VPS](#开发环境恢复)
        * [1.Vultr](https://www.vultr.com)（注册送25-100美金不等）
        * [2.Linode](https://www.linode.com/)（用过一年 还可以）
        * [3.Google coloud](https://cloud.google.com/)（目前正在用 新用户免费一年，感觉是目前体验最好的）
        
    * [购买后必须要做的事情](#购买后必须做的事情)
        * [1.测试速度](#测试速度)
        * [2.查询vps的虚拟架构](#查询vps的虚拟架构)
        * [3.最重要的安全](#最重要的安全)
        * [4.有问题就重启再说](#有问题就重启再说)
  * [日常使用软件](#日常使用软件)
        * [介绍下我用过的一些简单VPS](#开发环境恢复)
        * [1.Vultr](https://www.vultr.com)
        * [2.Linode](https://www.linode.com/)
        * [3.Google coloud](https://cloud.google.com/)
       





### 购买后必须做的事情


##### 测试速度
1.网络测速
```
wget -O speedtest-cli https://raw.github.com/sivel/speedtest-cli/master/speedtest.py && chmod +x speedtest-cli && ./speedtest-cli
```
2.I/O测速 转自萌咖大佬的脚本 https://moeclub.org/2017/07/01/299/
```
bash -c "$(wget –no-check-certificate -qO- 'https://moeclub.org/attachment/LinuxShell/bench.sh')"
```
###  查询vps的虚拟架构
```
apt-get install virt-what #debian/ubuntu安装
yum install virt-what  #centos安装
virt-what  #运行
```
### 最重要的安全
一、增强VPS 账号安全方法一：修改SSH登录端口
1、用下面命令进入配置文件。
```
 vi /etc/ssh/sshd_config
```
2、找到#port 22，将前面的#去掉，然后修改端口 port 123（自己设定）。
3、然后重启ssh服务。
```
/etc/init.d/ssh restart #centos命令的命令是 /etc/init.d/sshd restart 
```
二、增强VPS 账号安全方法二：使用密钥登录SSH
1、执行以下命令在VPS上生成密钥文件。
```
ssh-keygen -t rsa #创建密钥
cd .ssh #进入密钥文件夹 使用cat查看文件或者用cp复制到桌面用putty或者MobaXterm导入key
```
三、增强VPS 账号安全方法三：禁用Root账号
1、如果你已经设置SSH密钥登录的方式，就可以禁用Root账号了，或者你可以新建一个VPS账号。执行以下命令：
useradd kristina #添加用户名
passwd 12345678 #为kristina用户名设置密码
2、然后编辑进入配置：
```vim /etc/ssh/sshd_config```
找到PermitRootLogin yes，然后后面的Yes改no，如果没有这一行命令，直接将：PermitRootLogin no 加进去。
3、保存后，重启SSH服务，生效。
```
/etc/init.d/ssh restart #centos命令的命令是 /etc/init.d/sshd restart 
```
四、增强VPS 账号安全方法四：Denyhosts防暴力攻击
1、Linux各平台现在基本上都可以直接安装Denyhosts了，执行以下命令：
```
Debian/Ubuntu：
apt-get install denyhosts
RedHat/CentOS
yum install denyhosts
```
五、增强VPS 账号小结
1、上面讲到了四个方法来增强VPS 账号的安全性，那么如何得知自己的VPS曾经或正在遭受账号暴力破解登录呢？执行以下命令，查询出来的结果中包含了“ip地址=数量”就是攻击者信息。
```
cat /var/log/secure|awk '/Failed/{print $(NF-3)}'|sort|uniq -c|awk '{print $2"="$1;}'
```
![Eudic](https://www.freehao123.com/wp-content/uploads/2013/10/vps-sh_15.gif)
### 有问题就重启再说
```
reboot
```
---------------------------------------------------------------------------------------------------------------------------------------
### 日常使用软件

### screen (转自 VPS侦探 https://www.vpser.net）
screen命令使用方法
1、常用的使用方法

用来解决文章开始我们遇到的问题，比如在安装lnmp时。

1.1 创建screen会话

可以先执行：screen -S lnmp ，screen就会创建一个名字为lnmp的会话。
1.2 暂时离开，保留screen会话中的任务或程序

当需要临时离开时（会话中的程序不会关闭，仍在运行）可以用快捷键Ctrl+a d(即按住Ctrl，依次再按a,d)

1.3 恢复screen会话

当回来时可以再执行执行：screen -r lnmp 即可恢复到离开前创建的lnmp会话的工作界面。如果忘记了，或者当时没有指定会话名，可以执行：screen -ls screen会列出当前存在的会话列表，如下图：
![Eudic](https://www.vpser.net/uploads/2010/10/screen-ls.jpg)
11791.lnmp即为刚才的screen创建的lnmp会话，目前已经暂时退出了lnmp会话，所以状态为Detached，当使用screen -r lnmp后状态就会变为Attached，11791是这个screen的会话的进程ID，恢复会话时也可以使用：screen -r 11791

1.4 关闭screen的会话

执行：exit ，会提示：[screen is terminating]，表示已经成功退出screen会话。

### python virtualenv 虚拟环境（转自狗仔小分队 http://xiaofd.win/index.php/archives/6/）
安装
```
pip install virtualenv
```
基本使用

创建虚拟环境
```
cd my_folder
virtualenv venv  # 在当前目录下新建venv目录，并安装默认版本的pyhon
virtualenv -p /usr/bin/python2.7 venv2 # 安装指定版本的python
virtualenv -p C:\Anaconda3\python.exe venv3 # 以windows为例安装pyton3环境
```
激活虚拟环境
```
# linux
source venv/bin/activate
# windows 用cmd执行(powershell执行会报错)
venv\Scripts\activate
```
离开虚拟环境
```
# linux  ## linux在venv目录下可以直接使用deactive命令退出环境
source venv/bin/deactivate
#windows 用cmd执行(powershell执行会报错)
venv\Scripts\deactivate
```
删除虚拟机
```
rmvirtualenv my_project
```
导出与恢复
```
pip freeze > requirements.txt
# pip list # 显示已安装库
pip install -r requirements.txt
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
