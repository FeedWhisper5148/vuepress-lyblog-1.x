---
title: 关于信息课玩MC的研究
date: '2024-5-25 16:38:00'
sidebar: 'auto'
categories:
 - 信息技术
tags:
 - Minecraft
---
## 一、如何运行Minecraft？
- 首先，微机室的电脑为Windows7系统，没有*Microsoft Store*，也就无法运行*Minecraft 基岩版*，只能运行*Minecraft Java版*
- 32位操作系统最高只能运行Java8的32位版本，更高的Java版本已经不再支持32位系统，Java8最高支持的Minecraft版本为1.16
- 由于微机室没有网络，且确少.NET模块，所以不方便运行HMCL和PCL2第三方启动器，可使用HMCL启动器的生成启动脚本功能生成一个批处理脚本
- 下载Java8的32为版本，并安装，然后在*Program Files*文件夹里面找到Java文件夹并将其复制到游戏根目录里，作为Minecraft运行所需的Java环境
- 提前使用HMCL启动器下载Minecraft1.16.2版本，并在版本设置页面生成启动脚本，将它保存到游戏根目录，然后将脚本里面的绝对路径全部替换为相对路径（将*Java*改为*Java/bin/java.exe*），防止复制到其他电脑上后不可用
- 运行启动脚本，生成必要的文件，降低微机室电脑因首次启动造成的负载
- 将游戏根目录里的所有文件压缩，复制到U盘里
- 注意：使用该批处理脚本运行后会弹出一个命令提示符窗口，稍等片刻才会弹出Minecraft，且*如果关闭命令提示符窗口，Minecraft也会被关闭*，想要隐藏命令提示符窗口，可以将脚本中的*java.exe*换成*javaw.exe*
## 二、如何进行多人游戏？
- 首先，微机室虽然没有网络，但是所有设备或者部分设备连接在同一个交换机上，可以进行数据交换，因此联机是可行的
- 由于为离线登录，且Minecraft不允许同一个世界中存在两个玩家名或uuid相同的玩家（*玩家名是玩家的唯一标识，务必要记住*，而uuid只需要保证不重复即可），所以在解压完文件后，需要通过修改启动脚本的方式使不同玩家拥有不同的玩家名和uuid
- Minecraft本身就支持局域网联机，所以只需在一台电脑上创建一个新的世界再按Esc键，对局域网开放，然后其他与该电脑连接在同一个交换机上的电脑就可以在多人游戏页面找到该世界并进入
- 另外推荐使用服务器的方式进行多人游戏，因为微机室的电脑足够多，完全可以单独使用一台电脑当做服务器
- 在*Spigot服务端*官网上下载Minecraft1.16.2的服务端核心并使用以下命令运行：
```
java -Xms1G -Xmx1G -jar spigot-1.16.2.jar
```
- 同意*eula*协议，修改配置文件中的*online-mode*值改为*false*，使服务器切换到离线模式，允许离线登录的玩家进入
- 将服务端根目录所有文件压缩，复制到U盘里，然后在微机室找一台空电脑运行服务端启动脚本，等待片刻即可启动成功
- 打开该电脑的网络设置，查看网卡状态，记下其*ipv4地址*，打开Minecraft多人联机页面，点击直接连接，填入*ipv4地址*，即可进入服务器
- 在服务端的控制台上输入*op 玩家名*即可授予某玩家管理员权限，也可使用*gamerule keepInventory true*命令打开死亡不掉落
## 三、如何保存存档？
由于微机室里的电脑都有还原程序，重启电脑后系统会被还原，因此需要将服务端所有文件压缩并复制到U盘里，下次游玩只需再次运行服务端启动脚本
附：HMCL启动器生成的客户端启动脚本
```
@echo off
set APPDATA=.minecraft
set INST_NAME=1.16.2
set INST_ID=1.16.2
set INST_DIR=.minecraft\versions\1.16.2
set INST_MC_DIR=.minecraft
set INST_JAVA=Java\bin\java.exe

Java\bin\java.exe -Xmx1024m -Dfile.encoding=GB18030 -Dsun.stdout.encoding=GB18030 -Dsun.stderr.encoding=GB18030 -Djava.rmi.server.useCodebaseOnly=true -Dcom.sun.jndi.rmi.object.trustURLCodebase=false -Dcom.sun.jndi.cosnaming.object.trustURLCodebase=false -Dlog4j2.formatMsgNoLookups=true -Dlog4j.configurationFile=.minecraft\versions\1.16.2\log4j2.xml -Dminecraft.client.jar=.minecraft\versions\1.16.2\1.16.2.jar -XX:+UnlockExperimentalVMOptions -XX:+UseG1GC -XX:G1NewSizePercent=20 -XX:G1ReservePercent=20 -XX:MaxGCPauseMillis=50 -XX:G1HeapRegionSize=32m -XX:-UseAdaptiveSizePolicy -XX:-OmitStackTraceInFastThrow -XX:-DontCompileHugeMethods -Xss1m -Dfml.ignoreInvalidMinecraftCertificates=true -Dfml.ignorePatchDiscrepancies=true -XX:HeapDumpPath=MojangTricksIntelDriversForPerformance_javaw.exe_minecraft.exe.heapdump -Xss1M -Djava.library.path=.minecraft\versions\1.16.2\natives-windows-x86 -Dminecraft.launcher.brand=HMCL -Dminecraft.launcher.version=3.5.5 -cp .minecraft\libraries\com\mojang\patchy\1.3.9\patchy-1.3.9.jar;.minecraft\libraries\oshi-project\oshi-core\1.1\oshi-core-1.1.jar;.minecraft\libraries\net\java\dev\jna\jna\4.4.0\jna-4.4.0.jar;.minecraft\libraries\net\java\dev\jna\platform\3.4.0\platform-3.4.0.jar;.minecraft\libraries\com\ibm\icu\icu4j\66.1\icu4j-66.1.jar;.minecraft\libraries\com\mojang\javabridge\1.0.22\javabridge-1.0.22.jar;.minecraft\libraries\net\sf\jopt-simple\jopt-simple\5.0.3\jopt-simple-5.0.3.jar;.minecraft\libraries\io\netty\netty-all\4.1.25.Final\netty-all-4.1.25.Final.jar;.minecraft\libraries\com\google\guava\guava\21.0\guava-21.0.jar;.minecraft\libraries\org\apache\commons\commons-lang3\3.5\commons-lang3-3.5.jar;.minecraft\libraries\commons-io\commons-io\2.5\commons-io-2.5.jar;.minecraft\libraries\commons-codec\commons-codec\1.10\commons-codec-1.10.jar;.minecraft\libraries\net\java\jinput\jinput\2.0.5\jinput-2.0.5.jar;.minecraft\libraries\net\java\jutils\jutils\1.0.0\jutils-1.0.0.jar;.minecraft\libraries\com\mojang\brigadier\1.0.17\brigadier-1.0.17.jar;.minecraft\libraries\com\mojang\datafixerupper\4.0.26\datafixerupper-4.0.26.jar;.minecraft\libraries\com\google\code\gson\gson\2.8.0\gson-2.8.0.jar;.minecraft\libraries\com\mojang\authlib\1.6.25\authlib-1.6.25.jar;.minecraft\libraries\org\apache\commons\commons-compress\1.8.1\commons-compress-1.8.1.jar;.minecraft\libraries\org\apache\httpcomponents\httpclient\4.3.3\httpclient-4.3.3.jar;.minecraft\libraries\commons-logging\commons-logging\1.1.3\commons-logging-1.1.3.jar;.minecraft\libraries\org\apache\httpcomponents\httpcore\4.3.2\httpcore-4.3.2.jar;.minecraft\libraries\it\unimi\dsi\fastutil\8.2.1\fastutil-8.2.1.jar;.minecraft\libraries\org\apache\logging\log4j\log4j-api\2.8.1\log4j-api-2.8.1.jar;.minecraft\libraries\org\apache\logging\log4j\log4j-core\2.8.1\log4j-core-2.8.1.jar;.minecraft\libraries\org\lwjgl\lwjgl\3.2.2\lwjgl-3.2.2.jar;.minecraft\libraries\org\lwjgl\lwjgl-jemalloc\3.2.2\lwjgl-jemalloc-3.2.2.jar;.minecraft\libraries\org\lwjgl\lwjgl-openal\3.2.2\lwjgl-openal-3.2.2.jar;.minecraft\libraries\org\lwjgl\lwjgl-opengl\3.2.2\lwjgl-opengl-3.2.2.jar;.minecraft\libraries\org\lwjgl\lwjgl-glfw\3.2.2\lwjgl-glfw-3.2.2.jar;.minecraft\libraries\org\lwjgl\lwjgl-stb\3.2.2\lwjgl-stb-3.2.2.jar;.minecraft\libraries\org\lwjgl\lwjgl-tinyfd\3.2.2\lwjgl-tinyfd-3.2.2.jar;.minecraft\libraries\com\mojang\text2speech\1.11.3\text2speech-1.11.3.jar;.minecraft\versions\1.16.2\1.16.2.jar net.minecraft.client.main.Main --username FeedWhisper5148 --version 1.16.2 --gameDir .minecraft --assetsDir .minecraft\assets --assetIndex 1.16 --uuid ef1c7b9202813aa7bca2595999e99c16 --accessToken 94218875a861474d997da5bd9bc3bac0 --userType msa --versionType "HMCL 3.5.5" --width 854 --height 480
pause
```
以上脚本中FeedWhisper5148为用户名，可对该玩家名进行修改