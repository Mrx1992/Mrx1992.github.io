参考网站
[我的博客](https://man.openbsd.org/ssh "ssh官网")

# 名字

        ssh：openssh的远程登陆客户端

## 总览

```
ssh [-46AaCfGgKkMNnqsTtVvXxYy] [-B bind_interface] [-b bind_address] [-c cipher_spec] 
[-D [bind_address:]port] [-E log_file] [-e escape_char] [-F configfile] [-I pkcs11] 
[-i identity_file] [-J destination] [-L address] [-l login_name] [-m mac_spec] [-O ctl_cmd] [-o option] [-p port] [-Q query_option] [-R address] [-S ctl_path] [-W host:port] 
[-w local_tun[:remote_tun]] destination [command]
```

## 描述

ssh（ssh客户端）是一个用于登录远程机器和在运程机器运行命令的程序。
它提供了一种通过不安全的网络的两个不受信任主机之间提供安全的机密通信。
X11连接，任意tcp端口或unix套接字都可通过安全通道转发。

ssh连接并登录到指定的目标，该目标可以指定为[user@]主机名或ssh://[user@]主机名[：port]形式的URI。
用户必须使用下方的几个方法证明他的身份（见下方）。

如果指定了一个命令，则会在远程机器上执行，而不是登录。

选项如下：

### 2各种选项

#### [2.1](2.1ssh-options.md)

- `-4（强制IPv4）`
- `-6（强制IPv6）`

#### [2.1](2.1ssh-options.md)