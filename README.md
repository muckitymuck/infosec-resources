
<b>SSH over HTTP (Squid)</b>

<li> socat </li>

<pre>socat TCP-L:9999,fork,reuseaddr PROXY:192.168.1.41:127.0.0.1:22,proxyport=3128

ssh john@127.0.0.1 -p 9999 -t /bin/sh</pre>


