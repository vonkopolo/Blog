
```avatar
"0":
  - Cap.png
image: https:/labs.hackthebox.com/storage/avatars/70ea3357a2d090af11a0953ec8717e90.png
description: " Cap is an easy difficulty Linux machine running an HTTP server that performs administrative functions including performing network captures. Improper controls result in Insecure Direct Object Reference (IDOR) giving access to another user's capture. The capture contains plaintext credentials and can be used to gain foothold. A Linux capability is then leveraged to escalate to root. "
```
# **Enumeration**
-----------------------------------
## Nmap
----------------------------------------------
```nmap 10.10.10.245 -sC -sV -A -p 21,80

PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
80/tcp open  http    gunicorn

```

![[Pasted image 20241209004509.png]]

Running an nmap scan we find 3 open ports

## WEB 
----------------------------------------------
Accessing the web we find a dashboard
![[Pasted image 20241209004730.png]]

We discover changing the number after data gives us access to other users data

![[Pasted image 20241209004959.png]]

We download user 0's pcap file 
![[Pasted image 20241209005255.png]]

## Wireshark
-------------------------
Downloading and analyzing a pcap file we dowloaded from user 0 we find user credentials 
![[Pasted image 20241209005855.png]]

```
name: nathan
password: Buck3tH4TF0RM3!

```

## FTP
----------------------------------------------
Using the credentials we find we are able to gain access to FTP 
![[Pasted image 20241209004325.png]]

After accessing Ftp we find user.txt our first flag

# **Initial Access**
---------------------------------------------
## SSH
-------------------
Using the credentialls we found we are able to access SSH 
![[Pasted image 20241209010327.png]]

#  **Reconnaissance**
---------------------------------------------
## Linpeas
-------
Linpeas reveals how to get root access through pythin3.8
![[Pasted image 20241209012010.png]]

## GtfoBins
-----
Going to https://gtfobins.github.io/gtfobins/python/#capabilities we find how best to abuse this  
![[Pasted image 20241209012741.png]]

# **Privilege Escalation**
---------------------------------------------------
Running the binary we achieve root access
![[Pasted image 20241209012926.png]]
We navigate to /root and we find the root.txt
![[Pasted image 20241209013100.png]]

<center>END!!!!!!!!!!!</centre>