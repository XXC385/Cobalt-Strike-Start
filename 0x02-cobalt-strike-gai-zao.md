# 0x02 Cobalt Strike 改造



我将 Cobalt Strike 改造简单分为三个部分：优化使用体验、增加隐匿性、加固&修复安全漏洞

[![](https://camo.githubusercontent.com/af8df8936ebb8ff1fef29e2bd15772782060a495cf88ba55905de794596c4a5f/68747470733a2f2f6d65726d6169642e696e6b2f696d672f70616b6f3a654e7172566b724f54306c56736c4a4b4c306f73794644774359724a6338355053737770435334707973784f66545a6c3538754742626132646b38587a5876617465446c72416c50655f595f6131694f533158586771657a647a326431504e6b5f37716e533371667275743832727269325a372d5a31766d346444785a4d2d4d707a33546e757a645f337a4b696964374a37396331614f6b6f355362577053626d4a6b4364465631544a3643516f785353555a71626d714d6b6857516d5a4b616c6c696155784b6a464a4e5843315361574671534831795a6c36786b56564a556d71716a564671516b6c695336704b5a4350525072704a56576d4a4f63576f7441466674624367)](https://mermaid-js.github.io/mermaid-live-editor/edit#pako:eNqrVkrOT0lVslJKL0osyFDwCYrJc85PSswpCS4pysxOfTZl58uGBba2dk8XzXvateDlrAlPe\_Y\_a1iOS1XXgqezdz2d1PNk\_7qnS3qfrut82rri2Z7-Z1vm4dDxZM-Mpz3Tnuzd\_3zKiid7J79c1aOko5SbWpSbmJkCdFV1TJ6CQoxSSUZqbmqMkhWQmZKalliaUxKjFJNXC1SaWFqSH1yZl6xkVVJUmqqjVFqQkliS6pKZCPRPrpJVWmJOcWotAFftbCg)

## 0x03-1 优化使用体验

### 一. TeamSever 持久化

在我们安装完后，会发现一段时间不使用 SSH 工具会自动断开与 TeamSever 服务器的连接，导致服务端不可用，这时候使用 `screen` 工具实现TeamSever 的持久化

> **GNU Screen**是一款由GNU计划开发的用于命令行终端切换的自由软件。用户可以通过该软件同时连接多个本地或远程的命令行会话，并在其间自由切换

1. 下载 `screen` 工具，我的环境使用的是 Centos 7.6 ，所以使用 `yum install screen`

```
apt-get install screen # Debian系列：Debian、Ubuntu等
yum install screen  # RedHat系列：Redhat、Centos、Fedora等
```

1. 出现 `Is this ok [y/d/N]:` ，输入 `y` ，进行后续安装，出现**完毕**则安装成功

![image-20221006230229496](https://raw.githubusercontent.com/XXC385/img/main/image-20221006230229496.png)

📖 【知识点】y：下载安装/d：只下载不安装/n：不安装

1. 输入 `screen` ，会开启一个新的窗口

![image-20221006230311059](https://raw.githubusercontent.com/XXC385/img/main/image-20221006230311059.png)

1. 在新窗口启动 Teamserver 服务（需要切换到目标目录，如忘记方法见 **配置Teamserver** 部分）

```
cd /home/CobaltStrike # 这个是我的路径
sudo ./teamserver <ip> <password> #IP：本机IP    password：本机密码
```

![image-2022100623040307](https://raw.githubusercontent.com/XXC385/img/main/image-20221006230403071.png)

出现此回显后代表服务正常启动

1. 按下组合键 `Ctrl+A+D` 关闭窗口并后台执行，可以看到有会话为登出状态

![image-20221006230419322](https://raw.githubusercontent.com/XXC385/img/main/image-20221006230419322.png)

1. 使用 `screen –ls` 查看后台会话，也就是我们刚才挂起的服务，发现有一个

```
3107.pts-0.test1234Atest (Detached)
```

这个就是我们刚才挂起的项目，使用 **`screen –r id`** 即可回到刚才挂起的项目（每个机器 `id` 不同，根据自己的情况来，这里我的就是 3107 ）

1. 之后对我们刚才的成果进行测试，关闭 SSH 连接后发现 Teamserver 依然正常工作，如果需要关闭刚才的任务，回到 screen 页面执行 `screen -S id -X quit` 即可删除会话

![image-20221006230146511](https://raw.githubusercontent.com/XXC385/img/main/image-20221006230146511.png)
