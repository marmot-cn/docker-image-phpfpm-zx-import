# 导入服务镜像

---

## 概述

是在后端镜像基础上添加功能, 用于实现`excel`导入到`mysql`,`mongo`以及远程`oracle`数据库.

因为`php`的`composer`包`"phpoffice/phpspreadsheet": "1.0.0"`需要使用`gd`和`iconv`库支持, 所以额外编译`gd`库.

## 基本配置项

* 开启`opcache`
* `post_max_size`设置`post`传输限制
* `date.timezone`设定时区
* `memory_limit`设定内存限制, 这里限制为`512MB`, 限定用户导入`excel`为`5MB`进行测试.
* `file_uploads = off`上传文件功能关闭
* `upload_tmp_dir`虽然上传文件功能关闭, 还是把上传文件路径指向到别的位置
* `display_errors = off`不输出错误
* `error_reporting = E_ALL`错误级别,设定到`notice`
* `log_errors = on`开启记录错误日志, 因为默认配置文件会把错误输出指向到标准错误输出
* `expose_php = off`不返回`php版本号`
* `html_errors = off`关闭错误引导链接

## 基本编译配置项

* `--disable-session`禁用`session`
* `--enable-zip`
* `-enable-pcntl` 启用进程, 后端需要
* `--enable-sysvmsg`
* `--enable-sysvsem`
* `--enable-sysvshm`
* `--enable-bcmath` rabbitmq 需要

## 扩展安装

* inotify `2.0.0`
* memcached `3.0.3`
* mongo `1.2.10`
* redis `3.1.3`
* oracle(`oci8.so`)
* iconv
* gd
* mcrypt

### apt包

#### memcached

* `libmemcached-dev`
* `zlib1g-dev`

#### mongo

* `libssl-dev`

### 编译

#### memcached

因为在后端服务不使用`session`, 所以编译扩展不需要支持该项.

指定`--disable-memcache-session`, 否则会出现`Cannot find php_session.h`.

#### redis

因为在后端服务不使用`session`, 所以编译扩展不需要支持该项.

需要指定 `--disable-redis-session`, 否则会出现`Cannot find php_session.h`.