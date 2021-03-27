# 名称

- rsyncd.conf - 守护进程模式下的rsync配置文件

## 简介

rsyncd.conf

## 描述

- rsyncd.conf文件是作为rsync守护进程运行时的配置文件。
- rsyncd.conf文件控制着认证、访问、日志和可用模块。

## 文件格式

- 该文件由模块和参数组成。
- 一个模块以方括号内的模块名称开始，一直到下一个模块开始。
- 模块包含的参数形式为name=value。

- 该文件是以行为基础的--也就是说，每一个以新行结束的行代表一个注释、一个模块名称或一个参数。

- 只有参数中的第一个等号才是重要的。第一个等号之前或之后的空白会被丢弃。
- 模块和参数名中的前导空格、后导空格和内部空白都是无关紧要的。
- 参数值中的前导空格和后导空格会被丢弃
- 参数值中的内部空白将被逐字保留。

- 任何以哈希(#)开头的行都会被忽略，只包含空格的行也会被忽略。
- (如果在前导空格以外的任何地方出现了一个哈希，它将被视为该行内容的一部分。)

- 任何以"/"结尾的行都会以UNIX习惯的方式在下一行 "继续"。

- 参数中等号后面的值都是字符串（不需要引号）或布尔值，可以是yes/no、0/1或true/false。
- 在布尔值中，大小写并不重要，但在字符串值中会保留。

## 启动rsync进程
- rsync守护进程通过为rsync指定--daemon选项来启动。

## 2全局变量

### 2全局变量

- motd file(motd文件)
- pid file(进程文件)
- port(端口)
- address(地址)
- socket options(接口选项)
- listen backlog(监听积压工作)

### 3子节点

#### 3.1

- comment (描述 解释)
- path（路径）
- use chroot（使用chroot）

#### 3.2

- daemon chroot(守护进程chroot)
- proxy protocol(代理协议)
- name converter(换名器)
- numeric ids(数字化IDs)
- munge symlinks（符号链接）

#### 3.3

- charset（字符集）
- max connections（最大连接数）
- log file(日志文件)
- syslog facility（系统日志设施）
- syslog tag(系统日志标记)
- max verbosity(最大冗余)
- lock file(锁文件)
- read only(只读)
- write only(只写)
- open noatime（开放时间）
- list（列表）
- uid(用户)
- gid(用户组)
- daemon uid(守护进程uid)
- daemon gid(守护进程运行的gid)

#### 3.4

- fake super(假超级)
- filter(过滤)
- exclude(排除文件)
- include（包含文件）
- exclude from（排除合并）
- include from（包含合并）
- incoming chmod（传入权限）
- outgoing chmod（导出权限）
- auth users（认证用户）

#### 3.5

- secrets file(密钥文件)
- strict modes(严谨模式)
- hosts allow(允许主机)
- hosts deny(拒绝主机)
- reverse lookup（反向查找）
- forward lookup（正向查找）
- ignore errors（忽略错误）
- ignore nonreadable（rsync守护进程忽略用户不可读文件）

#### 3.6

- transfer logging（格式化日志）
- log format(日志格式化)
- timeout(超时)
- refuse options(拒绝选择)

#### 3.7

- dont compress(不要压缩)
- early exec, pre-xfer exec, post-xfer exec(执行)