

#Reverse_shell 
1. At this point you can look at the user's privileges.

```
whoami /priv
```

![[privileges.png]]

One of the user's privileges is `SeImpersonatePrivilege`  which is also vulnerable to `juicy potato exploit`. However, you can first check the two existing files where credentials could be possible to be found.

As this is a normal user account as well as a service account, it is worth checking for frequently access files or executed commands. To do that, you will read the `PowerShell history file`, which is the equivalent of `.bash_history` for Linux systems. The file `ConsoleHost_history.txt` can be located in the directory `C:\Users\sql_svc\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\` .

2. Navigate to the folder where the PowerShell history is stored:

```
cd C:\Users\sql_svc\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\
dir 
```

![[consolehos_history.png]]

3. Read the file `ConsoleHost_history.txt`.

```
more ConsoleHost_history.txt
```

![[admin_pass.png]]

You got in clear text the password for the `Administrator` user which is `MEGACORP_4dm1n!!`.

## Shell as the administrator

#Attakiing_machine 
1. Use the tool `psexec.py` again from the Impacket suite to get a shell as the administrator:

```
python3 psexec.py administrator@{MACHINE_IP}
```

![[admin_shell.png]]

2. Go to `C:\Users\Administrator\Desktop`.
3. Read the `root.txt` file.

> [!Note] Root flag
> b91ccec3305e98240082d4474b848528

