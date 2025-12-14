This a enumeration task. You can use *smblient* to figure out the answer.

#Attakiing_machine
```
smbclient -L //<MACHINE ip>
```

![[smbclient.png]]


## Share

#Attakiing_machine

- Connect to the share and list the files.
```
smbclient //<MACHINE ip>/backups -u ""
smb> dir
```

![[prod.dtsconfig.png]]


- Look at the `prod.disconfig` file content.

![[password.png]]


By reviewing the content of this configuration file, we spot in cleartext the password of the user `sql_svc` , which is `M3g4c0rp123` , for the host `ARCHETYPE` . With the provided credentials we just need a way to connect and authenticate to the MSSQL server.