# ![paw](images/paw-icon.jpg)

## 如何设置 cookie

### 1. 查看网站使用了哪些 cookie

> 以 Chrome 为例

第一种方式：**查看所有使用的 cookie**

1. 打开一个网页后，点击地址栏中地址左侧的🔒或者⚠️，选择cookie ![paw-cookie-look1](images/paw-cookie-look1.jpg)
2. 找到某一个具体的 cookie，下面可以查看其名称、值、域名、路径 ![paw-cookie-look2](images/paw-cookie-look2.jpg)

第二种方式：**查看请求发送的 cookie**

1. 网页中 <kbd>右键</kbd>，选择「检查」，弹出窗口中选择「Netword」![paw-cookie-look3](images/paw-cookie-look3.jpg)
2. 刷新网页，在下面的请求中找到一个请求，点击它 ![paw-cookie-look4](images/paw-cookie-look4.jpg)
3. 找到 Headers -> Request Headers，下面有一项 `Cookie`，后面跟的即是真正发送到服务器的 cookie，是用分号分隔的一个个 键=值 的键值对。 ![paw-cookie-look5](images/paw-cookie-look5.jpg)

至此，已经能通过两种方式查看某网站使用的 cookie 了。

### 2. 在 paw 中设置 cookie

假设某网站只有两个 cookie：csrftoken 和 sessionid

**为某一个请求单独设置**

1. 选择一个请求的 headers，新建一个键值对，键填入 `Cookie`（注意下面演示图中是错的，多了个s），值输入 cookie 字样选择弹出的 Cookies 选项 ![paw-cookie-set1](images/paw-cookie-set1.png)
2. 双击值的 Cookies，依次输入之前已经找到的 cookie 键值对即可 ![paw-cookie-set2](images/paw-cookie-set2.jpg)

**为某个域名下的所有请求设置**

1. 新建一个 session 并点击 manage 打开管理标签页
2. 新建键值对并设置值
3. 填入 Domain 的值为域名

![paw-cookie-set3](images/paw-cookie-set3.png)
