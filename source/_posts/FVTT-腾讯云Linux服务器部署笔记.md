---
title: FVTT服务器搭建记录
date: 2021-2-18
updated: 2021-2-18
tags: 
- FVTT
- 服务器
categories:
- 服务器
---

#  FVTT服务器搭建记录



> 感谢文文的指导与帮助。
> 感谢FVTT中文站的帮助。

<!--more-->

## 1. 购买服务器与域名

### 购买服务器

因为阿里云最近没什么活动，而且学生机只能买一台，所以第二台服务器就选择了腾讯云。

但是腾讯云学生服务器每日限购，我早上起不来。



最后干脆一步到位，把之后的vpn一起买了，价格如下：

![](https://raw.githubusercontent.com/DF-Master/yidapicbed/main/markdown/20210218164120.png)

如果是轻量应用服务器，一年1u 2g 40G SSD 5M峰值带宽的价格应该是107。



### 修改密码

![](https://raw.githubusercontent.com/DF-Master/yidapicbed/main/markdown/20210218164156.png)


### 绑定域名

进入服务器，购买一个域名。

我买的是badapple.online,出人意料的是只要8月/首年。



给FVTT留好端口。（FVTT的默认端口是30000）

![](https://raw.githubusercontent.com/DF-Master/yidapicbed/main/markdown/20210218164310.png)

顺带记录一下公网IP，之后要用。

我的公网IP：101.32.184.129





购买后进入我的域名，此时就有显示了

![](https://raw.githubusercontent.com/DF-Master/yidapicbed/main/markdown/20210218164336.png)

需要实名认证，所以上传身份证等待认证。虽然写着需要3-5工作日，但实际上几分钟就完成了人工认证。



随后解析——一键修改

![](https://raw.githubusercontent.com/DF-Master/yidapicbed/main/markdown/20210218164401.png)

大概一段时间之后

![](https://raw.githubusercontent.com/DF-Master/yidapicbed/main/markdown/20210218164437.png)

看到此时域名变成绿色。

![](https://raw.githubusercontent.com/DF-Master/yidapicbed/main/markdown/20210218164459.png)

添加记录，记录值改成IP。

此时域名已经绑定，我们已经可以用windows terminal 或者powershell来ssh远程控制服务器了。

![](https://raw.githubusercontent.com/DF-Master/yidapicbed/main/markdown/20210218164534.png)

```shell
ssh <username>@<hostname or IP address>
```

- `username` 即为前提条件中获得的默认帐号。
- `hostname or IP address` 为您的 Linux 实例公网 IP 或自定义域名

## 2. 搭建服务器

```shell
sudo su root
```

 获得root权限



```shell
sudo apt -y install zsh git
```

安装zsh(自动补全shell)和git



```shell
git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
```

克隆 oh-my-zsh



```shell
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
ZSH_THEME="ys"
```

复制 .zshrc，修改命令提示符样式

```shell
chsh -s /bin/zsh
```

修改 shell 类型



```shell
git clone --depth=1 https://gitee.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
# 找到的链接1

git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/powerlevel10k 
# 找到的链接2
```

安装主题powerlevel10k

重启连接工具或者重启系统，检查是否安装完成
		在终端输入 echo $SHELL，若成功在返回 /bin/zsh
		打开终端，则显示与原来不同

主题文件在 `~/.zshrc` ，输入命令 `cat ~/.zshrc` 查看 ，输入命令 `vim ~/.zshrc` 编辑	

我的设置如下：

```shell
# export MANPATH="/usr/local/man:$MANPATH"
#
# # You may need to manually set your language environment
# # export LANG=en_US.UTF-8
#
# # Preferred editor for local and remote sessions
# # if []; then
# #   export EDITOR='vim'
# # else
# #   export EDITOR='mvim'
# # fi
#
# # Compilation flags
# # export ARCHFLAGS="-arch x86_64"
#
# # Set personal aliases, overriding those provided by oh-my-zsh libs,
# # plugins, and themes. Aliases can be placed here, though oh-my-zsh
# # users are encouraged to define aliases within the ZSH_CUSTOM folder.
# # For a full list of active aliases, run `alias`.
# #
# # Example aliases
# # alias zshconfig="mate ~/.zshrc"
# # alias ohmyzsh="mate ~/.oh-my-zsh"
#
# # To customize prompt, run `p10k configure` or edit ~/.p10k.zsh.
[] || source ~/.p10k.zsh
alias ll="ls -lha"
```

重启服务器，会弹出powerlevel10k的一堆问题，完成问题后配置更改成功，我的界面如下：

![](https://raw.githubusercontent.com/DF-Master/yidapicbed/main/markdown/20210218164627.png)



## 3. 安装FVTT

提前在windows上装好winscp，连接到服务器上。

发现腾讯云无法直接用winscp访问root文件夹，用以下链接的办法解决：

https://blog.csdn.net/LoveDou0816/article/details/79886433

把本地的foundryvtt(Linux版本)和data(如果有的话)用winscp上传到服务器的root文件夹根目录下。

安装npm,用npm安装fvtt运行所需的forever:

```shell
apt-get install npm
npm install forever -g
```

安装解压缩软件，解压缩FVTT：

```shell
 apt-get install unzip
 apt-get install install p7zip-full
 unzip foundryvtt.zip -d $HOME/foundryvtt
```

然后根据fvtt官网操作：

```shell
	sudo apt install -y libssl-dev
	curl -sL https://deb.nodesource.com/setup_14.x | sudo bash -
	sudo apt install -y nodejs
	#ubuntu安装Nodejs
	
	
	cd $HOME
	mkdir foundryvtt
	mkdir foundrydata
	
	# Install the software
	cd foundryvtt
	wget -O foundryvtt.zip "<foundry-website-download-url>"
	unzip foundryvtt.zip
	#这一步不需要进行，已经安装完毕
	
	
	# Start running the server
	node resources/app/main.js --dataPath=$HOME/foundrydata
	
```

最后一步Nodejs报错不管她，进入foundrydata，看到已经出现了config等文件夹，说明已经安装完成。如果本地有data压缩包的话可以copy过去解压缩。最后启动fvtt。



```shell
forever start -a  /root/foundryvtt/resources/app/main.js --dataPath=/root/foundrydata
```

