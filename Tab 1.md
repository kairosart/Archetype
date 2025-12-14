## Which TCP port is hosting a database server?

This a enumeration task. You can use *nmap* to figure out the answer.

#Attakiing_machine
```
nmap -sC -sV <MACHINE ip>
```

![[nmap1.png]]
![[nmap2.png|944x497]]

As you can see:
1. The ms-sql-s port is 1433.
2. SMB ports are open.
	- **TCP 445** → **Main SMB port** (modern Windows / SMB over TCP)
	- **TCP 139** → SMB over **NetBIOS Session Service** (legacy systems)


> [!Note] Answer
> 1433

**Next step:** [[Tab 2]]
