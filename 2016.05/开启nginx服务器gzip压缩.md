title: "开启nginx服务器gzip压缩 - 前端运维小记"
date: 2015-08-26 15:57:07
categories: 运维
tags: 服务器
---
## 操作步骤
1. 打开nginx conf配置文件 vi nginx.conf
2. 在http配置中插入以下配置项(以下为我个人服务器配置，具体参数可参考下面的详细说明自定义)
> gzip on;<br>
gzip_min_length  2k;<br>
gzip_buffers     4 16k;<br>
gzip_http_version 1.0;<br>
gzip_comp_level 3;<br>
gzip_types       text/plain text/javascript application/javascript     application/x-javascript text/css application/xml application/x-httpd-php image/jpeg image/gif image/png;<br>
gzip_vary on;<br>

3. 保存退出vi
4. 重启nginx服务器
5. 打开网页并通过控制台查看response header 是否存在`Content-Encoding:gzip`项

**注意：**
`text/javascript` `application/javascript` `application/x-javascript` 这三种类型都可以表示javascript类型，
但很多教程中都没有给全，导致我在配置的时候一直以为不成功，后来才发现原来是类型没有给全！！！

## 配置详解
### gzip
决定是否开启gzip模块

param:on|off

example:`gzip on;`

### gzip_buffers
设置gzip申请内存的大小,其作用是按块大小的倍数申请内存空间

param1:int

param2:int(k) 后面单位是k

example: `gzip_buffers 4 8k;`

### gzip_comp_level
设置gzip压缩等级，等级越底压缩速度越快文件压缩比越小，反之速度越慢文件压缩比越大

param:1-9

example:`gzip_com_level 1;`

### gzip_min_length
当返回内容大于此值时才会使用gzip进行压缩,以K为单位,当值为0时，所有页面都进行压缩

param:int

example:`gzip_min_length 1000;`

### gzip_http_version
用于识别http协议的版本，早期的浏览器不支持gzip压缩，用户会看到乱码，所以为了支持前期版本加了此选项,目前此项基本可以忽略

param: 1.0|1.1

example:`gzip_http_version 1.0;`

### gzip_proxied
Nginx做为反向代理的时候启用，
param:off|expired|no-cache|no-sotre|private|no_last_modified|no_etag|auth|any]

expample:`gzip_proxied no-cache;`

`off` – 关闭所有的代理结果数据压缩

`expired` – 启用压缩，如果header中包含”Expires”头信息

`no-cache` – 启用压缩，如果header中包含”Cache-Control:no-cache”头信息

`no-store` – 启用压缩，如果header中包含”Cache-Control:no-store”头信息

`private` – 启用压缩，如果header中包含”Cache-Control:private”头信息

`no_last_modified` – 启用压缩，如果header中包含”Last_Modified”头信息

`no_etag` – 启用压缩，如果header中包含“ETag”头信息

`auth` – 启用压缩，如果header中包含“Authorization”头信息

`any` – 无条件压缩所有结果数据

### gzip_types
设置需要压缩的MIME类型,非设置值不进行压缩

param:text/html|application/x-javascript|text/css|application/xml

example:`gzip_types text/html;`
