<h1 align="center">Postman 简单使用</h1>

[下载](https://www.getpostman.com/downloads/)

## 安装及配置

1. 打开安装包，会在统计目录得到 postman 应用，双击
   1. 双击打开后会弹出选项框，说它可以把自己移动到“应用程序”目录下，点击让它自己移动过去就好，过一会儿就会打开 ![postman-install](./images/postman-install.jpg)
2. 打开就是创建页面，可以取消勾选让它不是默认打开。我们选择创建一个集合叫厨芯。 ![](images/postman-open.jpg) ![](images/postman-create-collection.jpg)
3. 打开集合创建一个请求，这个请求的存储会默认选到当前集合。如果是在左上角点击New创建的请求，要指定集合来存储。 ![](images/postman-collection-add-request.jpg) ![](images/postman-create-request.jpg)
4. 编辑请求的基本信息，然后设置 cookie（[查看一个页面的cookie](./paw.md)），postman里面同一个域名下的cookies都是公用的，无需重复创建 ![](images/postman-request-edit.jpg) ![](images/postman-create-cookies.jpg) ![](images/postman-cookies-addcookie.jpg) 在这个域名下有多个 cookie，下图中的 Add Cookie 多点几次填写好信息就行了。 ![](images/postman-cookies-add-cookie.jpg)
5. post 请求要通过 body 来设置请求体，数据的类型有 text/file，最后访问就可以了。 ![](images/postman-post-body.jpg) ![](images/postman-post-send.jpg)