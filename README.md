
<b>SSH over HTTP (Squid)</b>

<li> socat </li>

<pre>socat TCP-L:9999,fork,reuseaddr PROXY:192.168.1.41:127.0.0.1:22,proxyport=3128

ssh john@127.0.0.1 -p 9999</pre>


<li> proxytunnel </li>

<pre>proxytunnel -p 192.168.1.41:3128 -d 127.0.0.1:22 -a 5555

ssh john@127.0.0.1 -p 5555</pre>

<li> proxychains </li>

![proxychains](https://user-images.githubusercontent.com/7115563/33822522-1e15dbee-de58-11e7-9953-3da8ff684cfc.png)

<pre>http 192.168.1.41 3128

proxychains ssh john@127.0.0.1</pre>

<li> corkscrew </li>

![cork](https://user-images.githubusercontent.com/7115563/33822672-b92a51f0-de58-11e7-9936-06056b7903b8.png)

</pre>ssh john@192.168.1.41 -t /bin/sh</pre>
