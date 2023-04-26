---
title: "Linux Cheat Sheet — DevOps"
seoTitle: "Linux Cheat Sheet — DevOps"
seoDescription: "Linux Cheat Sheet — DevOps"
datePublished: Sat Apr 22 2023 14:32:27 GMT+0000 (Coordinated Universal Time)
cuid: clgs2xoqa000509l75cbqgosg
slug: linux-cheat-sheet-devops
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1682173829982/c65f9374-503d-4914-91aa-649b142d082b.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1682173914994/f3dc3bd8-1f91-48a1-b815-d6879b18727a.jpeg
tags: support, linux, community, devops, cheatsheet

---

Here are some important linux commands you must know !

💠 ***System/OS related commands.***

**#uname** -Displays Linux system information

**#uname** **\-r** -Displays kernel release information

**#uptime** -Displays how long the system has been running

**#hostname** -Shows the system hostname

**#hostname** -iDisplays the IP address of the system

**#last reboot** -Shows system reboot history

**#date** -Displays current system date and time

**#whoami** -Displays who you are logged in as

**#finger username** -Displays information about the user

💠 ***Hardware Based Command***

**#lshw -**Displays information about system’s hardware configuration

**#lsblk** -Displays block devices related information

**#free -m** -Displays free and used memory in the system (-m indicates memory in MB)

💠 ***Users Management Commands***

**#id** -Displays the details of the active user e.g. uid, gid, and groups

**#last** -Shows the last logins in the system

**#who** -Shows who is logged in to the system

**#groupadd “dev”** -Adds the group ‘dev’

**#adduser** - “dipraj”Adds user ‘dipraj’

**#userdel** - “dipraj”Deletes user ‘dipraj’

**#usermod** -Used for modifying user information

💠 ***File Commands***

**#ls -al** -Lists files — both regular & hidden files and their permissions

**#pwd** -Displays the present working directory path

**#mkdir** - ‘test’Creates a new directory named ‘test’

**#rm file\_name** -Removes a file

**#rm -f filename -**Forcefully removes a file

**#rm -r directory\_name -**Removes a directory recursively

**#rm -rf directory\_name -**Removes a directory forcefully and recursively

**#cp file1 file2** -Copies the contents of file1 to file2

**#cp -r dir1 dir2 -**Recursively Copies dir1 to dir2. dir2 is created if it does not exist

**#mv -** file1 file2Renames file1 to file2

**#ln -s /path/to/file\_name link\_name -**Creates a symbolic link to file\_name

**#touch file\_name** -Creates a new file

**#cat &gt; file\_name -**Places standard input into a file

**#more file\_name** -Outputs the contents of a file

**#head file\_name -**Displays the first 10 lines of a file

**#tail -20 file\_name** -Displays the last 20 lines of a file

**#gpg -c file\_name -**Encrypts a file

**#gpg file\_name.gpg -**Decrypts a file

**#wc -**Prints the number of bytes, words and lines in a file

**#xargs** -Executes commands from standard input

💠 ***Process Related Commands***

**#ps** -Display currently active processes

**#ps aux | grep ‘telnet’ -**Searches for the id of the process ‘telnet’

**#pmap -**Displays memory map of processes

**#top -** Displays all running processes

**#kill pid no** -Terminates process with a given pid

**#killall proc -**Kills / Terminates all processes named proc

**#pkill process-name** -Sends a signal to a process with its name

**#bg -**Resumes suspended jobs in the background

**#fg -**Brings suspended jobs to the foreground

**#lsof -**Lists files that are open by processes

💠 ***File Permission Commands***

**chmod octal filename -**Change file permissions of the file to octal

*Example -*

**#chmod 777 peep.txt** - Set rwx permissions to owner, group and everyone

**#chmod 755 peep.txt** -Set rwx to the owner and r\_x to group and everyone

**#chmod 766 peep.txt -** Sets rwx for owner, rw for group and everyone

**#chown owner user-file -**Change ownership of the file

**#chown owner-user:owner-group file\_name -**Change owner and group owner of the file

**#chown owner-user:owner-group directory -**Change owner and group owner of the directory

![](https://cdn-images-1.medium.com/max/1200/1*Pt81aUdcz-SH8J4GCNmwgQ.jpeg align="left")

File permission — DevOps

💠 ***Network Commands***

**#ip addr show -** Displays IP addresses and all the network interfaces

**#ip address add 192.160.0.1/24 dev eth0** -Assigns IP address 192.168.0.1 to interface eth0

**#ifconfig** -Displays IP addresses of all network interfaces

**#ping host** -Ping command sends an ICMP echo request to establish a connection to server

**#whois domain** -Retrieves more information about a domain name

**#dig domain** -Retrieves DNS information about the domain

**#host** [**google.com**](http://google.com) **-** Performs an IP lookup for the domain name

**#hostname -i** Displays local IP address

**#wget file\_name** -Downloads a file from an online source

**#netstat -pnltu** -Displays all active listening port

💠 Compression/Archives Commands

**#tar -cf peep.tar peep&lt;:code&gt; -**Creates archive file called ‘peep.tar’ from file ‘peep’

**#tar -xf peep.tar** -Extract archive file ‘peep.tar’

**#tar -zcvf peep.tar.gz source-folder** -Creates gzipped tar archive file from the source folder

**#gzip file** -Compression a file with .gz extension

💠 Install Packages Commands

**#rpm -i pkg\_name.rpm -** Install an rpm package

**#rpm -e pkg\_name** -Removes an rpm package

**#dnf install pkg\_name -**Install package using dnf utility

💠 Search Commands

**#grep ‘pattern’ files -**Search for a given pattern in files

**#grep -r pattern dir** -Search recursively for a pattern in a given directory

**#locate file** -Find all instances of the file

**#find /home/ -name “index”** -Find file names that begin with ‘index’ in /home folder

**#find /home -size +10000k -**Find files greater than 10000k in the home folder

💠 File Transfer Commands

**#scp file1.txt server2/tmp -**Securely copy file1.txt to server2 in /tmp directory

**#rsync -a /home/apps /backup/** -Synchronize contents in /home/apps directory with /backup directory

💠 Disk Usage Commands

**#df -h** -Displays free space on mounted systems

**#df -i** -Displays free inodes on filesystems

**#fdisk -l** -Shows disk partitions, sizes, and types

**#du -sh** -Displays disk usage in the current directory in a human-readable format

**#findmnt** -Displays target mount point for all filesystems

**#mount device-path mount-point -**Mount a device

💠 Directory Traverse Commands

**#cd ..** Move up one level in the directory tree structure

**#cd** Change directory to $HOME directory

*Thanks for reading*💫  
If you enjoyed this article share it with your friends and colleagues. Let me know your thoughts in the comments section, and don’t forget to clap.

Follow me for more tech blogs.

[LinkedIn](https://www.linkedin.com/in/diprajghosh/) | [Instagram](https://www.instagram.com/dipraj_ghosh/) | [Facebook](https://www.facebook.com/diprajriki/)

\-Dipraj ✨