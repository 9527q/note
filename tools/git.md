# GIT

设置大小写敏感，`git config core.ignorecase false`

本地分支和远程分支是相互独立的

## 1. 常用命令

### 1.1 初始化仓库

命令                      | 说明
--------------------------|---------------------------------------
`git init`                | 以当前所在文件夹创建初始化 git 仓库(在当前目录创建 .git 文件夹)
`git clone ssh或http链接` | 拉取远程仓库放到当前目录下，此时本地只有 master 一个分支

**ssh 还是 http？**
使用 ssh 需要事先将本地 ssh 公钥放到 git 服务器；使用 http 需要填写用户名和密码。

### 1.2 分支操作

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

### 1.3 查看代码情况

命令                                  | 说明
--------------------------------------|----------------------------------
`git status`                          | 查看当前仓库的改动情况（文件级别）
`git diff`                            | 以本地仓库为基准，工作区所做的改动
`git diff <branch1> <branch2>`        | 以分支1为基准，分支2所做的改动
`git diff <commit1-id> <commit2-id>`  | 以commit1为基准，commit2所做的改动
`git diff path1 path2 ...`            | 查看多个路径或文件的改动情况（不是他们之间的比较）
`git blame path/file`                 | 查看某具体文件的各行代码是在哪个版本哪个人改动的
`git log`                             | 查看 commit 历史
`git log -n`                          | 查看最近 n 次 commit 历史
`git reflog`                          | 查看 git 操作历史
`git show commit-id`                  | 查看某次 commit 的改动
`git show commit-id filename`         | 查看某次 commit 对某个文件的改动
`git remote`                          | 查看远程名字(一般是 origin)
`git remote get-url origin`           | 查看远程的仓库地址(origin 是`git remote`的值)
`git remote set-url origin <git-url>` | 修改远程仓库地址(origin 是`git remote`的值)
`git remote rm origin`                | 删除远程地址(origin 是`git remote`的值)
`git remote add orgin <git-url>`      | 添加远程地址 (origin 是`git remote`的值)

### 1.4 提交代码

命令                            | 说明
--------------------------------|-----------------------------------
`git add .`                     | 将工作区所有改动添加到暂存区（谨慎使用）
`git add path1/file1 path2 ...` | 将工作区指定路径下的改动或某文件的改动添加到暂存区
`git commit -m xxx`             | 将暂存区提交为一个版本（必须有说明）
`git commit`                    | 不加 -m 可以进入 commit 的编辑模式（也必须有说明）
`git commit --amend`            | 将暂存区提交到上一个commit中去(常用于补加东西或修改提交说明)
`git rebase -i <commit1-id>^`   | 把commit1及其之后的几个commit合并为一个
`git stash`                     | 将当前的改动全部暂时存放起来（此时再status将看不到那些改动）
`git stash apply`               | 将之前存储起来的改动布置到当前代码中
**rebase后的操作**：pick表示保留，f表示合并但不保留说明；最后末行模式执行 x 即可。

### 1.5 拉取推送代码

命令          | 说明
--------------|----------------------------------------
`git pull`    | 从对应的远程分支拉取代码到当前分支
`git push`    | 将当前分支的commit推送到远程
`git push -f` | 将当前分支的commit推送到远程(当历史commit不一致时用本地覆盖远程)

### 1.6 版本回退

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

## 2 快速关联/修改 Git 远程仓库地址

- 修改 .git 配置文件
   1. `vim .git/config`
   2. `[remote "origin"]` 下面的 `url = xxx` 那一行的值改为新的即可
- `git remote set-url origin <git-url>` (origin 是`git remote`的值)
- 先删除现在的远程地址，再添加新的远程地址
  1. `git remote rm origin` (origin 是`git remote`的值)
  2. `git remote add orgin <git-url>` (origin 是`git remote`的值)

## 3 GitHub 下载速度慢

1. 打开网址：[查询网站的 IP 地址](http://tool.chinaz.com/dns)
2. 查询 github.com、github.global.ssl.fastly.net 和 github-cloud.s3.amazonaws.com（用于 lfs 大文件存储）
3. 将 TTL 值小的放到 hosts 文件中

## 4 大文件存储

使用 [LFS （Git Large File Storage）](https://git-lfs.github.com/)，设置好后所有的操作都和普通情况下一样，但是 git 对大文件不会再进行行(hang)级别的管理。而是把大文件单独存放在一个地方，在工程中仅存储文本指针。即使大到几个 G，也能正常管理，整个的 git 工作流程不需要有任何变化，权限也是和仓库其余部分完全一样。总的来说，设置好后就什么都不用管了。

![git-lfs](images/git-lfs.gif)

1. 首先要安装 git-lfs，Homebrew: `brew install git-lfs` 
2. 进入到想要使用 git-lfs 的 git 工程中，`git lfs install`
3. 设置大文件的文件名表达式，`git lfs track "*.psd"`
   1. 如果是第一次执行此命令，会同时生成一个 .gitattributes 文件
   2. 如果不是第一次执行此命令，会将文件名表达是自动写入 .gitattributes 文件中
4. 然后就可以当作忘了这个事一样正常的去add、commit、push，都没问题。

## 5 设置 commit 钩子

1. 安装 [pre-commit](https://pre-commit.com/)
    ```bash
    pip install pre-commit
    ```
2. 在具体项目中激活 pre-commit
    ```bash
    # 项目目录中
    $ pre-commit install
    ```
3. 项目中添加文件 [`.pre-commit-config.yaml`](https://github.com/pre-commit/pre-commit/blob/master/.pre-commit-config.yaml)
    ```
    repos:
    -   repo: https://github.com/pre-commit/pre-commit-hooks
        rev: v2.1.0
        hooks:
        -   id: trailing-whitespace
        -   id: end-of-file-fixer
        -   id: check-docstring-first
        -   id: check-json
        -   id: check-yaml
        -   id: debug-statements
        -   id: name-tests-test
        -   id: requirements-txt-fixer
        -   id: double-quote-string-fixer
    -   repo: https://gitlab.com/pycqa/flake8
        rev: 3.7.7
        hooks:
        -   id: flake8
    -   repo: https://github.com/pre-commit/mirrors-autopep8
        rev: v1.4.3
        hooks:
        -   id: autopep8
    -   repo: https://github.com/pre-commit/pre-commit
        rev: v1.14.4
        hooks:
        -   id: validate_manifest
    -   repo: https://github.com/asottile/pyupgrade
        rev: v1.12.0
        hooks:
        -   id: pyupgrade
    -   repo: https://github.com/asottile/reorder_python_imports
        rev: v1.4.0
        hooks:
        -   id: reorder-python-imports
            language_version: python3
    -   repo: https://github.com/asottile/add-trailing-comma
        rev: v1.0.0
        hooks:
        -   id: add-trailing-comma
    -   repo: meta
        hooks:
        -   id: check-hooks-apply
        -   id: check-useless-excludes
    ```