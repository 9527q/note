# 环境配置


## Mac

1. 安装 [Homebrew](https://brew.sh/index_zh-cn)
    ```bash
    /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`
    ```

## git

1. 用[查询网站的 IP 地址](http://tool.chinaz.com/dns)更改有关 github 的 hosts 配置
   > github.com、github.global.ssl.fastly.net、github-cloud.s3.amazonaws.com
2. 生成 ssh 密钥并将公钥放到 git 服务器上
    ```bash
    ssh-keygen
    ```
3. 下载 git 大文件管理
   ```bash
   brew install git-lfs
   ```
4. 钩子准备
   ```bash
   pip install pre-commit
   ```

## 软件

- all
  - Wireshark、Webstorm、Chrome、TorBrowser、Anaconda、网易MuMu、微信、QQ
- macOS
  - Magnet、Mindnode、Hands Off!、Office、iTerm、Paw、Video GIF Creator
- Win
  - Postman

## Pycharm

1. [下载](https://www.jetbrains.com/pycharm/download/)
   1. 安装时勾选 markdown 插件
   2. [破解](http://idea.lanyus.com)
2. 设置背景图片:Shift Shift -> set background image
3. 设置代码规范：Shift Shift -> Inspections -> Python -> 
   - Missing or empty docstring
4. 设置 Font：Menlo、14、1.0; Color Scheme: Monkai;
5. 设置79字符竖线: 设置 -> Editor -> Code Style -> Python -> Hard wrap at -> 79

## vs code

1. 设置代码竖线：【⌘ ,】 -> Text Editor -> Rulers -> Edit in settings.json -> `editor.rulers = [79]`
2. 设置自动保存：【⌘ ,】 -> Commonly Used -> Files: Auto Save -> 选择适合自己的
3. 安装插件：【⇧ ⌘ X】
   - Markdown All in One
   - Open HTML in Default Browser

## 每个git项目单独操作

1. 使用 git-lfs 进行大文件管理：`git lfs install`，`git lfs track "*.psd"`
2. 设置文件名大小写敏感：`git config core.ignorecase false`
3. 设置 commit 检查
   1. `pre-commit install`
   2. 建立 [`.pre-commit-config.yaml`](https://github.com/pre-commit/pre-commit/blob/master/.pre-commit-config.yaml) 文件