## Connect to the MSSQL server

#Attakiing_machine 
Connect to the MSSQL server by issuing the following command with the credentials you got on [[Tab 3]].

```
impacket-mssqlclient ARCHETYPE/sql_svc@<MACHINE IP> -windows-auth
```

![[mssql.png]]

You have a MSSQL connection.

**Next step:** [[Foothold]]

