# 1 关于git
Git是一个开源的分布式版本控制系统，可以有效、高速地处理从很小到非常大的项目版本管理。  
分布式相比于集中式的最大区别在于开发者可以提交到本地，每个开发者通过克隆（git clone），在本地机器上拷贝一个完整的Git仓库。

# 2 git的本地库与远程库的交互方式
## 2.1 团队内协作
![QQ截图20200903091513.png](https://i.loli.net/2020/09/03/i3Gm9hfDlJLjty6.png)
## 2.2 跨团队协作
![QQ截图20200903091757.png](https://i.loli.net/2020/09/03/Izxrw59mSgKXAh1.png)

# 3 git的本地结构
![QQ截图20200903090847.png](https://i.loli.net/2020/09/03/GzhdupALkqOZ3fQ.png)

# 4 git的命令行操作
## 4.1本地库操作
### 4.1.1本地库初始化
- 命令：git init
- 效果  
![QQ截图20200903094146.png](https://i.loli.net/2020/09/03/qKvPt7c4Ys9Mgkd.png)
- 注意：.git目录存放的是本地库相关的子目录和文件，不要删除或着随便修改.

### 4.1.2设置签名
- 签名的作用：区分不同开发人员的身份  
- 签名的形式：由用户名和email组成(这里的用户名和邮箱仅仅起到区分作用)
- 注意：签名和登录远程库(比如：github)的账号密码一点关系都没有。
- 命令：
1. 项目(仓库)级别:仅在当前本地库范围内有效  
`git config user.name zyk`  
`git config user.email yongkangzhang123@foxmail.com`  
信息保存位置:./.git/config  
![QQ截图20200903135658.png](https://i.loli.net/2020/09/03/6LFlsAChmrJSevt.png)
2. 系统用户级别:登录当前操作系统的用户范围  
`git config --global user.name zyk`  
`git config --global user.email yongkangzhang123@foxmail.com`
信息保存位置:~/.gitconfig(~代表用户家目录)  
![QQ截图20200903140009.png](https://i.loli.net/2020/09/03/dcqnNZsDaUvBHR7.png)
- 级别优先级：如果项目签名和系统用户签名都存在那么，项目签名生效。

### 4.1.3状态查看操作
- 命令：git status
- 作用：查看工作区，暂存区的状态  
![QQ截图20200903140653.png](https://i.loli.net/2020/09/03/MobxCSfqlyL4F3J.png)

### 4.1.4添加操作
- 命令：git add [file name]
- 作用：将工作区的新建和修改添加到暂存区  
![QQ截图20200903141225.png](https://i.loli.net/2020/09/03/tLF6sIjCMx2J3WG.png)

### 4.1.5提交操作
- 命令：git commit (-m "commit message") [file name]
- 作用：将暂存区的内容提交到本地库  
![QQ截图20200903141917.png](https://i.loli.net/2020/09/03/V6YCXbjrwfdyI4l.png)

### 4.1.6 查看历史记录
- 命令1：git log
- 作用：完整显示提交的历史信息  
![QQ截图20200907181300.png](https://i.loli.net/2020/09/07/bTViXyWFjSnNO37.png)
- 注意：多屏显示控制方式：空格翻页，b向上翻页，q退出  
- 命令2：git log --pretty=oneline
- 作用：简洁显示提交信息。  
![QQ截图20200907183436.png](https://i.loli.net/2020/09/07/XDHPy7C4FVjgZhf.png)

- 命令3：git log --oneline
- 作用：简洁显示提交信息(相比上面的缩短了hash值)  
![QQ截图20200907183855.png](https://i.loli.net/2020/09/07/kyXfRmvgEI5DW4A.png)

- 命令4：git reflog
- 作用：相比oneline增加了到每个提交需要几步  
![QQ截图20200907192537.png](https://i.loli.net/2020/09/07/sQrNq5AkpyTbLEf.png)
- 注意：HEAD@{移动到最新版本需要的步数}

### 4.1.7 版本的前进后退
- 本质：移动HEAD指针进行更新版本
- 命令1：git reset --hard [索引值的一部分(git reflog可以获得)]
- 作用：回退到对应索引值的版本
![QQ截图20200909142732.png](https://i.loli.net/2020/09/09/mUtZf4J8c1BD79F.png)
- 命令2：git reset --hard HEAD^
- 作用：有多少^就回退几个版本，只能后退版本，不能前进，且在最初的版本不能使用该命令。  
![QQ截图20200909150102.png](https://i.loli.net/2020/09/09/UsPNzYdHW76ZtXV.png)
- 命令3：git reset --hard HEAD~n
- 作用：和上面的类似，只能回退，不能前进，n是几就回退几次。  
![QQ截图20200909151048.png](https://i.loli.net/2020/09/09/hZCcmwarlt1OLMd.png)
- 注意：git reset --option <commitid>是回滚命令，option有三个参数可选：
1. git reset --mixed，这也是默认方式（即不带参数默认是这种），回退暂存区和版本库信息，工作区的源码不会变化，可以重新add，重新commit。
2. git reset --soft，回退版本库信息，暂存区和工作区都不会变化，如果还要提交，直接commit即可。
3. git reset --hard，彻底回退，3个区都回退到历史某个版本。

### 4.1.8 比较文件差异
- 命令：git diff [历史索引] [文件名]
- 作用：比较工作区的文件和暂存区与本地库的版本有什么区别
- 注意：如果不加历史索引(如HEAD表示当前本地库的版本，HEAD^表示当前本地库的前一个版本)，则与暂存区进行比较，否则与对应的历史索引的版本进行比较。如果不加具体文件名，则显示所有文件的比较结果。
![QQ截图20200909162702.png](https://i.loli.net/2020/09/09/XeGoAISRswKDgLY.png)
![QQ截图20200909162753.png](https://i.loli.net/2020/09/09/7xvVWYgwzHSEaNA.png)
![QQ截图20200909163346.png](https://i.loli.net/2020/09/09/8WUPQ6YbMymczLF.png)

## 4.2 分支操作
> 1. **什么是分支?**  
在版本控制过程中，使用多条线同时推进多个任务
![QQ截图20200909201916.png](https://i.loli.net/2020/09/09/iOXgepJfTGocF7A.png)
hot_fix：临时分支，专门用来修复Bug，修复完之后会合并到主干上  
master：主干  
feature_blue、feature_game：从主干复制出来的其它分支，可以与主干同时开发，不会互相影响，最终都会合并到主干上  
> 2. **分支的好处**  
> - 同时并行推进多个功能开发，提高开发效率  
> - 各个分支在开发过程中，如果某一个分支开发失败，不会对其他分支有任何影响。失败的分支删除重新开始即可。
  
### 4.2.1 创建分支
- 命令：git branch [分支名]  
![QQ截图20200910103010.png](https://i.loli.net/2020/09/10/xl78jCzgWtZ3kQS.png)
### 4.2.2 查看分支  
- 命令：git branch -v  
![QQ截图20200910103029.png](https://i.loli.net/2020/09/10/XKmcn7Ciz29Etlr.png)
### 4.2.3 切换分支
- 命令：git checkout [分支名]  
![QQ截图20200910103352.png](https://i.loli.net/2020/09/10/qiGO52cW9Ypn6jr.png)
### 4.2.4 合并分支
1. 第一步：切换到接受修改的分支上
git checkout [接受修改的分支名]
2. 第二步：执行merge命令
git merge [有新内容分支名]  
![QQ截图20200910143507.png](https://i.loli.net/2020/09/10/izVoHyYIBNxPK1D.png)
### 4.2.5 解决冲突
- 如果两个分支对同一个文件进行了不同的修改，在合并时，就会触发冲突。
![QQ截图20200910140810.png](https://i.loli.net/2020/09/10/brHfmtiqen7Qk6v.png)
- 冲突后git会自动进入合并模式。  
![QQ截图20200910144416.png](https://i.loli.net/2020/09/10/vBgyCuJ65nc49PF.png)
- 使用vim(或者其他编辑器打开冲突的文件)会发现git已在对应处进行标记，根据实际情况来编辑并解决冲突。  
![QQ截图20200910140904.png](https://i.loli.net/2020/09/10/qF6L1bXWJOuUgxh.png)
> 此图中，HEAD表示现在分支的情况，而hot_fix(被合并分支的名字)代表被合并分支的情况。
- 编辑完成后保存并退出，使用git add [文件名/.]，和git commit来提交分支的冲突解决情况。  
![QQ截图20200910141125.png](https://i.loli.net/2020/09/10/FCPh5BJKvo84TGt.png)
> 注意这里的git commit不用在最后添加文件名或者.。