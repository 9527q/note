# GIT

设置大小写敏感，`git config core.ignorecase false`

本地分支和远程分支是相互独立的

## 常用命令

### 初始化仓库

命令                      | 说明
--------------------------|---------------------------------------
`git init`                | 以当前所在文件夹创建初始化 git 仓库(在当前目录创建 .git 文件夹)
`git clone ssh或http链接` | 拉取远程仓库放到当前目录下，此时本地只有 master 一个分支

**ssh 还是 http？**
使用 ssh 需要事先将本地 ssh 公钥放到 git 服务器；使用 http 需要填写用户名和密码。

### 分支操作

命令                                                                 | 说明
---------------------------------------------------------------------|--------------------------------
`git branch`                                                         | 查看本地分支，当前分支用‘*’+‘绿色’标出
`git branch -r`                                                      | 查看远程分支
`git branch -a`                                                      | 查看本地和远程所有分支
`git branch -d <branch-name>`                                        | 删除某个分支
`git branch --set-upstream-to=origin/<branch-origin> <branch-local>` | 设置本地分支跟踪某远程分支(pull/push到哪个远程分支)
`git checkout <branch-name>`                                         | 切换到目标分支
`git checkout -b <branch-name>`                                      | 切换或「新建并切换」到目标分支
`git checkout -b <branch-local> origin/<branch-origin>`              | 创建分支并设定跟踪某远程分支
`git merge <branch-name>`                                            | 将分支 branch-name 合并到当前分支

### 查看代码情况

命令                                 | 说明
-------------------------------------|--------------------------
`git status`                         | 查看当前仓库的改动情况（文件级别）
`git diff`                           | 以本地仓库为基准，工作区所做的改动
`git diff <branch1> <branch2>`       | 以分支1为基准，分支2所做的改动
`git diff <commit1-id> <commit2-id>` | 以commit1为基准，commit2所做的改动
`git diff path1 path2 ...`           | 查看多个路径或文件的改动情况（不是他们之间的比较）
`git blame path/file`                | 查看某具体文件的各行代码是在哪个版本哪个人改动的
`git log`                            | 查看 commit 历史
`git log -n`                         | 查看最近 n 次 commit 历史
`git reflog`                         | 查看 git 操作历史
`git show commit-id`                 | 查看某次 commit 的改动
`git show commit-id filename`        | 查看某次 commit 对某个文件的改动

### 提交代码

命令                            | 说明
--------------------------------|-----------------------------------
`git add .`                     | 将工作区所有改动添加到暂存区（谨慎使用）
`git add path1/file1 path2 ...` | 将工作区指定路径下的改动或某文件的改动添加到暂存区
`git commit -m xxx`             | 将暂存区提交为一个版本（必须有说明）
`git commit --amend`            | 将暂存区提交到上一个commit中去(常用于补加东西或修改提交说明)
`git rebase -i <commit1-id>^`   | 把commit1及其之后的几个commit合并为一个
`git stash`                     | 将当前的改动全部暂时存放起来（此时再status将看不到那些改动）
`git stash apply`               | 将之前存储起来的改动布置到当前代码中

**rebase后的操作**：pick表示保留，f表示合并但不保留说明；最后末行模式执行 x 即可。

### 拉取推送代码

命令          | 说明
--------------|----------------------------------------
`git pull`    | 从对应的远程分支拉取代码到当前分支
`git push`    | 将当前分支的commit推送到远程
`git push -f` | 将当前分支的commit推送到远程(当历史commit不一致时用本地覆盖远程)

### 版本回退

命令                  | 说明
----------------------|--------------------
`git reset HEAD^^`    | 回退多个版本，几个 ^ 就表示几个版本
`git reset HEAD~n`    | 回退 n 各版本
`git reset commit-id` | 回退到制定版本

**reset 的三个参数**：

- `--mixed` 指定版本之后的所有版本的改动放到工作区
- `--soft` 软回退，指定版本之后的所有版本的改动放到暂存区
- `--hard` 指定版本之后的所有版本的改动都舍弃掉
- 注意：当前工作区、暂存区也属于上述被操作的改动

将暂存区回退到工作区：`git reset HEAD file1`
