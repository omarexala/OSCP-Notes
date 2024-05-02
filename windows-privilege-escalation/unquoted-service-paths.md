# Unquoted Service Paths

> When a service is installed, the registry configuration specifies a path to the binary that should be executed on service start.
>
> If the binary is `not encapsulated within quotes`, Windows will attempt to locate the binary in **different folders**.
>
> For example, is the service binary path is `C:\Program Files (x86)\System Explorer\service\SystemExplorerService64.exe`
>
> Then Windows will attempt to run the following executables:
>
> `C:\Program.exe\`
>
> `C:\Program Files (x86)\System.exe`
>
> In these cases, you can put a malicious executable in these directories to escalate privileges



To enumerate all unquoted service paths: `wmic service get name,displayname,pathname,startmode |findstr /i "auto" | findstr /i /v "c:\windows\\" | findstr /i /v """`

After finding an unquoted service path, you can add a malicious executable file in a directory, following what was previously explained