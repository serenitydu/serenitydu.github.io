### FTP和TFTP
<pre>Date: 2019-11-03 21:11:00            Tag: 网络</pre>

<p>虽然tftp是基于UDP的，ftp是基于tcp的，但是tftp的传输速度远不及tfp。tftp采用的是简单的停止等待协议，发出去的UDP包必须要等待对方的回答或者超时才能开始下一个UDP发送或者重传。而FTP只要对方有ACK表示有win空间就可以持续的发，所以FTP要比TFTP快很多。<p>


