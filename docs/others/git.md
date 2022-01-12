# git

## 基础操作

 - 查看Git命令 ： `git`
 - 创建git仓库：`git init`
 - 查看当前仓库文件变化情况：`git status`
 - 添加修改：`git add` （可使用git add . 来添加当前仓库所有修改，尽量不要这么做）
 - 本次还没有提交的更改：`git diff`（比较工作区与暂存区的区别）
 - 回滚，撤销提交操作：`git reset`
 - 向Git提交内容：`git commit -m "xxx"` （xx为对提交的内容进行描述）
 - 让Git不提交某些文件/忽略某些文件：创建文件 .gitignore 并在文件中添加文件名/文件夹名 即可 （若git已经开始追踪某些文件 则需要11）
 - 让Git不再追踪某个/某些文件：`git rm --cached xxx`
 - Git创建分支：`git branch -b xxx`
 - Git切换分支：`git checkout xxx`
 - 合并分支：`git merge xxx`
 - 列出本地分支：`git branch`
 - 删除分支: `git branch -d xxx` (-D强制删除)
 - 添加远程仓库：`git remote add origin xxx` （xxx为远程地址）
 - 设置本地分支追踪远程分支：`git push --set-upstream`
 - 克隆仓库：`git clone xxx`

若push克隆下来的仓库到自己仓库时出现：`error: 远程 origin 已经存在`，只需要运行`git remote rm origin`将远程配置删除，重新添加远程地址即可。



## 进阶操作

### stash changes

### git rebase

git rebase可以对某一段线性提交历史进行编辑、合并、删除等操作。因此，合理使用rebase命令可以使我们的提交历史干净、简洁！

> 但是不要通过rebase对任何已经提交到公共仓库中的commit进行修改，除非是自己的独立分支。

即使是自己的独立分支，对已经push到线上的commit进行更改后也只能通过强推的方式push。所以尽量先在本地进行rebase。

 - pick：保留该commit（缩写:p）
 - reword：保留该commit，但我需要修改该commit的注释（缩写:r）
 - edit：保留该commit, 但我要停下来修改该提交(不仅仅修改注释)（缩写:e）
 - squash：将该commit和前一个commit合并（缩写:s）
 - fixup：将该commit和前一个commit合并，但我不要保留该提交的注释信息（缩写:f）
 - exec：执行shell命令（缩写:x）
 - drop：我要丢弃该commit（缩写:d）


### cherry-pick

假如当前的git log是：
```bash
commit 3reqwr: abc
commit 2weqwr: defg
commit 1fdass: hi
commit 0fjdal: original
```


我们基于commit 0拉了一个新分支，如何在其上面提交了3笔，现在想要将这三笔合成一笔，除了使用rebase外（rebase用不好容易出问题），还可以使用`git reset --soft 0fjdal`，回退到提交之前，这时后3笔提交会缓存到暂存区，如何再重新commit一下即可。

`git commit --amend` 将当前更改追加到上一笔提交。

参考：
https://www.jianshu.com/p/4a8f4af4e803