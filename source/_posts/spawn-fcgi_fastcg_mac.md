---
title: Mac OS下用Nginx/spawn-fcgi/fastcgi写C的Web应用
categories: [IT, C]
tags: [C, Web]
date: 2019-04-03 10:00:00
---

## I. 编写一个网页（在命令行运行）

### 1.下载安装fastcgi库

>brew install fcgi

### 2. 写一个动态网页

``` c
// 假设代码放到/projects/cgi目录
#include "fcgi_stdio.h" //要写在行首（fcgi_stdio.h里定义的printf与c里的冲突），且用冒号（引用路径而非全局）
#include <stdio.h>
#include <stdlib.h>

int main(void) {
    int count = 0;
    while(FCGI_Accept() >= 0) {
        printf("Content-type: text/html\r\n");
        printf("\r\n");
        printf("Hello Boot!<br>\r\n");
        printf("Request number %d.", count++);
    }
    return 0;
}

```
编译源代码：

>gcc /projects/cgi/boot.c -o /projects/cgi/boot.cgi -lfcg

注：如果找不到libfcgi.so，编译时要加上-L /usr/local/fastcgikit/lib/参数，指定依赖库所在的目录。

命令行运行：

>/projects/cgi/boot.cgi 

屏幕输出：

``` html
Content-type: text/html
Hello Boot!<br>
Request number 0
```
## II. 从浏览器访问boot.cgi

### 1. 安装Nginx、spawn-fcgi

>brew install nginx

brew install spawn-fcgi

### 2. 启动spawn

>spawn-fcgi -a 127.0.0.1 -p 9001 -F 1 -f /projects/cgi/boot.cgi

启动9001端口提供CGI服务。

### 3. 配置nginx连接spawn-fcgi，重新启动

在server节点（比如localhost）增加一个路径匹配：

```
location ~ ^.*\.cgi$ {
    root /project/cgi/;
    fastcgi_pass 127.0.0.1:9001; #让其监听9001端口，与spawn-cgi监听端口一致
    fastcgi_index index.cgi;
    fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    include fastcgi_params;
}
```

<font style="color:red">
注：经测试发现，配置中fastcgi_index、fastcgi_param、root都是不必要的; 关键就在fastcgi_pass配置。但是网上看别人资料从未有提起。
</font>

### 4. 访问该网页

浏览器输入：http://localhost/boot.cgi 返回页面显示：

```
Hello Boot!
Request number 0.

```

反复访问这个URL，Request number的值会加1，大家可以自己思考下这是为什么。