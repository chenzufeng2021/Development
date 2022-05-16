# 安装 oh-my-zsh

**Oh My Zsh** 是基于 **zsh** 命令行的一个扩展工具集，提供了丰富的扩展功能。

## Zsh 是什么

Zsh 是一款强大的虚拟终端，既是一个系统的虚拟终端，也可以作为一个脚本语言的交互解析器。

```sh
# 查看系统当前 shell
chenzufeng@MacBookPro ~ % cat /etc/shells
# List of acceptable shells for chpass(1).
# Ftpd will not allow users to connect who are not using
# one of these shells.

/bin/bash
/bin/csh
/bin/dash
/bin/ksh
/bin/sh
/bin/tcsh
/bin/zsh

chenzufeng@MacBookPro ~ % zsh --version
zsh 5.8 (x86_64-apple-darwin21.0)
```

## 安装

可以通过 curl 或 wget 两种方式来安装：

```sh
# Gitee镜像
sh -c "$(curl -fsSL https://gitee.com/mirrors/oh-my-zsh/raw/master/tools/install.sh)"
```

输入后会显示：`“git”命令需要使用命令行开发者工具`，即，需要先安装`Command Line Developer Tools`。

安装结果：

```sh
/Users/chenzufeng

Looking for an existing zsh config...
Using the Oh My Zsh template file and adding it to ~/.zshrc.

         __                                     __   
  ____  / /_     ____ ___  __  __   ____  _____/ /_  
 / __ \/ __ \   / __ `__ \/ / / /  /_  / / ___/ __ \ 
/ /_/ / / / /  / / / / / / /_/ /    / /_(__  ) / / / 
\____/_/ /_/  /_/ /_/ /_/\__, /    /___/____/_/ /_/  
                        /____/                       ....is now installed!


Before you scream Oh My Zsh! look over the `.zshrc` file to select plugins, themes, and options.
```

zsh 的配置文件是`~/.zshrc`，位置在用户家目录下，为隐藏文件。

```sh
➜  ~ pwd
/Users/chenzufeng
# 打开配置文件
➜  ~ open ~/.zshrc
```



## 安装主题

*The default that Robby Russell uses.*

```sh
# If you come from bash you might have to change your $PATH.
# export PATH=$HOME/bin:/usr/local/bin:$PATH

# Path to your oh-my-zsh installation.
export ZSH="$HOME/.oh-my-zsh"

# Set name of the theme to load --- if set to "random", it will
# load a random theme each time oh-my-zsh is loaded, in which case,
# to know which specific one was loaded, run: echo $RANDOM_THEME
# See https://github.com/ohmyzsh/ohmyzsh/wiki/Themes
ZSH_THEME="robbyrussell"
```

## 安装插件

```markdown
# Which plugins would you like to load?
# Standard plugins can be found in $ZSH/plugins/
# Custom plugins may be added to $ZSH_CUSTOM/plugins/
# Example format: plugins=(rails git textmate ruby lighthouse)
# Add wisely, as too many plugins slow down shell startup.
plugins=(git)
```

### zsh-syntax-highlighting

高亮语法：输入正确语法会显示绿色，错误的会显示红色。

1、安装插件到`/Users/chenzufeng/.oh-my-zsh/custom/plugins`

```sh
➜  plugins git:(master) git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

➜  plugins git:(master) ls
example                 zsh-syntax-highlighting
```

2、在 `~/.zshrc` 中配置

```markdown
plugins=(xxx zsh-syntax-highlighting)
```

3、更新配置

```sh
source ~/.zshrc
```

### zsh-autosuggestions

自动补全：只需输入部分命令即可根据之前输入过的命令提示，按右键`→`即可补全。

1、下载

```sh
➜  ~ git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
Cloning into '/Users/chenzufeng/.oh-my-zsh/custom/plugins/zsh-autosuggestions'...
```

2、在 `~/.zshrc` 中配置

```markdown
plugins=(xxx zsh-autosuggestions)
```

3、更新配置

```sh
source ~/.zshrc
```

### z

目录自动跳转命令，会==记忆你曾经进入过的目录==，用模糊匹配快速进入你想要的目录。

安装方法: 直接在 `.zshrc` 中的插件那行添加 `z`。

### extract

用于解压任何压缩文件，不必根据压缩文件的后缀名来记忆压缩软件。

安装方法: 直接在 `.zshrc` 中的插件那行添加 `extract`。

使用 `x` 命令即可解压文件。

# Java 安装

1、下载[Zulu JDK 8](https://www.azul.com/downloads/?version=java-8-lts&os=macos&architecture=arm-64-bit&package=jdk)

2、安装并验证

```sh
chenzufeng@MacBookPro ~ % java -version
openjdk version "1.8.0_332"
OpenJDK Runtime Environment (Zulu 8.62.0.19-CA-macos-aarch64) (build 1.8.0_332-b09)
OpenJDK 64-Bit Server VM (Zulu 8.62.0.19-CA-macos-aarch64) (build 25.332-b09, mixed mode)
```

3、查看 Java 安装地址

```sh
chenzufeng@MacBookPro / % /usr/libexec/java_home -V
Matching Java Virtual Machines (1):
    1.8.0_332 (arm64) "Azul Systems, Inc." - "Zulu 8.62.0.19" /Library/Java/JavaVirtualMachines/zulu-8.jdk/Contents/Home
/Library/Java/JavaVirtualMachines/zulu-8.jdk/Contents/Home
```

4、配置环境变量（可选）

```sh
open ~/.zshrc
# 在末尾添加
export JAVA_HOME=/Library/Java/JavaVirtualMachines/zulu-8.jdk/Contents/Home
```

刷新：

```sh
source ~/.zshrc
```



# 安装 IDEA

参考资料：https://vccv.cc/article/jetbrains-activate.html

1、下载[ja-netfilter.zip](https://yuesir.lanzoum.com/iNlyJ03cykid)；

2、打开访达，点击左侧的 **应用程序** 找到 **IDEA** ，在 **IDEA** 图标上右键，点击 **显示包内容**；

3、进入 **Contents/bin** 目录，使用文本编辑器打开 **IDEA.vmoptions** 文件：

```markdown
# 添加的是绝对路径
-javaagent:/Users/chenzufeng/Downloads/ja-netfilter/ja-netfilter.jar
```

4、打开 IDEA，选择**选择** **License Server **方式（许可证服务器），输入服务器地址：https://jetbra.in，然后激活即可。

## 插件

1、Alibaba Java Coding Guidelines；

2、Rainbow Brackets；

3、Key Promoter X：快捷键提示；

4、Restful Fast Request；

5、Free MyBatis Tool：生成 mapper xml 文件、快速从代码跳转到 mapper 及从 mapper 返回代码、mybatis 自动补全及语法错误提示；

6、Codota：代码提示；

7、jclasslib bytecode viewer：可视化的字节码查看；

8、Maven Helper：Maven 依赖检查；

9、Java Stream Debugger：将 Stream 的操作步骤可视化。

## 设置注释模版

参考链接：https://www.jianshu.com/p/dab337159b83

### 配置类注释模板

`settings`->`Editor`->`File and Code Templates`->`files`->`class`

添加注释模版：

```java
#if (${PACKAGE_NAME} && ${PACKAGE_NAME} != "")package ${PACKAGE_NAME};#end
#parse("File Header.java")
/**
 * ${description}
 * @author ${USER}
 * @date ${DATE}
 */
public class ${NAME} {
}
```





# 安装 Maven

## 下载

下载地址：https://maven.apache.org/download.cgi

下载至：`/Users/chenzufeng/Applications`并解压：

```sh
➜  Applications extract apache-maven-3.8.5-bin.tar.gz
```

## 配置环境变量

```sh
open ~/.zshrc
```

添加路径：

```markdown
export MAVEN_HOME=/Users/chenzufeng/Applications/apache-maven-3.8.5
export PATH=$PATH:$MAVEN_HOME/bin
```

刷新：

```sh
source ~/.zshrc
```

验证：

```sh
➜  ~ mvn --version
Apache Maven 3.8.5 (3599d3414f046de2324203b78ddcf9b5e4388aa0)
Maven home: /Users/chenzufeng/Applications/apache-maven-3.8.5
Java version: 1.8.0_332, vendor: Azul Systems, Inc., runtime: /Library/Java/JavaVirtualMachines/zulu-8.jdk/Contents/Home/jre
Default locale: zh_CN, platform encoding: UTF-8
OS name: "mac os x", version: "12.3.1", arch: "aarch64", family: "mac"
```

## 配置镜像

```sh
➜  conf open settings.xml 
```

设置镜像地址：

```xml
 <!-- localRepository
   | The path to the local repository maven will use to store artifacts.
   |
   | Default: ${user.home}/.m2/repository
  <localRepository>/path/to/local/repo</localRepository>
  -->

<mirror>
    <id>aliyunmaven</id>
    <mirrorOf>*</mirrorOf>
    <name>阿里云公共仓库</name>
    <url>https://maven.aliyun.com/repository/public</url>
</mirror>
```







