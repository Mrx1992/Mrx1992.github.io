# 全局参数

## 简介

- 文件中的第一个参数（在[module]头之前）是全局参数。
- Rsync还允许使用“[global]”模块名来指示一个或多个全局参数部分的开始（名称必须是小写）。

- 你也可以在配置文件的全局部分包含任何模块参数，在这种情况下，提供的值将覆盖该参数的默认值。

- 可以在参数的值中使用对环境变量的引用。
- 字符串参数的 %VAR% 引用将尽可能晚地展开（当字符串在程序中首次使用时），允许使用 rsync 在连接时设置的变量，如 RSYNC_USER_NAME。
- 非字符串参数（如真/假设置）在从配置文件中读取时被展开。
- 如果一个变量在环境中不存在，或者一个字符序列不是有效的引用（如未配对的百分号），则原始字符将被原封不动地传递。
- 这有助于实现向后的兼容性和安全性（例如，在路径中把一个不存在的%VAR%扩展为一个空字符串可能会导致一个非常不安全的路径）
- 在值中插入%的最安全的方法是使用%%。

## 参数

### motd file(motd文件)

- 此参数允许您指定在每次连接时向客户显示提示消息。
- 通常包含网站信息和任何法律声明。
- 默认值是不显示motd文件
- 当启动守护进程时，可以用--dparam=motdfile=FILE命令行选项来覆盖这个参数。

### pid file(进程文件)

- 这个参数告诉rsync守护进程将其进程ID写入该文件。
- rsync会锁定该文件，以便它知道什么时候可以安全地覆盖现有文件。
- 当启动守护进程时，文件名可以被--dparam=pidfile=FILE命令行选项覆盖。

### port(端口)

- 你可以通过指定这个值来覆盖守护进程的默认监听端口（默认值为873）。
- 如果守护进程由inetd运行，这个值会被忽略，并被--port命令行选项所取代。

### address(地址)

- 通过指定此值，可以覆盖守护进程将侦听的默认IP地址。
- 如果守护进程由 inetd 运行，这个值会被忽略，并被 --address 命令行选项取代。

### socket options(接口选项)

- 这个参数可以为喜欢把系统调到极致的人提供无穷的乐趣。
- 你可以设置各种各样的套接字选项，这些选项可能会使传输更快（或更慢！）。
- 请阅读setsockopt()系统调用的man页面，了解你可以设置的一些选项的细节。
- 默认情况下，没有设置特殊的套接字选项。这些设置也可以通过--sockopts命令行选项来指定。

### listen backlog(监听积压工作)
- 您可以在守护进程监听连接时覆盖默认的backlog值。默认值为5。