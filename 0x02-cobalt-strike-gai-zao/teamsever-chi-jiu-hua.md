# TeamSever 持久化

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

![image-20221006230403071](https://raw.githubusercontent.com/XXC385/img/main/image-20221006230403071.png)

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
