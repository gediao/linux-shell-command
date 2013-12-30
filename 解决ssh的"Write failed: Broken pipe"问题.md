问题场景

服务器环境：Linux CentOS 主机

客户端：Linux CentOS

问题现象

用 ssh 命令连接服务器之后，如果一段时间不操作，再次进入 Terminal 时会有一段时间没有响应，然后就出现错误提示：

    Write failed: Broken pipe

只能重新用 ssh 命令进行连接。这是因为如果有一段时间在SSH连接上无数据传输，连接就会断开。解决此问题有两种方法。

解决方法

方法一：在客户端设置(前提，你的办公本本或者pc 是os 是一个linux)
在客户端电脑上编辑（需要root权限）/etc/ssh/ssh_config，并添加如下一行：

    ServerAliveInterval 60

方法二：在服务器端设置
如果有相应的权限，也可以在服务器端设置，即编辑/etc/ssh/sshd_config，并添加：

    ClientAliveInterval 60


方法三：如果您只想让当前的 ssh 保持连接，可以使用以下的命令：

    $ ssh -o ServerAliveInterval=60 user@sshserver

重启OPENSSH服务器后该项设置会生效。

    sudo /etc/rc.d/init.d/sshd restart 
    sudo /etc/init.d/sshd restart
    etc目录下的init.d是软链接到/rc.d/init.d下的。

每一个连接到此服务器上的客户端都会受其影响。应注意启用该功能后，安全性会有一定下降（比如忘记登出时……）,所以 建议用客户端设置
