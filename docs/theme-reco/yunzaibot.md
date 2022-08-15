---
title: Termux部署Yunzai-Bot教程
date: '2022-08-15 16:50:00'
sidebar: 'auto'
categories:
 - 编程
tags:
 - Termux
 - 机器人
publish: true
---
# 方法一 使用大佬的一键部署代码

这位大佬的一键部署地址：https://gitee.com/TimeRainStarSky/TRSS_Yunzai

同时还有视频演示：AV983453309

请自行查看gitee项目和视频演示内容。

# 方法二 自行手动部署

大致情况就是，一键部署指令会部署相应的环境以及云崽项目，但是指令克隆的项目是乐神的项目，而乐神的项目更新到了v3，所以现在使用一键部署指令一定部署的是v3。所以需要手动部署并且克隆喵佬那边的云崽v2项目.

这里参照了乐神专栏内的部署内容（CV15126105），以及芒果猫的手动部署内容（CV17479494）。

首先请确保自己下载的是最新版本的termux并打开，且设备非虚拟机，因为termux不支持虚拟机运行。

依次按照乐神的专栏，输入代码，这里直接搬运过来了

**注意，多段代码复制粘贴的话请检查每段代码是否都有所执行。**

安装模拟权限，git，python：

```
`pkg install proot git python -y`
```



```
pkg install proot git python -y
```

依次执行命令

```
git clone https://gitee.com/Le-niao/termux-install-linux.git
```

```
cd termux-install-linux
```

```
python termux-linux-install.py
```

（这段复制粘贴后会自动换行执行，但最后一行代码需手动回车执行）

```
git clone https://gitee.com/Le-niao/termux-install-linux.git
```

```
cd termux-install-linux
```

输入1安装Ubuntu

```
python termux-linux-install.py
```

安装Ubuntu成功

安装ubuntu成功
切换目录，启动Ubuntu

```
cd ~/Termux-Linux/Ubuntu
```

```
./start-ubuntu.sh 
```

启动Ubuntu成功
到这里已经成一半了！

apt更新一波

```
apt update 
```

（如失败，请使用apt upgrade）

```
apt update
```

安装curl

```
apt install curl -y
```

```
apt install curl -y
```

注意！

后面的下一个指令就是curl一键部署，这里就需要开始手动部署了！

还是直接搬运的芒果猫大佬指令：

```
curl -sL https://deb.nodesource.com/setup_17.x | bash  - 
```

```
apt-get install -y nodejs 
```

（这两行执行可能会自动换行导致第二行代码不执行，请检查是否有第二行代码执行的记录，第二行代码不执行将导致最后的cnpm install步骤报错）

```
curl -sL https://deb.nodesource.com/setup_17.x | bash -
```

```
apt-get install -y nodejs
```

安装redis并启动

```
apt-get install redis -y
```

```
redis-server --daemonize yes --save 900 1 --save 300 10
```

**(注意，如果同时复制这两段代码的话，可能会出现第二行的redis启动代码不执行，请参照视频内容检查是否执行)**

安装chromium

```
apt install chromium-browser -y 
```

中文字体

```
apt install -y --force-yes --no-install-recommends fonts-wqy-microhei 
```

安装git

```
apt install git -y
```

芒果猫大佬接下来的代码就是克隆云崽项目了，但是芒果猫大佬的克隆用的是乐神的项目，现在乐神已经更新到v3了，所以克隆下来的云崽项目也是v3，这里就需要克隆喵佬的项目了。

```
git clone https://gitee.com/yoimiya-kokomi/Yunzai-Bot.git
```

克隆完成就大功告成啦！

接下来就是进入云崽目录

```
cd Yunzai-Bot
```

```
npm install -g cnpm -registry=https://registry.npm.taobao.org
```

```
cnpm install
```

**(这里在我视频中是npm install，但是由于大部分人使用npm install报错，所以更改为下载cnpm，使用cnpm进行安装)**

启动云崽开始配置

```
node app
```

**QQ建议填写小号。**

登录设备建议填写自己不用的或者不常用的，比如常用电脑和安卓手机登录，那就建议填写安卓手表或者apad对应的数字。

米游社ck可先不配置，直接回车跳过即可，后续机器人成功运行后可向机器人发送“#体力帮助”指令以了解ck获取方法。

账号初次使用机器人登录，会出现“收到滑动验证码，请访问以下地址完成滑动”等提示，请复制所给链接，并下载滑动验证助手（https://maupdate.rainchan.win/txcaptcha.apk ），将链接输入滑动验证助手完成滑块验证，并复制返回的ticket，回到termux将ticket输入即可。

如果输入ticket后遇到“当前设备存在安全风险，请使用常用设备登录”，请再次输入node app启动，重复滑块验证步骤，获取ticket后粘贴，将出现“收到登录保护URL，只需一次验证即可长期生效”，请复制所给链接，转到浏览器粘贴打开，使用已经登录了小号的设备进行扫码验证即可。


退出termux后，想要启动机器人请使用如下代码，直接复制粘贴即可：

```
cd ~/Termux-Linux/Ubuntu
./start-ubuntu.sh
redis-server --daemonize yes --save 900 1 --save 300 10
cd Yunzai-Bot
node app
```

  作者：长-楠 https://www.bilibili.com/read/cv17712967 出处：bilibili