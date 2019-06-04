# 环境配置


## Mac

1. 安装 [Homebrew](https://brew.sh/index_zh-cn)：`/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`
2. 软件：

## git

1. 生成 ssh 密钥：`ssh-keygen`；将公钥放到 git 服务器上
2. 用[查询网站的 IP 地址](http://tool.chinaz.com/dns)更改有关 github 的 hosts 配置
   > github.com、github.global.ssl.fastly.net 和 github-cloud.s3.amazonaws.com（用于 lfs 大文件存储）
3. 下载 git 大文件管理：`brew install git-lfs`
   > 使用git-lfs进行大文件管理：`git lfs install`，`git lfs track "*.psd"`（每个工程执行）
4. 设置文件名大小写敏感：`git config core.ignorecase false`（每个工程执行）

## 软件

- all
  - Wireshark、Webstorm、Chrome、TorBrowser、Anaconda、网易MuMu、微信、QQ
- macOS
  - Magnet、Mindnode、Hands Off!、Office、iTerm、Paw
- Win
  - Postman

## Pycharm

1. [下载及安装](https://www.jetbrains.com/pycharm/download/)
   1. 安装时选择markdown插件
2. [破解](http://idea.lanyus.com)
3. 设置背景图片:Shift Shift -> set background image
4. 设置代码规范：Shift Shift -> Inspections -> Python -> 
   - Missing or empty docstring
5. 设置 Font：Menlo、14、1.0; Color Scheme: Monkai;
6. 设置79字符竖线: 设置 -> Editor -> Code Style -> Python -> Hard wrap at -> 79

## vs code

1. 设置代码竖线：【⌘ ,】 -> Text Editor -> Rulers -> Edit in settings.json -> `editor.rulers = [79]`
2. 设置自动保存：【⌘ ,】 -> Commonly Used -> Files: Auto Save -> 选择适合自己的
3. 安装插件：【⇧ ⌘ X】 -> Markdown All in One
