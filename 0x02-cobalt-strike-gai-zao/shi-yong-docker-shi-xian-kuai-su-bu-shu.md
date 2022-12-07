# 使用 Docker 实现快速部署

我这里用的环境如下：

| Linux      | JDK | 系统内核                         | SSH 工具                |
| ---------- | --- | ---------------------------- | --------------------- |
| CentOS 7.6 | 11  | 3.10.0-1160.45.1.el7.x86\_64 | FinalShell / Xshell 7 |

**1. 安装 Docker**

清除旧版本 Docker，如果没有匹配项也是正常的

```bash
yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```

`yum install -y yum-utils` 进行 Docker 的安装

![Untitled](https://raw.githubusercontent.com/XXC385/pic-club/main/Untitled%2014.png)

设置镜像仓库，根据你的需求进行选择

```bash
# 官方源：
yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo

# 阿里云：
yum-config-manager \
    --add-repo \
    https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

如果显示 `bash: um-config-manager: 未找到命令`，使用 `yum -y install yum-utils` 安装 yum-utils 包即可

![Untitled](https://raw.githubusercontent.com/XXC385/pic-club/main/Untitled%2015.png)

安装 Docker 引擎，出现 `Is this ok [y/d/N]:` ，输入 `y`

```bash
yum makecache fast #安装之前可以先更新下yum源(可选)
sudo yum install docker-ce docker-ce-cli containerd.io docker-compose-plugin
# docker-ce：社区版
# docker-ee：企业版
```

启动 Docker

```bash
sudo systemctl start docker
```

执行 `sudo docker run hello-world` 或者 `docker version` 验证环境安装是否成功

![Untitled](https://raw.githubusercontent.com/XXC385/pic-club/main/Untitled%2016.png)

![Untitled](https://raw.githubusercontent.com/XXC385/pic-club/main/Untitled%2017.png)

卸载（非必要）

如果你想卸载 Docker，执行以下命令即可

```bash
# 卸载依赖
yum remove docker-ce docker-ce-cli containerd.io
# 删除资源  . /var/lib/docker是docker的默认工作路径
rm -rf /var/lib/docker
```

如有其他版本安装需求请根据 Docker 官方文档进行操作：https://docs.docker.com/engine/install/

**2. 编写 Dockerfile**
