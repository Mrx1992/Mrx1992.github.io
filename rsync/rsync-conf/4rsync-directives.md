**# 模块参数总结(8)**



**## CONFIG DIRECTIVES**



\- 目前有两个配置指令允许配置文件合并其他文件的内容：&include和&merge。

\- 这两个指令都允许引用一个文件或一个目录。

\- 它们的不同之处在于文件内容被认为是分离的。



\- &include指令将每个文件处理得比较独特，每个文件都继承了父文件的默认值，

\- 以globals/defaults的方式开始参数解析，而对父文件的其他部分的解析则不改变默认值。





\- 而&merge指令则把文件的内容当作是简单的插入指令的地方，

\- 因此它可以在另一个文件中启动的模块中设置参数，可以影响其他文件的默认值等。



\- 当一个&include或&merge指令提到一个目录时，

\- 它将读入该目录内包含的所有*.conf或*.inc文件(分别)(不进行任何递归扫描)，文件按字母顺序排列。

\- 因此，如果您有一个名为 "rsyncd.d "的目录，里面有 "foo.conf"、"bar.conf "和 "baz.conf "三个文件



\- 本指令：

```
&include /path/rsyncd.d
```



\- 会和这组指令一样：



\```

&include /path/rsyncd.d/bar.conf

&include /path/rsyncd.d/baz.conf

&include /path/rsyncd.d/foo.conf

\```



\- 除了它会随着目录中文件的添加和删除而调整。



\- &include指令的优点是可以在一个单独的文件中定义一个或多个模块，而不用担心自带的模块文件之间会产生意外的副作用。



\- &merge指令的好处是，你可以加载可以包含在多个模块定义中的配置片段，你还可以设置影响连接的全局值（如motd文件），

\- 或者影响其他include文件的globals。



\- 例如，这是一个有用的/etc/rsyncd.conf文件：

\```

port = 873

log file = /var/log/rsync.log

pid file = /var/lock/rsync.lock



&merge /etc/rsyncd.d

&include /etc/rsyncd.d

\```

\- 这将合并任何/etc/rsyncd.d/*.inc文件（对于全局值应该保持有效），

\- 然后包含任何/etc/rsyncd.d/*.conf文件（定义没有任何全局值交叉的模块）。



\> include比较独立，全局变量都是互相独立

\> merge将合并全局变量，对之前定义的全局变量将保存住



**### AUTHENTICATION STRENGTH**

\- rsync中使用的认证协议是一个基于128位MD4的挑战响应系统。

\- 但这是相当弱的保护（至少有一种粗暴的哈希查找算法公开），

\- 所以如果你想要真正的顶级安全，那么我建议你在ssh上运行rsync（是的，未来版本的rsync会改用更强的哈希方法）。



\- 此外，请注意rsync守护进程协议目前并没有对通过连接传输的数据进行任何加密。

\- 只提供认证。如果你想要加密，请使用ssh作为传输。



\- 如果您把rsync放在SSL代理后面，您也可以使用SSL/TLS加密。



**### SSL/TLS Daemon Setup(SSL/TLS守护进程设置)**

\- 当设置一个rsync守护进程通过SSL/TLS访问时，你需要配置一个代理（如haproxy或nginx）作为处理加密的前端。

  \- 你应该限制对后台rsyncd端口的访问，只允许代理连接。

  \- 如果它和代理服务器在同一个主机上，那么将它配置为只监听localhost是个好主意。



  \- 如果您的代理支持发送信息，您应该考虑开启代理协议参数。

  \- 下面的例子假设启用了这个功能。

  

Haproxy设置的例子如下:

\```

frontend fe_rsync-ssl

   bind :::874 ssl crt /etc/letsencrypt/example.com/combined.pem

   mode tcp

   use_backend be_rsync



backend be_rsync

   mode tcp

   server local-rsync 127.0.0.1:873 check send-proxy

\```



一个nginx代理设置的例子如下:

\```

stream {

   server {

​       listen 874 ssl;

​       listen [::]:874 ssl;



​       ssl_certificate /etc/letsencrypt/example.com/fullchain.pem;

​       ssl_certificate_key /etc/letsencrypt/example.com/privkey.pem;



​       proxy_pass localhost:873;

​       proxy_protocol on; # Requires "proxy protocol = true"

​       proxy_timeout 1m;

​       proxy_connect_timeout 5s;

   }

}

\```



**### 例子**

\- 一个简单的rsyncd.conf文件，允许匿名rsync到/home/ftp的ftp区域。

\```

[ftp]

​        path = /home/ftp

​        comment = ftp export area

\```



\- 一个更复杂的例子是：

\```

uid = nobody

gid = nobody

use chroot = yes

max connections = 4

syslog facility = local5

pid file = /var/run/rsyncd.pid



[ftp]

​        path = /var/ftp/./pub

​        comment = whole ftp area (approx 6.1 GB)



[sambaftp]

​        path = /var/ftp/./pub/samba

​        comment = Samba ftp area (approx 300 MB)



[rsyncftp]

​        path = /var/ftp/./pub/rsync

​        comment = rsync ftp area (approx 6 MB)



[sambawww]

​        path = /public_html/samba

​        comment = Samba WWW pages (approx 240 MB)



[cvs]

​        path = /data/cvs

​        comment = CVS repository (requires authentication)

​        auth users = tridge, susan

​        secrets file = /etc/rsyncd.secrets

\```



\- /etc/rsyncd.secrets文件看起来像这样：

\```

tridge:mypass

susan:herpass

\```



**### version**

This man page is current for version 3.2.3 of rsync.



参考网站：https://download.samba.org/pub/rsync/rsyncd.conf.5.html

man rsyncd.conf