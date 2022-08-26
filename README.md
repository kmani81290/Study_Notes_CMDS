https://raw.githubusercontent.com/kmani81290/Study_Notes_CMDS/main/README.md
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++

what is inode value
An inode is an internal data structure that Linux uses to store information about a filesystem object. 
The inode count equals the total number of files and directories in a user account or on a disk. 
Each file or directory adds 1 to the inode count.

What is the use of Hardlink?
With a hard link, the link points to the inode directly. With a symbolic link, the link points to the object (which then in-turn points to the inode). Hard links are a way of bypassing the middle-man, it's like creating a copy of the original file, while only using the disk space of one file.

What is Softlink used for?
In computing, a symbolic link (also symlink or soft link) is a term for any file that contains a reference to another file or directory in the form of an absolute or relative path and that affects pathname resolution.
 Eg:-   Create hard link between sfile1file and link1file, run: ln sfile1file link1file
    To make symbolic links instead of hard links, use: ln -s source link
    To verify soft or hard links on Linux, run: ls -l source link

create an Network Bonding (NIC teaming) using nmcli
Mode 	Policy 	How it works 	Fault Tolerance 	Load balancing
0 	Round Robin 	packets are sequentially transmitted/received through each interfaces one by one. 	Yes 	Yes
1 	Active Backup 	one NIC active while another NIC is asleep. If the active NIC goes down, another NIC becomes active. only supported in x86 environments. 	Yes 	No
2 	XOR [exclusive OR] 	In this mode the, the MAC address of the slave NIC is matched up against the incoming request’s MAC and once this connection is established same NIC is used to transmit/receive for the destination MAC. 	Yes 	Yes
3 	Broadcast 	All transmissions are sent on all slaves 	Yes 	No
4 	Dynamic Link Aggregation 	aggregated NICs act as one NIC which results in a higher throughput, but also provides failover in the case that a NIC fails. Dynamic Link Aggregation requires a switch that supports IEEE 802.3ad. 	Yes 	Yes
5 	Transmit Load Balancing (TLB) 	The outgoing traffic is distributed depending on the current load on each slave interface. Incoming traffic is received by the current slave. If the receiving slave fails, another slave takes over the MAC address of the failed slave. 	Yes 	Yes
6 	Adaptive Load Balancing (ALB) 	Unlike Dynamic Link Aggregation, Adaptive Load Balancing does not require any particular switch configuration. Adaptive Load Balancing is only supported in x86 environments. The receiving packets are load balanced through ARP negotiation.
# nmcli connection 
# nmcli con add type bond con-name bond0 ifname bond0 mode active-backup ip4 192.168.219.150/24
# cat /etc/sysconfig/network-scripts/ifcfg-bond0
# ip addr show bond0
Creating slave interfaces
# nmcli con add type bond-slave ifname ens33 master bond0

what is cluster in linux
A high availability Linux cluster is a group of Linux computers or nodes, storage devices that work together and are managed as a single system. In a traditional clustering configuration, two nodes are connected to shared storage (typically a SAN).

--------------RAID 0
In a RAID 0 system, data are split up into blocks that get written across all the drives in the array. By using multiple disks (at least 2) at the same time, this offers fast read and write speeds. All storage capacity can be fully used with no overhead. The downside to RAID 0 is that it is NOT redundant, the loss of any individual disk will cause complete data loss. Thus, it is not recommended to use unless the data has no value to you.
---------------RAID 1
RAID 1 is a setup of at least two drives that contain the exact same data. If a drive fails, the others will still work. It is recommended for those who need high reliability. An additional benefit of RAID 1 is the high read performance, as data can be read off any of the drives in the array. However, since the data needs to be written to all the drives in the array, the write speed is slower than a RAID 0 array. Also, only capacity of a single drive is available to you.
yum install mdadm	
mdadm -E /dev/sd[b-c]				-- checking
fdisk /dev/sdb
# mdadm --create /dev/md0 --level=mirror --raid-devices=2 /dev/sd[b-c]1
# cat /proc/mdstat
# mdadm -E /dev/sd[b-c]1
# mdadm --detail /dev/md0      --status checking
# mkfs.ext4 /dev/md0			--make file system
# mkdir /mnt/raid1
# mount /dev/md0 /mnt/raid1/
# touch /mnt/raid1/tecmint.txt
# echo "tecmint raid setups" > /mnt/raid1/tecmint.txt			--test
------------------RAID 5
RAID 5 requires the use of at least 3 drives, striping the data across multiple drives like RAID 0, but also has a “parity” distributed across the drives. In the event of a single drive failure, data is pieced together using the parity information stored on the other drives. There is zero downtime. Read speed is very fast but write speed is somewhat slower due to the parity that has to be calculated. It is ideal for file and application servers that have a limited number of data drives.

How to Create and Setup LUNs using LVM in “iSCSI Target Server” on RHEL/CentOS/Fedora – Part II
Why LUNS are Used?
LUNS used for storage purpose, SAN Storage’s are build with mostly Groups of LUNS to become a pool, LUNs are Chunks of a Physical disk from target server. We can use LUNS as our systems Physical Disk to install Operating systems, LUNS are used in Clusters, Virtual servers, SAN etc. The main purpose of Using LUNS in Virtual servers for OS storage purpose. LUNS performance and reliability will be according to which kind of disk we using while creating a Target storage server.
fdisk -l /dev/sda




Interview questions-

Link pathing,   clusterin,  nic bonding, 
Jboss 
Nagios
Rsync file sharing
Ftp and samba diff
Lamp troubleshoots,  php file 
Engines aws
Docker usage 
User files storing location
Jira port number 
Nagios configuration and how to  add services php and monitor
Monitoring tools
Backup methods for an cleint environment
Middleware tools 
Squid proxy
Web admin conrf qnd port
Samba congi test
Nfs ip arddres /etc/exports
Dns  
Haproxy load balancing
Scpk
Samba backup 
Lvm backup
Jboss dump questions
Find 
hardenning
grub issue
kernel issue
yum repository

Crak paswd

https://www.rootusers.com/how-to-reset-root-user-password-in-centos-rhel-7/




Peepare for linux interview

Interview questiins

How to check user login expiry - #chage -l
Raid differences
Kernel panic
Cr procedures
Added lun how to add into the servers commands 
How to format disk
Add lvm

Lisf top files

https://www.google.co.in/amp/s/www.tecmint.com/find-top-large-directories-and-files-sizes-in-linux/amp/

How to remove 7 days older file: creating cron job for run every day night
https://www.udemy.com/course/linux-technical-interview-questions-and-answers/



http://linuxsay.com/t/welcome-introduce-yourself-here/1740

Rhcsa quest

https://insidegnulinux.blogspot.com/2016/11/rhel-7-rhcsa-exam-questions-and-answers.html?m=1

Iscsi
https://insidegnulinux.blogspot.com/2016/10/deep-dive-into-iscsi.html?m=1


########## TCS  ############

Cmd

Subcription-msnager list
Export http_proxy=threstpulse


Pe prod checklist
Windows

Activatijn check
Slmgr /xpr
Slui 3      give activation code
Diskmgmt.msc

Ntp sync
W32tm /query /status


System properties  /advanced / bsck groung services
Performance option 

Windows defender

Winfows  conf fownlosd

Cscript.exe wintel_sysconfig

Tzutil /g


NFS
-----

Port No: 2049
Conf File : /etc/exports
/home 10.0.0.0/24(rw,sync,no_root_squash,no_all_squash) 
# *note
/home ⇒ shared directory
10.0.0.0/24 ⇒ range of networks NFS permits accesses
rw ⇒ writable
sync ⇒ synchronize
no_root_squash ⇒ enable root privilege
no_all_squash ⇒ enable users' authority

/etc/sysconfig/nfs -  is the file through which we can fix ports
for RQUOTAD_PORT, MOUNTD_PORT, LOCKD_TCPPORT,
LOCKD_UDPPORT and STATD_PORT

List available nfs share on Client machine :
showmount -e serverip 
mount 192.168.0.104:/home/lokesh /mnt


1. NFSSTAT
Displays the statistics about NFS clinet and NFS server activity.

2. Purpose of NFS
NFS can be used for sharing of files remotely. Data can be stored on a single machine and still remain accessible to others over the network.  Reduction of the number of removable media drive throughout the network since they can shared.

3. What is Autofs and its advantages?
Autofs is auto mounting file system on demand like when ever you need it. 
NFS is like mounting a complete partition remotely and you will have availibility of whole content of the partition.
But there are few advantages with autofs over nfs.

4. Advantages of AutoFS:
shares are accessed automatically and transparently when a user tries to access any files or directories under the designated mount point of the remote filesystem to be mounted.
Booting time is significantly reduced because no mounting is done at boot time.
Network access and efficiency are improved by reducing the number of permanently active mount points.
Failed mount requests can be reduced by designatin alternate servers as the source of a filesystem.

5. What is the Default permission applied on the user when you mount a nfs permission on any local directory in your system?
No user permissin which is a system account in all the machines having normal user level privileges unless no_root_squash or any other permission specification is not provided on the share.

6. What is the Difference Between Nfs Share And A Samba Share?
NFS sharing is done between linux to linux where samba sharing can be done between Linux - Linux and Linux - windows.

7. What is Hard and Soft Mount of NFS?
In Hard Mount:
If the NFS file system i hard mounted, the NFS daemons will try repeatedly to contact the server. The NFS daemon retries will not time out will affect system performance and you cannot interrupt them
If you just mount a file system without specifying hard or soft, the default is a hard mount. Hard mounts are preferable because of the stateless nature of NFS.
If a client sends an I/O request to the server (such as an ls -la), and the server gets rebooted, in client machine the process will keep on running. This preserves data transfers in the event of a server failure.
In SOFT Mount:
A soft mount allows the client to stop trying an operation after a period of time. If the NFS server goes down at the time of data trasfer, it will alert and the process will do down.This may cause the data corruption.
A soft link will return with an error and fail. You should only use soft mounts in the cases where client reponsiveness is more important than data integrity. in another word soft mount will allow automatically unmount if the filesystem is idle for a specified time period.

8. i am unable to mount a NFS Share. How will you trace out the reason.
Firstly, check that you have permission to mount nfs share or not. Check /etc/exports file.
Secondly you can get RPC error: Program not Registered (or another "RPC" error)
For this check your NFS server and portmap service running or not by "rpcinfo -p"

9. What is the role of "all _squash" option?
Treat all cleint users as anonymous users. Map all user 	and group 	IDs to the  	anonymous user and group ID.

10. Why to use NFS?
A Network File system (NFS) allows remote machine to mount file systems over a network and interact with those file systems as thougj they are mounted locally. This enables system administrators to consolidate resources onto centralized servers over the network.

11. Default PORT Number for NFS : 2049

12. What are Different options used in /etc/exports File?
Below are list of options used in /etc/exports

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++
RWX
------

1.  Manual Packagement Management Configuration

mount /dev/cdrom /mnt
cp /mnt/* /var/ftp/pub -rvf
createrepo -v /var/ftp/pub
vi /etc/yum.repos.d/server1.repo
[server]
name=server1
Baseurl=file:///var/ftp/pub
gpgcheck=0
enabled=1
yum list all 
yum repolist
yum install  createrepo.  Manual Packagement Management Configuration

mount /dev/cdrom /mnt
cp /mnt/* /var/ftp/pub -rvf
createrepo -v /var/ftp/pub
vi /etc/yum.repos.d/server1.repo
[server]
name=server1
Baseurl=file:///var/ftp/pub
gpgcheck=0
enabled=1
yum list all 
yum repolist
yum install  createrepo
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++
2. Samba configuratio
--------------------------
samba port no :-
137 - netbios-ns  - Used for naming service
138 - datagram
139 - session service
445 - microsoft active directory

Configuration file : /etc/samba/smb.conf
[lokesh]
comment=lokesh documents
Path=/home/lokesh
Valid Users=lokesh
public=no
writable=yes
printable=no
create mask=0777

Packages : samba, samba-utils, smbclient
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++
collected questions
------------------------
link pathing
clustering 

Ricci is a daemon which used for cluster management and configurations. It distributes/dispatches receiving messages to the nodes configured.
Luci is a server that runs on the cluster management server and communicates with other multiple nodes. It provides a web interface to make things easier.
Mod_cluster is a load balancer utility based on httpd services and here it is used to communicate the incoming requests with the underlying nodes.
CCS is used to create and modify the cluster configuration on remote nodes through ricci. It is also used to start and stop the cluster services.
CMAN is one of the primary utilities other than ricci and luci for this particular setup, since this acts as the cluster manager. Actually, cman stands for CLUSTER MANAGER. It is a high-availability add-on for RedHat which is distributed among the nodes in the cluster.

ccs -h 172.16.1.250 --createcluster tecmint_cluster
ccs -h 172.16.1.250 --addnode 172.16.1.222
ccs –h 172.16.1.250 --lsnodes


nic bonding
 vi /etc/sysconfig/network-scripts/ifcfg-bond0
 
jboss

nagios
rsync file sharingftp and samba diff
lamp troubleshoots, php fileengines aws
docker usage
user file storing location
jira port no 8080
nagios configuration and howe to add services [hp and monitor
monitoring tools
backup method for an client environment
middleware toolss
squid proxy
web admin conf qnd port
samba confi test
nfs ip address 
dns
haproxy load balancing
scpk
samba backuplvm backup
jboss dumb questionsfind
hardening
grub issue
kernel; issue
yum repo
crak pasword
how to check user login expiru  chage -laraid difference
kernel panic
cr procedures
add lun how to add into tjhe servers commands'
how to format disk
add lvm

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++
LVM 
-----
Recover Deleted LVM in Linux.

fdisk -l
fdisk /dev/sdb
n
t -> type 8e (LVM)
w
partprobe /dev/sdb
pvcreate /dev/sdb1
vgreate vg0 /dev/sdb1
lvcreate -n lv0 -L 2G vg0
mkfs.xfs /dev/vg0/lv0
mkdir /lv1
mount /dev/vg0/lv0 /lv1
cd /lv1
touch test{1..20}.txt
vi test17.txt
test files
vi test20.txt
data files
umount /lv1
lvremove /dev/vg0/lv0
ls -ltr /etc/lvm/archieve
vgcfgrestore --list vg0
vgcfgrestore -f /etc/lvm/archieve/vg0_0002_3840085.vg0 vg0
lvscan  --- it will inactive
lvchange -ay /dev/vgo/lv0   --> activating cmd
mount /dev/vg0/lv0 /lv1

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++
fstab entries
---------------
cat 
/etc/fstab
/dev/mapper/rhel-root/	xfs	defaults	0 0

1. /dev/devicename - Block device path of NFS path (servername /IP:nfssharepath)
2./ - Mount point
3. xfs - file system
4. defaults - Mount options
5. 0 - zero means excluded from backup. non zero dump program enabled device will be backep
6. 0 - FSCK check. if value is 0 excluded to check FSCK on boot, Non- zero value 2 partition will be checked by fsck

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++
what is sticky bit?  how it will be useful explain with example?
chmod +t /dir
when run this folder any one its run belongs to the owner
no permission to delete some other user
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++
How to provide access to single file to multiple users and groups with customized permission?
Using ACl - Access Control List you can provide access to directory/file for multiple users and groups
setfacl -m -u:ravi:rw filename
setfacl -m g:group1:r filename
getfacl test1 
file: test1
owner: root
group: root
user::rwx
user:ravi:rw-
group::rwx
mask::rwx
other::---
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++
--incomplete

HA Cluster Configuration in RHEL 8 (CentOS 8):
High Availability cluster, also known as failover clustr active-passive cluster, is one of the most widely used cluster types in a production environment to have conti,
In technical, if the server running application has failed for some reason (ex: hardware failure), cluster software (pacemaker) will restart the application on the working
Failover is not just restarting an application; it is a series of operations associated with it, like mounting filesystems, configuring networks, and starting dependent ap
Environment:
Here, we will configure a failover cluster with Pacemaker to make the Apache (web) server as a highly available application.
Here, we will configure the Apache web server, filesystem, and networks as resources for our cluster.
For a filesystem resource, we would be using shared storage coming from iSCSI storage.

[rootstorage .]# dnf install -y targetcli lvm2 iscsi-initiator-utils lvm2
Let’s list the available disks in the iSCSI server using the below command.
[rootstorage .]# fdisk -l I grep -i sd
Here, we will create an LVM on the iSCSI server to use as shared storage for our cluster nodes.
[rootstor’age ...]# pvcreate /dev/sdb
[rootstorage ...]# vgcreate vg_iscsi /dev/sdb
[rootstorage .]# lvcreate -l løø%FREE -n lv_iscsi vg_iscsi

https://www.youtube.com/watch?v=ayPLYjGZ19Y

--incomplete

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++
ISCSI
------

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++
Booting Process
-------------------
POST
BIOS
MBR
GRUB
KERNAL
INIT
SYSTEMD
TARGET

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++
GRUB ISSUE FIX
--------------------
Insert live cd and reboot 
enter troubleshooting => rescue mode
continue
chroot /mnt/sysimage
grub2-install /dev/sda
grub2-mkconfig -o /boo/grub2/grub.cfg

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++
apache configuration
yum install httpd

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++
how to disable the ipv6
net.ipv6.conf.all.disable_ipv6 = 1

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++
where you place dns entry
/etc/resolve.conf
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
																				DOCKER
																			!!!!!!!!!!!!!!!!!!!!!!
Docker file --> Docker Image--> Docker container--->Docker Image-->Docker File
Dockerfile -->Build-->Docker Image-->Dcoker Container-->

docker pull httpd
docker start -itd --name httpdcon1 -p "8090:80" httpd
docker start container-id
docker exec -it con-id /bin/bash --> to go container
when apache container path for html file
/usr/local/apache2/htdocs/index.html

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++
docker volumes
-------------------
docker run -itd --name web1 -p "8080:80" -v "D:\Docker\mylogs:/usr/local/apache2/htdocs" httpd
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++
docker python installation
--------------------------------
mkdir pythdir
cd pythdir
echo "FROM ubuntu:18.04" >> Dockerfile
echo "ENV TZ=Europe/Kiev" >> Dockerfile
echo "RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone" >> Dockerfile
echo "RUN apt update && apt install -y python-pip python-dev ssh python-boto3" >> Dockerfile
echo "RUN pip install ansible==2.4.3.0" >> Dockerfile
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++
Docker Sync
---------------
docker run -itd --name webserver -p "8080:80" -v "/root/mysql:/usr/local/apache2/htdocs" httpd
Notes:- we can modify index file from base machine it will refflect on the container

docker desktop iniatial configuration
-----------------------------------------

clone

docker run --name repo alpine/git clone \ https://github.com/docker/getting-started.git
docker cp repo:/git/getting-started/ .

Build 
cd getting-starteddocker build -t docker101tutorial .
docker build -t docker101tutorial .

Run
docker run -d -p 80:80 \ --name docker-tutorial docker101tutorial

Share

---------------------------------------------------------
Docker session greens tech
Devops - Docker containerization - Deployment Tool
---------------------------------------------------
login to container
docker exec -it 1hfyuop45 /bin/bash
 
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
																	GITHUB ACTIONS
																	!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
how to push files windows to github repo

git config --global user.email "kmani81290@gmail.com"
git config --global user.name "kmani81290"
git init
git remote add origin https://github.com/kmani81290/Study_Notes_CMDS.git
git remote -v
git add .
git commit -m "First Commit"
git push origin master    

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++
github action

1) Listen to Event
pr created
cont joined
other apps issue createdpr merged

2) trigger workflow
sort --> action


label--> action
assign it-->action
reproduce --> action

why is the setup easier?
integration with other technoligies is important

pipeline=> nodejs app / build docker image/ push to nexus repo / deploy digital ocean server /java app with maven / int test linux and win / build docker / push to aws repo

=> integration with other technoligiesis imp!
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++
CI/CD Demo

java app with gradle - build docker image - push to private repo

What are github actions?
A tool that lets you automate your software development workflows.
You can write individual tasks, called actions and combine them to create a custom workflow.

What are the workflows?
Workflows are custom automated process that you can set up in your repository to build, test, package, release, or deploy any code project on github.

Eg:-                                                                                   workflow
Github Repository -> push                                                        github server
											pull request (opened mered)  -->job - virtual machine instance, linux, wind, mac 
											issue -created, closed, ...                             with tools installed or docker container
											schedule (every 6pm)                                 step1,2-action, step3,4-cmd
											external event                                      job -   ,,   ,, 

Notes:- we can do a test code first then it will start android and mac application will start thats possible	in Github Actions

Github hosted runners
Linux, windows virtual environments with commonly used pre-installed software.

self hosted runners
-A machine you manage and maintain with the runer app installed
-You have more control of hardware, Oprating system, and software tools than Github-hosted runners provide.
-Ideal if you need to control hardware, ex. add more memory for larger jobs or choose and operating system not offered by github-hosted runners.

+++++++++++++++++++++++++++++++++++++++++++++++++++++++
Build-> Test -> Merge --------->Automatically release to repository->auto deploy to production
Continuos Integration						Continour Delivery

simple githuhub action 
--------------------------
1. Create new repository with newfile
2. create new file under repository /mygithubaction/.github/workflows/superlinter.yml
3. copy paste below code

name: super-linter

on: push

 jobs:
     super-lint:
	     name: Lint code base
		 runs-on: ubuntu-latest
		 steps:pp
		     - name: Checkout Code
			    uses: actions/checkout@v2
				
			 - name: Run Super-Linter
			    uses: github/super-linter@v3
				env:
				    DEFAULT_BRANCH: main
					GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}













