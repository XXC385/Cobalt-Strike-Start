# 0x01 Cobalt Strike 安装指南

### 0x01-1 常用环境

| 服务端        | 服务端环境          | GUI 客户端              | SSH 工具     |
| ---------- | -------------- | -------------------- | ---------- |
| Centos 7.6 | Oracle Java 11 | Windows / Linux kali | FinalShell |

### 0x01-2 安装过程

### 一. 安装 Open JDK 环境

CS 官方建议安装 `JDK 11/1.8` ，所以这里我们用 `JDK 11` 作为例子，如果服务器开机自带 Java 环境，**建议先卸载，防止环境混乱**

1. 输入命令（**二选一即可**）

```
yum install java-11-openjdk-devel #jdk 11

yum install java-1.8.0-openjdk* -y #jdk 1.8
```

1. 如果你的系统中还装有不同版本的 JDK 的话，请使用 `alternatives --config java` 对默认运行的 Java 版本进行选择，或使用 `rpm -qa | grep java | xargs rpm -e --nodeps` 进行删除

![Untitled](https://raw.githubusercontent.com/XXC385/img/main/Untitled.png)

1. 验证 Java 环境是否成功配置，运行Java版本检查命令：

```
java -version
```

如图显示则为成功安装

![Untitled](https://raw.githubusercontent.com/XXC385/img/main/Untitled%201.png)

### 二. 配置服务端

#### 1. 资源下载

我使用的软件包是 @www.ddosi.org 上的 Cobalt Strike 4.5 + CS Agent 版本，这里同时放出原版

[Coablt strike\_4.5](https://www.ddosi.org/cobaltstrike-4-5/)

[Coablt strike\_4.5+CSAgent .zip](https://www.ddosi.org/cobaltstrike-4-5-cracked/)

部分破解版本有可能会带有木马。另外即使没有后门，CS本身也是会报毒，因为本身带很多攻击性的payload，可以通过此页面进行判断是否来自官方：

**Hash查验方法**

在 Cobalt Strike 文件夹上框输入 `powershell` 打开 powershell

![image-20221006100756657](https://raw.githubusercontent.com/XXC385/img/main/image-20221006100756657.png)

输入`Get-FileHash .\文件名`**（注意：包括后缀）**

![image-20221006100826405](https://raw.githubusercontent.com/XXC385/img/main/image-20221006100826405.png)

对比 Hash 是否相同，如不同则已经被修改，可能存在投毒风险，在线对比工具：[http://www.jsons.cn/txtdiff/](http://www.jsons.cn/txtdiff/)

**Hash 查询在线地址（更新到4.7.1）**

[https://verify.cobaltstrike.com/](https://verify.cobaltstrike.com/)

```
# Cobalt Strike 4.7.1 (September 16, 2022)
2387c9ead13876d70a332c4ce57c4c090232d346376e174c703b38cda39f3f8f	Cobalt Strike 4.7.1 Licensed (cobaltstrike.jar)

# Cobalt Strike 4.7 (August 17, 2022)
c1cda82b39fda2f77c811f42a7a55987adf37e06a522ed6f28900d77bbd4409f	Cobalt Strike 4.7 Licensed (cobaltstrike.jar) 

# Cobalt Strike 4.6.1 (May 23, 2022)
09e30bde7602cfa3358c0b1c9124079c77181c81c4ef0ef4f6789e24a3f07d5b	Cobalt Strike 4.6.1 Licensed (cobaltstrike.jar)

# Cobalt Strike 4.6 (April 12, 2022)
939aa731685ac5c2632e4790daf034110ae4aa7237a6db72c7bba219bd450727	Cobalt Strike 4.6.0 Licensed (cobaltstrike.jar)

# Distribution Packages (released with Cobalt Strike 4.6)
d1f7eb1a34e17bb945f9b6bd656eac9d7837a00b2fadbc7d4d3e2621d2123a39	Cobalt Strike MacOSX Distribution Package (cobaltstrike-dist.dmg 20220412)
f2d4a2312abc4357c19a876d335d1da41ca01e4d4c8c056890ed32c4a16055b4	Cobalt Strike Linux Distributions Package (cobaltstrike-dist.tgz 20220412)
f696215f7fdf07a6525e91f864b39afc23e4e761cbca97c6ecb6c4ae0ffa8967	Cobalt Strike Windows Distribution Package (cobaltstrike-dist.zip 20220412)

# Cobalt Strike 4.5 (December 14, 2021)
a5e980aac32d9c7af1d2326008537c66d55d7d9ccf777eb732b2a31f4f7ee523	Cobalt Strike 4.5 Licensed (cobaltstrike.jar)

# Cobalt Strike 4.4 (August 04, 2021) 
7af9c759ac78da920395debb443b9007fdf51fa66a48f0fbdaafb30b00a8a858	Cobalt Strike 4.4 Licensed (cobaltstrike.jar)

# Distribution Packages (released with Cobalt Strike 4.4)
5adf9d086a2f59be9095458f207de9e947a05696e63365a4da02acdc17caa130	Cobalt Strike MacOSX Distribution Package (20210804)
8331a77fb2f81ce969795466f8f441f02813789c24b47d0771ffdceddf8d91fe	Cobalt Strike Linux Distributions Package (20210804)
fdcc265fcf1d87bdfd0f7ea91138d7d9f8128f8ed157d427317619002aadd17d	Cobalt Strike Windows Distribution Package (20210804)

# Cobalt Strike 4.3 (March 17, 2021) [bug fixes]
c3c243e6218f7fbaaefb916943f500722644ec396cf91f31a30c777c2d559465	Cobalt Strike 4.3 Licensed (cobaltstrike.jar)

# Cobalt Strike 4.3 (March 3, 2021)
02fa5afe9e58cb633328314b279762a03894df6b54c0129e8a979afcfca83d51	Cobalt Strike 4.3 Licensed (cobaltstrike.jar)

# Cobalt Strike 4.2 (November 6, 2020)
56a53682084c46813a5157d73d7917100c9979b67e94b05c1b3244469e7ee07a	Cobalt Strike 4.2 Licensed (cobaltstrike.jar)

# Distribution Packages (released with Cobalt Strike 4.2)
f82531f3e18de0801bf18a4f65070cd927b656c3ef4b9ae8fb2c666338e65352  	Cobalt Strike Linux Distributions Package (20201106)
ad5348bc090fd47a414329a27c80c14de5bd739b58ef5aa66ab886219a27c9f6  	Cobalt Strike Windows Distribution Package (20201106)
4592a252a1b72928c87a7a38f4ec13cc929cbc3bdd8861ac51e678a55559167c  	Cobalt Strike MacOSX Distribution Package (20201106)

# Cobalt Strike 4.1 (June 25, 2020)
1f2c29099ba7de0f7f05e0ca0efb58b56ec422b65d1c64e66633fa9d8f469d4f	Cobalt Strike 4.1 Licensed (cobaltstrike.jar)

# Distribution Packages (re-released with new verify.cobaltstrike.com certificate)
b367ee44bff09254f0a8dbf229e9c4c7c8b961adcbe6d47864b493236d2f8b0a	Cobalt Strike Linux Distribution Package (20200511)
e1189afca708394c530f239c6c9604b6063f3295a0aa996354573d5cf2f1705e	Cobalt Strike Windows Distribution Package (2020511)
3eadce2f4eaa81646d0f53aa751c5456c9c4a74ab71fd51f66af9866cdafef69	Cobalt Strike MacOS X Distribution Package (20200511)

# Cobalt Strike 4.0 (February 22, 2020) [bug fixes]
10fe0fcdb6b89604da379d9d6bca37b8279f372dc235bbaf721adfd83561f2b3	Cobalt Strike 4.0 Licensed (cobaltstrike.jar)

# Cobalt Strike 4.0 (December 5, 2019)
558f61bfab60ef5e6bec15c8a6434e94249621f53e7838868cdb3206168a0937	Cobalt Strike 4.0 Licensed (cobaltstrike.jar)

# Distribution Packages (co-released with Cobalt Strike 4.0)
51d1d14239b591d5ecf30f10e21ec5f6d196e9fe939bef23bf494a626b3addc8	Cobalt Strike Linux Distribution Package (20191205)
008d5f2b1af6a5b64b80fafee16ccdd924ad2132aabe2b287e19c5181759a549	Cobalt Strike Windows Distribution Package (20191205)
34166f7f1ae1f25dc3eca047ee53bd39c844e7b602e877e4321bdeb539b92893	Cobalt Strike MacOS X Distribution Package (20191205)

# Cobalt Strike 3.14 (May 4, 2019) [bug fixes]
0e3e7ace7f6f99b9227e9e644ae0e7469e79e4fc746a8f632940e35821a74da9	Cobalt Strike 3.14 Licensed (cobaltstrike.jar)

# Cobalt Strike 3.14 (May 2, 2019)
303486b3b06ef6b1e6c8facfe3ccc4a525f2795b7f55faca591f66c70baa2bda	Cobalt Strike 3.14 MacOS X Trial Package
8d9522c69a4df90f2738498ec836f2c44632c10406f81cad1b1d992eccca62cf	Cobalt Strike 3.14 Linux Trial Package
a5c9ec241baa6a85c77460e63b9fb50b4c2ced7186a0f947b9bf0397215659ff	Cobalt Strike 3.14 Windows Trial Package
283d9074bc089841b9ef39100928ed240721c3dbce003c93f4283d71d7a3a410	Cobalt Strike 3.14 Licensed (cobaltstrike.jar)

# Cobalt Strike 3.13 (January 2, 2019)
b4f0fdbc782d1b81a8aa6176a5bfa9c1e76754b6f74a1224c79812ce7e0c2284	Cobalt Strike 3.13 MacOS X Trial Package
a28aa4aa35190a2d6d09c1c6f894bb51f86f7d4a93a60b40bf6933bb4e9245e2	Cobalt Strike 3.13 Linux Trial Package
f5865b4c05742b07f8fcd21e847a1657ec6908887a2787ffd27fe05de7b905c6	Cobalt Strike 3.13 Windows Trial Package
2c44e5426c41798dd11764cf64bf493ff81d4e77e3ed96dd6c65cf3333bdd809	Cobalt Strike 3.13 Licensed (cobaltstrike.jar)

# Cobalt Strike 3.12 (September 6, 2018)
b43fda924df85ff9f30864c1d17f6df5c3e73d28a31666e58a12f529084a6a0a	Cobalt Strike 3.12 MacOS X Trial Package
05faf192798d94a63ab6610c0c9459c4b446c4d594188abcaa3236b6d7d2593d	Cobalt Strike 3.12 Linux Trial Package
70f4d53d02a68641ed816ef97a51b091267228dd5ab22dcc5c6dc1aef233345a	Cobalt Strike 3.12 Windows Trial Package
4349e9195e083573fca38a35f7327b6d2a95538101bef9c9efdb7476d4642d8c	Cobalt Strike 3.12 Licensed (cobaltstrike.jar)

# Cobalt Strike 3.11 (May 24, 2018) [bug fixes]
468dbaa489ff86bdd173e7c6e208719d4c3cb95adc1fda0b8ceb7d81d2c89d06	Cobalt Strike 3.11 MacOS X Trial Package
a13e0819ef4609e40ba33f96a6baab43c2cccb74956a5f708b6f4426063544e6	Cobalt Strike 3.11 Linux Trial Package
848516b701aeb46f248e9a0313fa3406f3b89cd44c3232855f5668ebbe8910f5	Cobalt Strike 3.11 Windows Trial Package
d37ab96af1cc3f4a98ba63804138f644508e632f3791e3cfdde745d307bff5d9	Cobalt Strike 3.11 Licensed (cobaltstrike.jar)

# Cobalt Strike 3.11 (April 9, 2018)
d625fc6026a5b07aa9ff759879bce8497fd2e8e5cb62a5efc9f23e140e259d3e	Cobalt Strike 3.11 MacOS X Trial Package
8a5a4c8088b75d9df1df1d0ba500bcb2d56404412da6cb9288d38e032b35f344	Cobalt Strike 3.11 Linux Trial Package
05cf861725efd4ab18c2af69133a0a9c1617dd1eb2583b97b6d41bdf658a2711	Cobalt Strike 3.11 Windows Trial Package
f3e3e645141ffcd5089816f90dee24ded30386277343f3254df05c837a6068aa	Cobalt Strike 3.11 Licensed (cobaltstrike.jar)

# Cobalt Strike 3.10 (December 11, 2017)
952407771d6b193b58ed0e07ea2e2f647d916aed86e9a8cae64828bc14be5970	Cobalt Strike 3.10 MacOS X Trial Package
3147cd19146f886fd41a3add6be947f3a4581047d4a7393f01d355c732587336	Cobalt Strike 3.10 Linux Trial Package
7035a1957ca69daa96c29cc7058b32a772c769cff26e8805b12a10e9f8b1abd5	Cobalt Strike 3.10 Windows Trial Package
f6fff191e05e3e1345db600f2731fea6324b10e57023e38e712e7f648e8643eb	Cobalt Strike 3.10 Licensed (cobaltstrike.jar)

# Cobalt Strike 3.9 (September 26, 2017) [bug fix II]
3083bed43aeeb058ef8580c7bd564cbd3910c579ecb535cdc7fd0cb397fe8c05	Cobalt Strike 3.9 MacOS X Trial Package
fdd15df9dc42717a91f94ae508744f9b584d81503408b34d3c2227895d8d3400	Cobalt Strike 3.9 Linux Trial Package
d024b760768839bb71aea16eb1d3ff86e67bbacf4539bf743ce9b0cdbbbfdb42	Cobalt Strike 3.9 Windows Trial Package
20aacc907dddaa528ebfe5fa74743a5366d52dd28073ecfd05a4922fb23ada40	Cobalt Strike 3.9 Licensed (cobaltstrike.jar)

# Cobalt Strike 3.9 (September 21, 2017) [bug fix]
853b9887b4195b38d2b424c2e2dfeafad5f2b44cff3178b3d5fcdae9cecddd02	Cobalt Strike 3.9 MacOS X Trial Package
650bd8b279135091c0d77c1057cb5c543b9de356eb4c4797a48e2ee0a5dd5df0	Cobalt Strike 3.9 Linux Trial Package
0cc1f52f678bc3ae30f81c614ffb7fb051d61a7b4998c739c6ae92487696ccbd	Cobalt Strike 3.9 Windows Trial Package
a9bde8f8694f1bcd23a3ec9774fe00ba4fad6d80bbf14aadf48940a9cd20b0e5	Cobalt Strike 3.9 Licensed (cobaltstrike.jar)

# Cobalt Strike 3.9 (September 20, 2017)
be86a78be20b9efbaea50ff6b17545738ef388103f1535b14327b3f2d8081e3f	Cobalt Strike 3.9 MacOS X Trial Package
1d035cc7eab0d27cfefb61d7eed50ca175ad66af3191c70d60081838e909d92e	Cobalt Strike 3.9 Linux Trial Package
597268753a1717936136a77d668b26f62997bee8077693f65c3f7003f016209b	Cobalt Strike 3.9 Windows Trial Package
57090f6e3a5721e4d00ebc57b65bf3c8ca29809f8dd5ac0ac5b31c0ece76f02d	Cobalt Strike 3.9 Licensed (cobaltstrike.jar)

# Cobalt Strike 3.8 (May 23, 2017)
ad2ddb76ab3f4438d2553a2fa8f98384f8778e6c18e49daaca5f3fca0bbae1e2	Cobalt Strike 3.8 MacOS X Trial Package
424ad1308b630b5f000405ad36cfec4c811fc2d2a398d1bad3c182e7259a81f5	Cobalt Strike 3.8 Linux Trial Package
0931929fcdf9c066ca765899e424d6f094879c84ad6624f37fde35e903793f80	Cobalt Strike 3.8 Windows Trial Package
77ad57b1f29569773350b228d065135c8745949bd80ee7ba59f3b01c27895bfb	Cobalt Strike 3.8 Licensed (cobaltstrike.jar)

# Cobalt Strike 3.7 (March 15, 2017)
41c02ba399b3d97b6028d49a100b29f76f60e57ed245837d08b3e5c2a894073f	Cobalt Strike 3.7 MacOS X Trial Package
3b87d9ae634c74e83161f9e549e3af9000340343f9b72fa61a3454d69b9b5dfc	Cobalt Strike 3.7 Linux Trial Package
8b1722a1989ad1c0e9f8b6f99bae49789c2b9e4a8e1535e0a1556f230cd50515	Cobalt Strike 3.7 Windows Trial Package
20bebed19e0e1639c7b719d5db70c574417707063fcd669e60349a89485d392b	Cobalt Strike 3.7 Licensed (cobaltstrike.jar)
```

#### 2. **CSAgent 说明**

原项目地址：[CSAgent](https://github.com/Twi1ight/CSAgent)（由于 DMCA 删除，存储库不可用）

说明：`Cobalt Strike 4.x` 通用白嫖及汉化加载器，采用 `javaagent+javassist` 的方式动态修改 jar包，可直接加载原版 cobaltstrike.jar，理论上支持到目前为止的所有4.x版本（不包括 4.7）

1. 汉化内容更详细，非机翻，所有文字是我一句句人工翻译的，不只简单的汉化了菜单，各类错误、说明信息都有汉化，尤其是用正则表达式覆盖了各类动态生成的错误信息
2. 汉化范围更全面，之前的各类汉化版都是没有完全汉化按钮的，因为这里涉及到 Java 的一个坑，汉化后可能导致按钮功能失效，本版本对所有按钮全覆盖； 另外，针对 Beacon 终端交互内的命令及命令帮助也都有详尽的汉化说明，部分命令还加上了我个人的说明见解
3. 汉化方式更先进，并非纯粹的正则替换，针对菜单、命令、命令帮助说明的汉化利用了Cobalt Strike加载资源文件的特性，直接翻译资源文件即可，无需再做动态替换，性能更高，后续版本更新也更方便 针对界面的各类说明、标签汉化，全部写入配置文件中，后续版本只需修改这部分配置即可，无需再修改 Java 代码

使用方法（资源已内置，无需进行配置）：

1. 下载 CSAgent.zip 解压，将原版 cobaltstrike.jar 放到解压目录中，确保CSAgent.jar、resources文件夹、scripts文件夹和 cobaltstrike.jar 处于同级目录
2. 替换 cobaltstrike、teamserver、agscript、c2lint、cobaltstrike.bat 文件中的解密 Key，目前内置的key为4.4版本，各个版本的官方解密 Key：

```
4.0 1be5be52c6255c33558e8a1cb667cb06
4.1 80e32a742060b884419ba0c171c9aa76
4.2 b20d487addd4713418f2d5a3ae02a7a0
4.3 3a4425490f389aeec312bdd758ad2b99
4.4 5e98194a01c6b48fa582a6a9fcbb92d6
4.5 f38eb3d1a335b252b58bc2acde81b542
```

1. 正常使用 teamserver 和 cobaltstrike 脚本启动即可，windows 使用 cobaltstrike.bat 启动
2. 如果仅想使用破解功能，只需删除resources文件夹和scripts文件夹即可去除汉化

#### 3. 配置 TeamSever

Cobalt Strike 需要团队服务器才能使用，也就是 TeamSever ，必要的文件为 `teamserver` 与 `cobaltstrike.jar`

![Untitled](https://raw.githubusercontent.com/XXC385/img/main/Untitled%202.png)

在任意目录下创建创建一个文件夹方便管理，这里我在 /home 目录下创建了名叫 CobaltStrike 的文件夹（这里不要出现空格，如Cobalt Strike，否则后面目录切换回出现问题）

将 `teamserver` 与 `cobaltstrike.jar` 上传到你创建的文件夹下（如果使用的是 CSAgent 进行破解需要上传 `CSAgent.jar` ，否则回出现报错）

![Untitled](https://raw.githubusercontent.com/XXC385/img/main/Untitled%203.png)

将目录转到你存放文件的目录

```
cd /home/CobaltStrike  # cd /目标路径
```

之后对 teamserver 进行提权，并运行 teamserver 使服务端正常运转

```
chmod +x teamserver  #增加teamserver执行的权限
sudo ./teamserver <ip> <password> #IP：本机IP    password：本机密码
```

出现此回显则代表配置成功

![Untitled](https://raw.githubusercontent.com/XXC385/img/main/Untitled%204.png)

### 三. GUI 客户端连接服务端

双击 cobaltstrike.bat 启动客户端，填写服务端信息

![Untitled](https://raw.githubusercontent.com/XXC385/img/main/Untitled%205.png)

检查指纹是否与服务端指纹（Hash256）一致

![Untitled](https://raw.githubusercontent.com/XXC385/img/main/Untitled%206.png)

![Untitled](https://raw.githubusercontent.com/XXC385/img/main/Untitled%207.png)

检查后一致，说明服务端 & 客户端都无问题，可以正常使用

![Untitled](https://raw.githubusercontent.com/XXC385/img/main/Untitled%208.png)

### 0x01-3 荐读

Cobalt Strike 官方安装文档（4.6版，大体与4.5安装一致）：

[cobalt-strike-install.pdf](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d8d92368-4ce9-48fe-a431-d5aac09ea80f/cobalt-strike-install.pdf?X-Amz-Algorithm=AWS4-HMAC-SHA256\&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD\&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221006%2Fus-west-2%2Fs3%2Faws4\_request\&X-Amz-Date=20221006T020513Z\&X-Amz-Expires=86400\&X-Amz-Signature=13b3e899d54f0e894ae7c1f51d909c60f3f856580c34731b44784f722f5012fd\&X-Amz-SignedHeaders=host\&response-content-disposition=filename%20%3D%22cobalt-strike-install.pdf%22\&x-id=GetObject)

[cobalt-strike-install CN.pdf](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/98df9164-b693-40fa-881b-bfcd836b08be/cobalt-strike-install\_CN.pdf?X-Amz-Algorithm=AWS4-HMAC-SHA256\&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD\&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221006%2Fus-west-2%2Fs3%2Faws4\_request\&X-Amz-Date=20221006T020549Z\&X-Amz-Expires=86400\&X-Amz-Signature=3b93a01774e7f604f3a88efd6e15f3797d56c0c172c773144344c62e073d5451\&X-Amz-SignedHeaders=host\&response-content-disposition=filename%20%3D%22cobalt-strike-install%2520CN.pdf%22\&x-id=GetObject)
