# 使用 IntelliJ IDEA 构建二次开发环境

> 何为反编译？
>
> 顾名思义，反编译的的概念与编译相反，说白了就是将已编译好的程式还原到未编译的状态，目的是找出程序的源代码

首先我们先找到 IntelliJ IDEA 中的 `java-decompiler.jar` 文件，`java-decompiler.jar` 是 IntelliJ IDEA 自带的反编译插件，一般存在此目录下：

```
IntelliJ IDEA存放位置\plugins\java-decompiler.jar\lib\
```

![image-20221209094530826](https://raw.githubusercontent.com/XXC385/pic-club/main/image-20221209094530826.png)

然后将 `coablt_strike` 拷贝到进行二次开发的目录中，再新建两个目录（这里我命名为 `cs-begin`和 `cs-end` ），其中 `cs-begin`用来存放未反编译的 Cobalt Strike ， `cs-end` 用来存放反编译后的源码，因为这里我们是对原版 Cobalt Strike 进行二次开发，所以文件夹中不存放 CSAgent （Cobalt Strike 破解工具），只放入 `cobaltstrike.jar` ，再把 `java-decompiler.jar` 放在你需要反编译的jar包路径的上级目录

![image-20221209100444921](https://raw.githubusercontent.com/XXC385/pic-club/main/image-20221209100444921.png)

随后执行命令（这里我写的有点麻烦了，大家写绝对路径就可以），一开始我使用的是 JDK 15 报 `加载主类时出现 LinkageError` 错误，改为 JDK 17 后解决，如果懒得折腾 JDK 版本，可以用 `jd-gui` 或 `CFR` 这类反编译工具，这些工具通常都有独立的可执行文件，不需要使用 java 命令来运行 jar 文件

```
java -cp java-decompiler.jar org.jetbrains.java.decompiler.main.decompiler.ConsoleDecompiler -dsg=true D:\ShenTou\CobaltStrike\coablt_strike(2)\cs-begin\cobaltstrike.jar 
D:\ShenTou\CobaltStrike\coablt_strike(2)\cs-end
# java -cp java-decompiler.jar org.jetbrains.java.decompiler.main.decompiler.ConsoleDecompiler -dsg=true cs原版路径 二次开发目录
```

运行成功后，会出现这样的页面，稍等 2-3 分钟就好

![image-20221209111226218](https://raw.githubusercontent.com/XXC385/pic-club/main/image-20221209111226218.png)

之后我们在解压缩一下 `cobaltstrike.jar` 就可以获得源码了

![image-20221209111922589](https://raw.githubusercontent.com/XXC385/pic-club/main/image-20221209111922589.png)

如果成功反编译，你解压缩后的文件是 `.java` 格式

![image-20221209112038896](https://raw.githubusercontent.com/XXC385/pic-club/main/image-20221209112038896.png)

反之，如果没有成功，文件是 `.class` 格式

![image-20221209112203627](https://raw.githubusercontent.com/XXC385/pic-club/main/image-20221209112203627.png)
