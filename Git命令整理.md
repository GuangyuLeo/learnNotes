## 生成ssh密钥
`ssh-keygen -t rsa -C "email@address.com"`

## GIT命令列表与说明
### 本地命令

* 创建版本库
`git init [dir]`
* 设定用户
`git config --global user.name "name"`
`git config --global user.email "email"`
> --global命令针对所有仓库，默认针对当前Reository
* 添加文件至stage暂存区
`git add [dir/fileName]`
* 提交文件至当前分支及说明
`git commit -m "说明"`
* 检查当前版本库状态
`git status`
* 查看提交历史
`git log --pretty=oneline`
* 查看命令历史
`git reflog`
* 版本回退
`git reset --hard [headNo|HEAD^|HEAD-no]`
> **HEAD**表示当前版本，**^**表示上一版本，可以使用git log 查看head编号，输入部分head编号来回退至指定版本
* 查看版本区别
`git diff HEAD --fileName`
* 对某个文件撤回修改（回到最近一次commit or add 后的状态）
`git checkout -- fileName`
* 对某个已放入stage暂存区的文件撤销add操作
`git reset HEAD -- fileName`
### 远程命令
* curl调用api接口创建GitHub远程库

  `curl -u 'GuangyuLeo':'password' https://api.github.com/user/repos -d '{"GuangyuLeo":"learnNotes"}'`

* 关联远程Origin库
  `git remote add origin https://github.com/GuangyuLeo/learngit.git`

* 推送本地master至origin库并关联
  `git push -u origin master`

* 从远程origin库克隆到本地
  `git clone git@github.com:GuangyuLeo/gitskills.git`

* 查看远程库信息
  `git remote`
  `git remote -v`
> github提供两种地址分别支持ssh和https，https需要登录github，ssh只需要添加rsa密匙
* 推送分支
`git push`
`git push origin master`
`git push origin dev`
* 抓取分支
`git checkout -b dev origin/dev`
* 抓取合并分支到本地分支
`git pull`
`git pull origin dev`
* 设置本地与远程库分支的链接
`git branch --set-upstream-to=origin/dev dev`

## 创建与合并分支
* 创建dev分支，然后切换到dev
`git checkout -b dev`
> `git checkout`命令加上 `-b`参数表示创建并切换，等于以下两个命令
	1. 创建分支： `git branch dev`
	2. 切换分支： `git checkout dev`
* 查看当前分支
`git branch`
> 列出所有分支，当前分支用*标出
* 合并某分支到当前分支
`git merge <name>`
> 合并时如果可能，git会使用fast-forward模式合并分支，导致分支删除后丢失分支信息（无法看出曾经做过合并）
> 禁用ff会在merge时进行自动commit，从分支历史上就可以看出合并过。
	`git merge --no-ff -m "merge with no-ff" dev
* 删除分支
`git branch -d <name>`
* 删除没有merge过的分支
`git branch -D <name>`

## 解决冲突
* 当分支合并无法自动合并时，首先解决冲突，再提交冲突文件以完成合并
* 查看合并分支图
`git log --graph`
`git log --graph --pretty=online --abbrev-commit`

## bug分支
* 临时需要创建bug修复分支，而当前尚有未完成工作，保存当前工作现场
`git stash`
* 查看保存的现场
`git stash list`
* 还原现场
`git stash apply`
* 删除保存的现场
`git stash drop`
* 还原现场的同时删除
`git stash pop`

## 变基
* 整理基线，消除分叉
`git rebase`

## 标签管理
* 创建标签
`git tag v1.0`
* 查看所有标签
`git tag`
* 对某个commit打上标签
`git tag v1.0 commit_No`
* 查看标签信息
`git show <tagname>`
* 创建带有说明的标签，-a指定标签名，-m指定文字说明
`git tag -a v1.0 -m "version 1.0 released" commit_No`
* 删除标签
`git tag -d <tagname>`
* 推送本地tag到远程仓库
`git push origin <tagname>`
`git push origin --tags`
* 删除本地标签后删除远程标签
`git push origin :refs/tags/v0.9`



































