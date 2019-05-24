# Mac 安装 node、npm

## 安装

```sh
brew install node
```

## 查看是否成功安装

```sh
$ node -v
v11.6.0
$ npm -v
6.5.0
```

## 看到啤酒🍺了但是 node 提示没有

```sh
$ brew install node
...
🍺  /usr/local/Cellar/node/11.6.0: 3,938 files, 46.6MB
$ node
-bash: node: command not found
```

### 解决
可能是安装上了，但是安装之后创建链接等步骤没有完成，查看安装记录，应该有提示信息：

```sh
Warning: The post-install step did not complete successfully.
You can try again using `brew postinstall node`
```

那我们就把安装后该做的步骤再来一次试试

```sh
brew postinstall node
```

但是很可能还报上面的错误，这时顺着安装信息再网上看，还应该有提示信息：

```sh
The `brew link` step did not complete successfully`.
The formula built, but is not symlinked into /usr/local
Could not symlink include/node/common.gypi
Target /usr/local/include/node/common.gypi
already exists. You may want to remove it:
  rm '/usr/local/include/node/common.gypi'

To force the link and overwrite all conflicting files:
  brew link --overwrite node

To list all files that would be deleted:
  brew link --overwrite --dry-run node
```

如果是上面这个报错的话，那就用它提示这个命令来操作：`brew link --overwrite node`，强制覆盖已经存在的链接。（`brew link --overwrite --dry-run node` 可以先查看一下哪些会被删除）

在执行时可能遇到类似这样的报错：`Could not symlink include/node/common.gypi`，这时只要把信息中提示的文件删去，再次执行 `brew link --overwrite node` 即可，这个过程可能重复多次。

# node 安装好了但是找不到 npm

问题：

```sh
# node 安装好了但是找不到 npm
$ node -v
v11.6.0
$ npm -v
bash: /usr/bin/npm: No such file or directory
```

解决：

```sh
# 1. 找到 npm 在哪里，可能会找到多个，看看哪个是刚刚安装的 node 下的
$ find / -name "npm-cli.js"
/usr/local/Cellar/node/11.6.0/libexec/lib/node_modules/npm/bin/npm-cli.js

# 2. 测试这个 npm 是不是正常的
$ /usr/local/Cellar/node/11.6.0/libexec/lib/node_modules/npm/bin/npm-cli.js -v
6.5.0

# 3. 创建链接
$ ln -s /usr/local/Cellar/node/11.6.0/libexec/lib/node_modules/npm/bin/npm-cli.js /usr/bin/npm
```

## ln 报错

问题：使用 `ln` 将链接创建到 `/usr/bin` 时报错 `Operation not permitted`，并且使用 `sudo` 也不管用

解决：将连接创建到 `/usr/local/bin`