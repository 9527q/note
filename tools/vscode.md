# VS Code

Visual Studio Code 是微软基于 Electron 开发(但并不是Atom的fork)的开源代码编辑器，支持Windows、Linux、macOS，界面简洁，简单易用，轻量级，插件库非常丰富(各种语言和小工具，管理操作也很简单)，支持测试，语法高亮，括号匹配，代码片段收集，内置Git版本控制，支持个性化配置(主题、快捷键、各种属性和参数)。

## Mac快捷键

o | i
-|-
⌘ X | 剪切光标所在行或剪切选中部分
⌘ , | 打开设置
⌥ ↕ | 选中部分所在行(可多)上下移动
↩︎ | 选中文件(夹)为修改名字(再次 ↩ 确认)；选中项目目录为打开和关闭

## 打开设置

- ⌘ ,
- Code -> Preference -> Settings
- 「左下角小齿轮」 -> Settings

## 设置代码竖线

【设置】-> 找到 Rulers -> 打开 settings.json 文件 ->
设置editor.rulers = [79]

![vscode-rulers](images/vscode-rulers.png)
![vscode-code-line](images/vscode-code-line.png)

## 常见问题

1. 能不能打开 VS Code 后直接创建一个项目目录？
    - 不行，项目目录必须是已经存在的
    - 可以创建文件
2. 设置界面的颜色主题：「左下角小齿轮」 ➡ 「Color Theme」
3. 自动保存设置：「左下角小齿轮」 ➡ 「Settings」 ➡ 「Commonly Used」 ➡ 「Files: Auto Save」，选择适合自己的
4. 快捷键：用浏览器打开html文件，下载一个插件（<kbd>⇧</kbd> <kbd>⌘</kbd> <kbd>X</kbd>）：Open HTML in Default Browser
   ![vscode_open_html](images/vscode_open_html.png)

## 插件

- Markdown All in One
  - 格式化表格，选中表格，<kbd>⌘</kbd> <kbd>K</kbd> + <kbd>⌘</kbd> <kbd>F</kbd>
  - 加 ``` ` * _ ( [ ``` 等时可以直接选中文字部分，然后输入即可。