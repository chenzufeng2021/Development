# 日志

| 版本 | 内容     | 时间       |
| ---- | -------- | ---------- |
| V1.0 | 添加笔记 | 2022/05/16 |
|      |          |            |
|      |          |            |

# 配置

在 Mac 上安装 Git 有多种方式，最简单的方法是安装 Xcode Command Line Tools。 在 Terminal 里尝试首次运行 `git` 命令即可，如果没有安装过命令行开发者工具，将会提示安装：

```sh
➜  ~ git --version
git version 2.32.1 (Apple Git-133)
```

Git 自带一个 `git config` 的工具来帮助设置控制 Git 外观和行为的配置变量。 这些变量存储在三个不同的位置：

1、`/etc/gitconfig` 文件：包含系统上每一个用户及其仓库的==通用配置==。 

如果在执行 `git config` 时带上 `--system` 选项，那么它就会读写该文件中的配置变量（由于它是系统配置文件，因此需要管理员或超级用户权限来修改它）。

2、`~/.gitconfig` 或 `~/.config/git/config` 文件：只针对==当前用户==。 

可以使用 `--global` 选项让 Git 读写此文件，这会对系统上**所有**的仓库生效。

3、当前使用仓库的 Git 目录中的 `config` 文件（即 `.git/config`）：针对==该仓库==。 

可以使用 `--local` 选项让 Git 强制读写此文件，默认情况下用的就是它（需要进入某个 Git 仓库中才能让该选项生效）。

注意：

每一个级别会覆盖上一级别的配置，所以 `.git/config` 的配置变量会覆盖 `/etc/gitconfig` 中的配置变量。



可以通过以下命令查看所有的配置以及它们所在的文件：

```sh
git config --list --show-origin
file:/Library/Developer/CommandLineTools/usr/share/git-core/gitconfig   credential.helper=osxkeychain
```

## 用户信息

安装完 Git 之后，要做的第一件事就是设置你的==用户名==和==邮件地址==。 这一点很重要，因为它们会写入到你的每一次提交中：

```sh
➜  ~ git config --global user.name "chenzufeng"
➜  ~ git config --global user.email "chenzufeng@outlook.com"

➜  ~ git config --list --show-origin
file:/Library/Developer/CommandLineTools/usr/share/git-core/gitconfig   credential.helper=osxkeychain
file:/Users/chenzufeng/.gitconfig       user.name=chenzufeng
file:/Users/chenzufeng/.gitconfig       user.email=chenzufeng@outlook.com
```

## 配置验证信息

由于本地 Git 仓库和 GitHub 仓库之间的传输是通过 SSH 加密的，所以我们需要配置验证信息，以便推送本地修改。

使用以下命令生成 SSH Key ：

```sh
➜  ~ ssh-keygen -t rsa -C "chenzufeng@outlook.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/chenzufeng/.ssh/id_rsa): 
Created directory '/Users/chenzufeng/.ssh'.
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /Users/chenzufeng/.ssh/id_rsa
Your public key has been saved in /Users/chenzufeng/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:Ty+gCI8WH+NUkslaimnj0tB9donLvzrFXKoo3OhjrQ8 chenzufeng@outlook.com
The key's randomart image is:
+---[RSA 3072]----+
|                 |
|   . o           |
|    * .          |
| + = o . ..      |
|+o* = +oSo.      |
|oo.O B +=+ .     |
|.oE+=.+o  o .    |
|..*.+ o.   .     |
| oo=. .oo.       |
+----[SHA256]-----+

# 打开文件夹
➜  .ssh open . 
```

复制 d_rsa.pub 中的内容，在 Github 页面 `Account->Setting->SSH and GPG keys` 中新建 `SSH key`。

验证是否配置成功：

```sh
➜  .ssh ssh -T git@github.com                        
The authenticity of host 'github.com (140.82.114.3)' can't be established.
ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'github.com' (ED25519) to the list of known hosts.
Hi chenzufeng2021! You've successfully authenticated, but GitHub does not provide shell access.
```



# Git 基础

## 获取仓库

通常有两种获取 Git 项目仓库的方式：

1、将尚未进行版本控制的==本地目录==转换为 Git 仓库；

2、从其它服务器==克隆==一个已存在的 Git 仓库。

两种方式都会在你的本地机器上得到一个工作就绪的 Git 仓库。

### 初始化仓库

如果你有一个尚未进行版本控制的项目目录，想要用 Git 来控制它，那么==首先需要进入该项目目录中==：

```sh
➜  ~ cd /Users/chenzufeng/Documents/Development 
```

然后执行：

```sh
➜  Development git init         
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint: 
hint: 	git config --global init.defaultBranch <name>
hint: 
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint: 
hint: 	git branch -m <name>
Initialized empty Git repository in /Users/chenzufeng/Documents/Development/.git/
➜  Development git:(master) ✗ 

➜  Development git:(master) ✗ git config --global init.defaultBranch main  

➜  Development git:(master) ✗ git branch -m main                         
➜  Development git:(main) ✗ 
```

该命令将创建一个名为 `.git` 的子目录，这个子目录含有初始化的 Git 仓库中所有的必须文件。 但是，在这个时候，仅仅是做了一个==初始化==的操作，项目里的文件还没有被跟踪。

### Github 仓库

地址：

```markdown
https://github.com/chenzufeng2021/Development.git

git@github.com:chenzufeng2021/Development.git
```

create a new repository on the command line：

```sh
echo "# Development" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
# 添加一个新的远程仓库，可以指定一个简单的名字，以便将来引用
git remote add origin https://github.com/chenzufeng2021/Development.git
git push -u origin main
```

push an existing repository from the command line：

```sh
git remote add origin https://github.com/chenzufeng2021/Development.git
git branch -M main
git push -u origin main
```



# 参考资料

[^1]:[官方文档](https://git-scm.com/book/zh/v2)