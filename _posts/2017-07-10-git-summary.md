---
layout: post
title: 完整版git使用总结
author: Wplay
---

完整版git使用总结. 
<!-- wplay -->

全程参考廖雪峰的[git教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
## 安装git
-----
- 下载git [git-window-x64](https://git-scm.com/download/win)
- 除了安装路径更换，其他的都建议一路默认

## 预设置git
- 全局配置一下个人信息
	+ `git config --global user.name 'wplay'` *姓名随意填*
	+ `git config --global user.email 'yingxionguc@163.com'` *邮箱随意填*
- 创建密钥对
	+ `ssh-keygen -t rsa -C '838523799@qq.com'` *邮箱随意填*
	+ 三个选项，分别是`设置ssh保存路径`，`设定密码`，`确认密码`，一路enter就好
	+ 打开`C/User/Administer/.ssh/`, 记事本打开`id_rsa.pub`, 复制秘钥
	+ 粘贴秘钥到gitHub/gitLab
	
		> 打开`github > settings > SSH and GPG keys > new SSH key`, 粘贴
		> 打开`gitLab > settings > SSH keys`，粘贴，`Add key`

- *PS:* 如果你当前笔记本有两个github或者是两个gitLab账号（`是吗？今天bug太多，忘记是不是这个原因了，有待商榷？`），那么你需要设置多个秘钥，详细方法在底部`git补充`中 


## 链接一个远程仓库
-----
- 方式一: `git clone`
	+ copy你想要获取到的仓库的网址
	+ 在指定的文件夹下打开`git bash`, `git clone [url]` (url代表你复制的网址)

- 方式二: `git init`
	+ gitLab或者gitHub上找到你想要的远程仓库，获取仓库的ssh网址(和url不同)
	+ 在磁盘指定的文件夹下打开`git bash`, 开始下面的指令
		* `git init`
		* `git remote add origin [ssh-url]`(你复制的ssh网址)

## 开始开发
-----
### 标准流程
- `git pull origin master`

	> 'pull'指拉取，指令表示拉取服务器的最新版本库

- 撰写代码
- `git add .` 

	> `add`指将指定文件放入缓存区
	> `.`代表全部，如果想要指定的文件，就把`.`换成`文件名/文件夹名`（文件夹是这样上传的吧）

- `git commit -m 'add a readme'`

	> `commit`表示将缓存区的文件放在本地版本库HEAD
	> `-m '说明'`这个是本次修改文件的注释，不能少！

- `git push origin master`

	> `push`和`pull`相反，表示提交到远程仓库

- `git status`

	> 查看当前git仓库状态，建议上面的后三步骤，每一步骤之后都查看一次`git status`，防止出现问题
	
- `git diff`

	> 查看被修改文件的具体改动内容*git bash中绿字显示*



### 版本回撤(*特指本地版本库的回撤*)
- `git log`
	
	> 显示最近三次的提交详情（及其版本号id）

- `git reflog`

	> 查看所有的版本号及其简略信息

- `git reset --hard [version]` `git reset --hard HEAD~10` `git reset --hard ` 
	
	> 这里的`[version]`有三种写法
	> 	- `HEAD^^` 回撤两个版本以前，`HEAD`指当前版本，一个`^`代表一个版本回撤
	> 	- `HEAD~10` 回撤到10个版本以前
	> 	- `version` 填写你的版本号，可通过`git log`获取（**版本号不必写完整，前六七位就行**）

### 冲突解决

> 当你进行`git push origin master`，如果有人比你先提交了代码，就会出现冲突
> 此时`git status`，看看里面说了哪些文件 `both modified` ,然后逐个文件去修改
> 打开具体冲突文件，
>	```
>	<<<<<<
>	wplay's code
>	=============
>	2dog's code
>	>>>>>>
>	```
>	然后我们斟酌一下二狗的代码和我们的代码，修改一下，修改好了，把`<<<` `===` `>>>`删掉即可

### 分支
> `master`是默认分支，可以叫`主线`
> 如果我们想要对代码进行自己的DIY，但是又害怕影响到本身项目，那么，创建分支进行各种折腾是一个很好地选择

- `git branch`
	+ 查看当前仓库的所有分支，颜色不同的那个代表当前正在使用的分支
- `git checkout -b <branch name>` <==> `git branch <branch name>` + `git checkout <branch name>`
	+ `git checkout -b <branch name>`表示创建分支branch并且切换到新建的分支
	+ `git branch <branch name>` 创建新的分支，如果name重复，会有错误提示的
	+ `git checkout <branch name>` 切换到指定分支
	+ **切换分支前必须把当前分支必须将当前分支的内容add， commit**

- `git merge [branch name]`
	+ 将指定分支合并到当前分支上。
		* 如果有冲突，自行处理咯
		* 合并前，当前分支需要已经commit
- `git branch -d <branch name>` 
	+ 如果报错说the branch is not fully merged
	+ 就使用`git branch -D <branch name>`
	+ 不能删除当前选中的分支

## git补充
-----

### 设置多个ssh[参考资料](http://blog.csdn.net/chaoyue0071/article/details/41824339)
> 对于两个gitLab账号，我们如何配置两个ssh分别针对不同的gitLab呢？

- 随便哪里打开`git bash`
- 创建密钥对，`ssh-keygen -t rsa -C 'yingxionguc@163.om'`
- 这时候让你设置名称，这里不要使用默认的，而是输入`/C/User/Bill/.ssh/id_rsa_work`(名字自定义啊，我起名为`id_rsa_work`)
- 创建`config`
	- 手动创建一个`config`文件（全名就叫config，没有后缀）,记事本打开
	- 使用vi创建 `以管理员身份打开git bash` `vi .ssh/config`，然后输入内容，再`wq!`**退出vim状态**即可
- config里面的内容如下
```
# 加上以下内容
#default github
Host github_default
  HostName gitLab.com
  IdentityFile ~/.ssh/id_rsa
					`不要粘贴我：上面的可有可无，毕竟默认id_rsa，下面这个必须有`
Host gitLab_work  `这个是名称，随意起名啦`
  HostName 192.168.x.xx  `这个是url`
  IdentityFile ~/.ssh/id_rsa_work  `这个是指定秘钥文件`
```


### 退出vim状态
- vim是Unix及类Unix系统文本编辑器
- git bash自带的编辑器功能使用的就是vim
- 但是呢，我们基本不会或者不想要在git bash进入vim编辑模式
- 普通的ctrl+c无法退出的话，就是进入了vim编辑模式
- 退出方法：
	+ `ESC`退出编辑模式（相反，`Insert`进入编辑模式）
	+ `shift + ;`（可以在底部输入指令）
	+ `q!`（不保存退出）或者`wq!`(保存并退出)

### git修改远程仓库的方法
> 两种方式

	- `git remote -v` 查看远程仓库的url
	- `git remote set-url origin [new-url]` 直接设置
	- `git remote rm origin` + `git remote add origin [new-url]` 先删除原本的origin，再添加新的origin
