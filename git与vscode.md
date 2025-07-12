[TOC]

# GIT



### 初始化本地Git仓库

git init

### 查看当前仓库状态

git status

### 添加所有文件到暂存区

git add .

### 添加特定文件到暂存区

git add 文件名

### 提交文件到本地Git仓库并添加注释

git commit -m "提交注释"



### 查看当前配置的远程仓库URL

git remote -v

### 连接远程仓库（可以连接多个，取名不同即可）

git remote add origin https://github.com/你的用户名/你的仓库名

### 克隆远程仓库到本地

git clone https://github.com/你的用户名/你的仓库名.git

### 修改远程仓库origin的地址（从HTTPS修改为SSH）

git remote set-url origin git@github.com:Shugify/survey.git

| 命令             | 用途                                        | 是否拉代码 | 是否创建 `.git`  |
| ---------------- | ------------------------------------------- | ---------- | ---------------- |
| `git clone`      | 克隆远程仓库（首次使用）                    | ✅ 是       | ✅ 是             |
| `git remote add` | 给已有的本地仓库添加远程地址（比如 GitHub） | ❌ 否       | ❌ 否（要求已有） |

使用SSH登录则使用URL为  git@github.com:Shugify/survey.git

尝试能不能连接github  :  `ssh -T git@github.com`

Git 需要知道是谁提交的更改，否则无法执行 `git commit`，你就必须配置用户名和邮箱：

```
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```



### 推送到远程仓库特定分支

git push -u origin 分支名

### 拉取远程仓库的更新并合并到当前分支

git pull origin 分支名

### 从远程仓库 origin 拉取最新的提交和分支信息，但不自动合并到当前分支

git fetch origin 

### 创建新分支并切换到该分支

git checkout -b 新分支名

### 切换到已存在的分支

git checkout 分支名

### 合并分支到当前分支

git merge 分支名

### 查看本地分支

git branch

### 重命名本地分支

git branch -m 原名 新名

### 删除本地分支

git branch -d 分支名

### 删除远程分支

git push origin --delete 分支名



### 回退到某个提交（但保留记录）

git revert <commit-id>

### 回退到指定的提交

git reset --hard 提交ID

| 方面             | git reset --hard <commit-id>   | git revert <commit-id>       |
| ---------------- | ------------------------------ | ---------------------------- |
| 修改历史         | **是**，回退分支指针，历史改变 | **否**，添加新提交，历史完整 |
| 工作区文件       | **重置到指定提交状态**         | **应用一个撤销补丁**         |
| 暂存区           | 同步重置                       | 不影响暂存区                 |
| 是否产生新提交   | 否                             | 是                           |
| 是否破坏公共历史 | 是，强推可能影响他人           | 否，安全                     |
| 典型用途         | 本地回退，清理提交             | 协作中撤销错误提交           |



### 撤销工作目录中的更改（即撤销本地对它的修改,没有add的）

git checkout -- 文件名

### 撤销已暂存的更改（撤销已经add但还没 commit 的修改。）

git reset HEAD 文件名

### 撤销最后一次提交（暂存区和工作区会保留）

git reset --soft HEAD^

### 修改最后一次提交的注释

git commit --amend

### 强制推送更改（当修改过历史提交时）

git push --force

git push -f origin main

### 查看当前所在的分支

git branch

### 查看提交历史

git log

### 查看远程仓库的详细信息

git remote show origin







# VScode上克隆远程仓库

[【研1基本功 别人不教的，那就我来】SSH+Git+Gitee+Vscode 学会了就是代码管理大师_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Fw4m1C7Tq/?spm_id_from=333.337.search-card.all.click&vd_source=9e5a373a45a6360ae3ba2687556fb2bc)

做好代码管理，GitHub容纳项目大小有上限，一般在1G以内

可以利用ssh公钥连接Github: 远程服务器生成公钥和私钥，公钥上传GutHub，远程服务器即可关联GitHub仓库



克隆与拉取区别在？

* 克隆, `git clone` , 从远程仓库复制一整个 Git 项目（包括代码、提交历史、分支等）到本地新目录,clone下来的仓库在执行clone的目录下
* 拉取,`git pull`, 从远程仓库拉取最新改动并合并到当前本地分支，用于已有仓库的更新同步



`--depth 10`  表示只克隆最近的10次提交

![image-20250709122823147](C:\Users\SHI\AppData\Roaming\Typora\typora-user-images\image-20250709122823147.png)



Vscode的Git Graph插件可以管理从GitHub克隆下来的分支，以及提交，感觉没有命令行直接操作好用



公司会遇到的坑：

```
git submodule update --init --recursive		#很久不用的分支，需要更新子模块
git status		#查看状态，有没有track的子模块
```



配置身份信息，设置提交作者（Author），全局设置（默认用于所有 Git 仓库

```
 git config --global user.email "you@example.com"
 git config --global user.name "Your Name"
```

![image-20250709182716712](C:\Users\SHI\AppData\Roaming\Typora\typora-user-images\image-20250709182716712.png)



创建新的分支并切换到该分支（感觉类似克隆，对分支的操作不会影响到主分支）

使用默认主分支创建新的分支

`git checkout -b  分支名(推荐用日期表示)`



在某一次提交的基础上创建新的分支

![image-20250709163130938](C:\Users\SHI\AppData\Roaming\Typora\typora-user-images\image-20250709163130938.png)

点击后再次`git checkout -b  分支名(推荐用日期表示)`就是基于某次提交的基础上创建的新分支



在VScode上对分支进行修改，修改后的代码会标绿而且在文件标注M(Modify)

![image-20250709154850245](C:\Users\SHI\AppData\Roaming\Typora\typora-user-images\image-20250709154850245.png)

![image-20250709154906447](C:\Users\SHI\AppData\Roaming\Typora\typora-user-images\image-20250709154906447.png)



VScode中源代码管理

![image-20250709154941817](C:\Users\SHI\AppData\Roaming\Typora\typora-user-images\image-20250709154941817.png)

操作分别为：打开更改文件，撤销文件更改，暂存更改的文件(可将后序更改的内容与暂存更改的做对比)

![image-20250709155107758](C:\Users\SHI\AppData\Roaming\Typora\typora-user-images\image-20250709155107758.png)

```
git add xxx.py
```



提交修改(commit+注释，建议很多的修改分次提交)

对应`git commit -m "说明"`

![image-20250709161419498](C:\Users\SHI\AppData\Roaming\Typora\typora-user-images\image-20250709161419498.png)

然后将修改push到github仓库

可以用`git push` , 或者本地新建的分支第一次上传需要用`git push --set-upstream origin 分支名`

或者直接发布branch（VScode真是个伟大的发明）

![image-20250709162445868](C:\Users\SHI\AppData\Roaming\Typora\typora-user-images\image-20250709162445868.png)



然后关于撤回

提交的分支改错了，或者同一个功能需要加新的东西（可合并），在分支的基础上增加新分支会显得杂乱，因此考虑撤回

把上一次的提交回退了（这时候远程还有这个分支吗,应该是没了？）

（多人项目时谨慎使用）

```
git reset --soft HEAD^
```



更新内容并且commit以后会出现

![image-20250709164340606](C:\Users\SHI\AppData\Roaming\Typora\typora-user-images\image-20250709164340606.png)

这时点击同步更改会报错，需要强制提交`git push -f`

然后就只有新的提交了



### 分支合并时， 三种典型情况

| 情况                     | 是否会覆盖主分支内容？ | 结果                                     |
| ------------------------ | ---------------------- | ---------------------------------------- |
| ✅ 不同文件被修改         | ❌ 不会覆盖             | 自动合并，两个文件都保留                 |
| ⚠️ 同一文件不同位置被修改 | ❌ 不会覆盖             | 自动合并，两个修改共存                   |
| ❗ 同一文件同一位置被修改 | ⚠️ 可能冲突             | **你必须手动解决冲突，决定保留哪个内容** |



origin是默认远程仓库的名字

![image-20250710000908134](C:\Users\SHI\AppData\Roaming\Typora\typora-user-images\image-20250710000908134.png)







## 问题：fatal: unable to access ' ': Failed to connect to github.com port 443 即git链接不上github 

**设置HTTP代理**

git config --global http.proxy http://127.0.0.1:我的端口号

**设置HTTPS代理**

git config --global https.proxy http://127.0.0.1:我的端口号







