# linux

##   What command can tell you if another command is internal / built in or external?

<!-- notecardId: 1758107635778 -->

```console
    cip@DESKTOP-KJIIPF2:~$ type cd
    cd is a shell builtin
```
##   What is an argument?

<!-- notecardId: 1758107635780 -->

A command is split into an array of strings called arguments:
```bash
    ls -la /tmp /var/tmp
    # arg0 = ls
    # arg1 = -la
    # arg2 = /tmp
    # arg3 = /var/tmp
```
##   What is an option?

<!-- notecardId: 1758107635782 -->

An option is a type of argument modifying the behavior of a command :
```bash
    ls -la /tmp /var/tmp
    # option1= -l
    # option2= -a
```
##   How does pushd and popd work?

<!-- notecardId: 1758107635784 -->

pushd adds a new current directory in the stack and switches to it
popd removes last entry from the stack and changes the current directory back

##    How do you coppy a directory?

<!-- notecardId: 1758107635787 -->

```console
cip@DESKTOP-KJIIPF2:~/testcp$ tree
.
├── testcp1
│   └── testcp3
│       ├── tst1
│       ├── tst2
│       └── tst3
└── testcp2

4 directories, 3 files
cip@DESKTOP-KJIIPF2:~/testcp$ cp -r testcp1/testcp3/ testcp2/
cip@DESKTOP-KJIIPF2:~/testcp$ tree
.
├── testcp1
│   └── testcp3
│       ├── tst1
│       ├── tst2
│       └── tst3
└── testcp2
    └── testcp3
        ├── tst1
        ├── tst2
        └── tst3

5 directories, 6 files
```

##   How do you display a long list of files from newest to oldest?

<!-- notecardId: 1758107635789 -->

```bash
    ls -lt
    # -l long list format
    # -t sort by time, newest first
```

##   How do you display a long list of files from oldest to newest?

<!-- notecardId: 1758107635791 -->

```bash
    ls -ltr
    # -l long list format
    # -t sort by time, newest first
    # -r reverse order while sorting
```

##   How do you search man pages for a keyword?

<!-- notecardId: 1758107635794 -->

```console
    cip@DESKTOP-KJIIPF2:~$ apropos cmd
    proc_cmdline (5)     - kernel boot arguments
    proc_pid_cmdline (5) - command line
    openssl-cmds (1ssl)  - OpenSSL application commands
```

##   How do you find out what is the current shell?

<!-- notecardId: 1758107635796 -->

```console
    cip@DESKTOP-KJIIPF2:~$ echo $SHELL
    /bin/bash
```

##   How do you change the current shell?

<!-- notecardId: 1758107635798 -->

```console
    cip@DESKTOP-KJIIPF2:~$ chsh
```

##   How do you create shorter version of a command?

<!-- notecardId: 1758107635801 -->

```bash
    alias dt=date
```

##   How do you create a new environment variable?

<!-- notecardId: 1758107635803 -->

```bash
    export varname=value
```

##   How do you add a path to the $PATH?

<!-- notecardId: 1758107635805 -->

```bash
    export PATH=$PATH:/new/path
```

##   In what file can you set custom user settings?

<!-- notecardId: 1758107635808 -->

```bash
    ~/.profile
```

##   What does the $PS1 variable do?

<!-- notecardId: 1758107635810 -->

tells the terminal what text to display before each command
```console
    cip@DESKTOP-KJIIPF2:~$
```

## How do you list hidden files?

<!-- notecardId: 1758111131313 -->

```bash
    ls -a
    # -a do not ignore entries starting with .
```

## What is the linux kernel?

<!-- notecardId: 1758518931010 -->

A kernel is the core interface between computer hardware and application processes.

## How do you find the kernel version?

<!-- notecardId: 1758518931013 -->

```console
    cip@DESKTOP-KJIIPF2:~$ uname -r
    5.15.133.1-microsoft-standard-WSL2
```
version:
kernel            5.
major             15.
minor             133.
distro-specific   1-microsoft-standard-WSL2

## How is memmory divied in linux?

<!-- notecardId: 1758518931016 -->

between kernel space and user space

## What runs in kernel space?

<!-- notecardId: 1758518931019 -->

kernel code and modules
device drivers

## What runs in user space?

<!-- notecardId: 1758518931022 -->

applications

## How do you find the os version?

<!-- notecardId: 1758518931025 -->

```console
cip@DESKTOP-KJIIPF2:~$ cat /etc/os-release
PRETTY_NAME="Ubuntu 24.04.1 LTS"
NAME="Ubuntu"
VERSION_ID="24.04"
VERSION="24.04.1 LTS (Noble Numbat)"
VERSION_CODENAME=noble
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=noble
LOGO=ubuntu-logo
```

## What does dmesg do?

<!-- notecardId: 1758518931028 -->

the dmesg tool displays messages from the kernel's ring buffer,
boot-time logs that reveal how hardware was detected and configured

## What does udevadm do?

<!-- notecardId: 1758518931031 -->

the udevadm utility is used to query and monitor device events
```console
[~]$ udevadm info --query=path --name=/dev/sda5
/devices/pci0000:00/0000:00:17.0/ata3/host2/target2:0:0/2:0:0:0/block/sda/sda5
```
see info about a specific device

## What does udevadm monitor do?

<!-- notecardId: 1758518931034 -->

monitor kernel uEvents in real time
```console
cip@DESKTOP-KJIIPF2:~$ udevadm monitor
monitor will print the received events for:
UDEV - the event which udev sends out after rule processing
KERNEL - the kernel uevent
```

## What does lspci do?

<!-- notecardId: 1758518931037 -->

lists all PCI devices configured in your system,
such as Ethernet cards, RAID controllers, video cards, and wireless adapters
PCI stands for Peripheral Component Interconnect
representing devices directly attached to the motherboard.

```console
cip@DESKTOP-KJIIPF2:~$ lspci
328f:00:00.0 3D controller: Microsoft Corporation Basic Render Driver
63e9:00:00.0 System peripheral: Red Hat, Inc. Virtio file system (rev 01)
6bb1:00:00.0 SCSI storage controller: Red Hat, Inc. Virtio 1.0 console (rev 01)
```

## What does lsblk do?

<!-- notecardId: 1758518931041 -->
provides detailed information about block devices present on your system
it displays the physical disk (e.g., sda) along with its partitions (e.g., sda1 to sda5)
the term "disk" refers to the entire physical disk
each "partition" is a section of that disk
devices are also linked with major and minor numbers
the major number signifies the device driver type
(for example, the number 8 indicates a block disk device)
minor number distinguishes between individual devices handled by the same driver
```console
cip@DESKTOP-KJIIPF2:~$ lsblk
NAME
    MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
sda   8:0    0 389.8M  1 disk
sdb   8:16   0     2G  0 disk [SWAP]
sdc   8:32   0     1T  0 disk /snap
                              /mnt/wslg/distro
                              /
```

## How do you display cpu info?

<!-- notecardId: 1758518931044 -->

```console
cip@DESKTOP-KJIIPF2:~$ lscpu
Architecture:            x86_64
  CPU op-mode(s):        32-bit, 64-bit
  Address sizes:         39 bits physical, 48 bits virtual
  Byte Order:            Little Endian
CPU(s):                  8
  On-line CPU(s) list:   0-7
Vendor ID:               GenuineIntel
  Model name:            Intel(R) Core(TM) i7-7700K CPU @ 4.20GHz
    CPU family:          6
    Model:               158
    Thread(s) per core:  2
    Core(s) per socket:  4
...
```

## How do you find memory configuration information?

<!-- notecardId: 1758518931046 -->

```console
cip@DESKTOP-KJIIPF2:~$ lsmem
RANGE                                  SIZE  STATE REMOVABLE BLOCK
0x0000000000000000-0x00000000f7ffffff  3.9G online       yes  0-30
0x0000000100000000-0x0000000207ffffff  4.1G online       yes 32-64

Memory block size:       128M
Total online memory:       8G
Total offline memory:      0B
```

## How do you find memory usage statistics in megabites?

<!-- notecardId: 1758518931050 -->

```console
cip@DESKTOP-KJIIPF2:~$ free -m
               total        used        free      shared  buff/cache   available
Mem:            7923         653        6244           3        1272        7270
Swap:           2048           0        2048
```

## How do you find comprehensive details about the system's hardware configuration?

<!-- notecardId: 1758518931053 -->

```console
cip@DESKTOP-KJIIPF2:~$ lshw
WARNING: you should run this program as super-user.
desktop-kjiipf2
    description: Computer
    width: 64 bits
    capabilities: smp vsyscall32
...
```

## What is the linux boot sequence?

<!-- notecardId: 1758521744275 -->

BIOS POST (Power on self test, tests hardware is running ok)
Boot Loader (GRUB2) (allows os selection)
Kernel Initialization (decompresion, load into memory)
Service Initialization (INIT Process) (systemd)

## How do you check what init process is used?

<!-- notecardId: 1758521744278 -->

```console
cip@DESKTOP-KJIIPF2:~$ sudo ls -l /sbin/init
lrwxrwxrwx 1 root root 22 Jun  4 15:24 /sbin/init -> ../lib/systemd/systemd
```

## What does the runlevel command do?

<!-- notecardId: 1758521744282 -->

it determines the current runlevel of a Linux system
```console
cip@DESKTOP-KJIIPF2:~$ runlevel
N 5
```
runlevel 5 provides a graphical interface
runlevel 3 is console mode

## How do you check the current systemd target?

<!-- notecardId: 1758521744284 -->

```console
cip@DESKTOP-KJIIPF2:~$ systemctl get-default
graphical.target
```

## How do you switch systemd from graphical to console mode?

<!-- notecardId: 1758521744287 -->

```console
systemctl set-default multi-user.target
```

## How do you switch systemd from console to graphical mode?

<!-- notecardId: 1758521744291 -->

```console
systemctl set-default graphical.target
```

## What is runlevel called in systemd?

<!-- notecardId: 1758521744294 -->

target

## What are the 3 types of files in linux?

<!-- notecardId: 1758521744297 -->

Regular
Directory
Special
    
## What are the 6 types of special files in linux?

<!-- notecardId: 1758521744301 -->
    Character (serial devices)(mouse, keyboard)
    Block (read/write devices)(ram, hard disk)
    Links
        Hard (asociates multiple filenames with same block of data)
            (deletion will cause loss of data)
        Symbolic (shortcut to another file) (pointer)
            (deletion does not cause loss of data)
    Sockets (ensure communication between different processes)
    Named Pipes (FIFOs) (allow one process to deliver its output directly to another using a unidirectional data flow)

## How do you determine a file type?

<!-- notecardId: 1758521744304 -->

```console
cip@DESKTOP-KJIIPF2:~$ file ./snap
./snap: directory
```

## How do you determine a file type with the ls -l command?

<!-- notecardId: 1758521744306 -->

```console
cip@DESKTOP-KJIIPF2:~$ ls -l
total 4
drwx------ 3 cip cip 4096 Sep 17 14:58 snap
```

We look at the first leter in the command output:
d: Directory
-: Regular file
c: Character device
l: Link (symbolic or hard link)
s: Socket
p: Named pipe
b: Block device

## What is the purpose of /home?

<!-- notecardId: 1758522667320 -->

holds the home directories for all users except the root user
the root user’s home directory is located at /root

## What is the purpose of /opt?

<!-- notecardId: 1758523075485 -->

holds third-party programs

## What is the purpose of /mnt?

<!-- notecardId: 1758522667323 -->

temporarily mounting filesystems

## What is the purpose of /tmp?

<!-- notecardId: 1758522667326 -->

storing temporary data

## What is the purpose of /media?

<!-- notecardId: 1758522667328 -->

it's used for all external media (usb device, etc)

## What is the purpose of /dev?

<!-- notecardId: 1758522667332 -->

contains special block and character device files
(hardware devices such as external hard disks, mice, keyboards, etc)

## What is the purpose of /bin?

<!-- notecardId: 1758522667335 -->

contains essential programs and binaries 
(cp, mv, mkdir, date, etc)

## What is the purpose of /etc?

<!-- notecardId: 1758522667338 -->

stores the majority of Linux configuration files

## What is the purpose of /lib and /lib64?

<!-- notecardId: 1758522667341 -->

to store shared libraries required by programs during runtime

## What is the purpose of /usr?

<!-- notecardId: 1758522667344 -->

stores userland applications and their data

## What is the purpose of /var?

<!-- notecardId: 1758522667347 -->

stores logs and cached data

## How do you find details about the mounted filesystems?

<!-- notecardId: 1758522667350 -->

```console
cip@DESKTOP-KJIIPF2:~$ df -hP
Filesystem      Size  Used Avail Use% Mounted on
none            3.9G  4.0K  3.9G   1% /mnt/wsl
none            232G  172G   60G  75% /usr/lib/wsl/drivers
/dev/sdc       1007G  2.2G  954G   1% /
...
```
-h human readable
-P use the POSIX output format

## What is the package manager for ubuntu/debian?

<!-- notecardId: 1758526136074 -->

DPKG 	 Base package manager 
APT      Front-end 
         (automatically manage and resolve dependencies)
         (interactive use)
APT-GET  command-line front-end
         (stable interface for scripting)

## What is the package manager for redhat/centos?

<!-- notecardId: 1758526136078 -->

RPM     Base package manager
YUM     Front-end (automatically manage and resolve dependencies)
DNF     Feature-rich front-end (yum but better)

## How do you install a package in redhat?

<!-- notecardId: 1758526136081 -->

```bash 
rpm -ivh package.rpm
```

-i: Install the package.
-v: Verbose mode for detailed output.
-h: Display the installation progress.

## How do you uninstall a package with rpm?

<!-- notecardId: 1758527375201 -->

```bash 
rpm -e package
```

## How do you upgrade a package with rpm?

<!-- notecardId: 1758527375204 -->

```bash 
rpm -Uvh package.rpm
```

## How do you query the database for details about installed packages with rpm?

<!-- notecardId: 1758527375207 -->

```bash 
rpm -q package
```

## How do you verify an installed package against its original metadata with rpm?

<!-- notecardId: 1758527375210 -->

```bash 
rpm -Vf path/to/file
```

## Where are yum repo files located?

<!-- notecardId: 1758527375213 -->

```bash
/etc/yum.repos.d
```

## How do you list yum repositories?

<!-- notecardId: 1758527375216 -->

```bash
yum repolist
```

## How do you identify which package provides a specific command e.g. scp?

<!-- notecardId: 1758527375219 -->

```bash
yum provides scp
```

## How do you uninstall a package with yum?

<!-- notecardId: 1758527375223 -->

```bash
yum remove httpd
```

## How do you upgrade a package with yum?

<!-- notecardId: 1758527375225 -->

```bash
yum update telnet
```

## How do you upgrade all packages with yum?

<!-- notecardId: 1758527375228 -->

```bash
yum update
```

## How do you install a package with dpkg?

<!-- notecardId: 1758547405756 -->

```bash 
dpkg -i telnet.deb 
```

## How do you uninstall a package with dpkg?

<!-- notecardId: 1758547405759 -->

```bash 
dpkg -r telnet.deb 
```

## How do you list installed packages with dpkg?

<!-- notecardId: 1758547405761 -->

```console 
cip@DESKTOP-KJIIPF2:~$ dpkg -l
Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not/Inst/Conf-files/Unpacked/halF-conf/Half-inst/trig-aWait/Trig-pend
|/ Err?=(none)/Reinst-required (Status,Err: uppercase=bad)
||/ Name                          Version                                 Architecture Description     
+++-=============================-=======================================-============-===============>ii  adduser                       3.137ubuntu1                            all          add and remove >ii  adwaita-icon-theme            46.0-1                                  all          default icon th>ii  apparmor                      4.0.1really4.0.1-0ubuntu0.24.04.3       amd64        user-space pars>ii  apport                        2.28.1-0ubuntu3.8                       all          automatically g>ii  apport-core-dump-handler      2.28.1-0ubuntu3.8                       all          Kernel core dum>
...
```

## How do you check the status of an installed package with dpkg?

<!-- notecardId: 1758547405764 -->

```bash 
dpkg -s telnet.deb 
```

## How do you install a package with apt?

<!-- notecardId: 1758547405766 -->

```bash 
apt install gimp
```

## What is the location of the repo files for apt?

<!-- notecardId: 1758547405769 -->

```console
/etc/apt/sources.list
```

## How do you refresh the package repository information with apt?

<!-- notecardId: 1758547405771 -->

```console 
cip@DESKTOP-KJIIPF2:~$ sudo apt update
[sudo] password for cip: 
Get:1 http://security.ubuntu.com/ubuntu noble-security InRelease [126 kB]
Hit:2 http://archive.ubuntu.com/ubuntu noble InRelease
Get:3 http://archive.ubuntu.com/ubuntu noble-updates InRelease [126 kB]
...
```

## How do you upgrade installed packages to the latest version?

<!-- notecardId: 1758547405773 -->

```console
cip@DESKTOP-KJIIPF2:~$ sudo apt upgrade
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Calculating upgrade... Done
The following packages were automatically installed and are no longer required:
  libdrm-nouveau2 libdrm-radeon1 libgl1-amber-dri libglapi-mesa libllvm17t64 libxcb-dri2-0
Use 'sudo apt autoremove' to remove them.
The following NEW packages will be installed:
  ethtool libllvm20 mesa-libgallium
The following packages have been kept back:
  libgl1-amber-dri libglapi-mesa
The following packages will be upgraded:
  apparmor apt apt-utils base-files bsdextrautils
...
```

## How do you remove an installed package with apt?

<!-- notecardId: 1758547405776 -->

```bash
apt remove gimp
```

## How do you search for a package in a repository with apt?

<!-- notecardId: 1758547405778 -->

```bash
apt search telnet
```

## How do you check a file or folder size?

<!-- notecardId: 1758547405780 -->

```console
cip@DESKTOP-KJIIPF2:~$ du -sh snap/
28K     snap/
```
or 
```console
cip@DESKTOP-KJIIPF2:~$ ls -lh .
total 4.0K
drwx------ 3 cip cip 4.0K Sep 17 14:58 snap
```

## Create a tar file named test.tar containing files : file1 and file2.

<!-- notecardId: 1758547405783 -->

```bash
tar -cf test.tar file1 file2
```

## List the contents of a tar file.

<!-- notecardId: 1758547405785 -->

```bash
tar -tf test.tar
```

## Extract the contents of a tar file.

<!-- notecardId: 1758547405787 -->

```bash
tar -xf test.tar
```

## Create a compressed tar file with the tar command.

<!-- notecardId: 1758547405790 -->

```bash
tar -zcf test.tar file1 file2
```

## What do bzip2 gzip and xz commands do?

<!-- notecardId: 1758547405792 -->

compress files

## What are the uncompress commands for bz2, gz and xz file formats?

<!-- notecardId: 1758547405795 -->

bunzip2, gunzip, unxz

## Can you read compressed files without uncompressing them, if yes with what tools ?

<!-- notecardId: 1758547405797 -->
yes with zcat, bzcat, xzcat

## How can you search for a file in linux?

<!-- notecardId: 1758547405799 -->

```bash
locate filename
```
or 
```bash
find some/path -name filename.txt
```

## How do you manually update the db for locate command?

<!-- notecardId: 1758547405802 -->

```bash
updatedb
```

## How do you perform a case sensitive search within a file?

<!-- notecardId: 1758558781383 -->

```bash 
grep seccond sample.txt
```

## How do you perform a case insensitive search within a file?

<!-- notecardId: 1758558781386 -->

```bash
grep -i capital sample.txt
```

## How do you perform a search on all files in a directory?

<!-- notecardId: 1758558781388 -->

```bash 
grep -r "some text" /some/folder
```

## How do you find all lines that do not contain a particular string in a file?

<!-- notecardId: 1758558781390 -->

```bash 
grep -v printed sample.txt
```

## How do you find all lines in a file that contain a certain word?

<!-- notecardId: 1758558781393 -->

```bash
grep -w exam examples.txt
```

## How do you find all the lines matching a pattern and the line bellow and above?

<!-- notecardId: 1758558781395 -->

```bash
grep -A1 -B1 Chelsea premier-league-table.txt
```

## How many io stream are there?

<!-- notecardId: 1758559711211 -->

standard 
    input
    output
    error

## How do you redirect the output of a command to a file and overwrite it?

<!-- notecardId: 1758559711214 -->

```bash
echo tst > somefile.txt
```

## How do you redirect the output of a command to a file and append to it?

<!-- notecardId: 1758559711216 -->

```bash
echo tst >> somefile.txt
```

## How do you redirect just the error output of a command to a file?

<!-- notecardId: 1758559711219 -->

```bash
ls /root 2> err.txt
```

## How do you force a command to execute without showing any error message?

<!-- notecardId: 1758559711221 -->

```bash
cat somemissingfile 2> /dev/null
```

## How do you link the output of a command to input of another?

<!-- notecardId: 1758559711224 -->

```bash
echo $SHELL | tee shell.txt
```

## What does the tee command do?

<!-- notecardId: 1758559711226 -->

it reads from standard input to both standard output and files

## What makes tee different than redirect?

<!-- notecardId: 1758559711229 -->

it has one in and two outs, it will read from one source and write to both standard output and a file provided as argument, redirect has only one out it's file or standard output

## How do you switch from command mode to insert mode in vi?

<!-- notecardId: 1758561896115 -->

i

## How do you switch from insert mode to command mode in vi?

<!-- notecardId: 1758561896117 -->

esc

## How do you switch from the insert mode to the last line mode?

<!-- notecardId: 1758561896119 -->

:

## How do you switch from the last line mode to the command mode?

<!-- notecardId: 1758561896122 -->

esc

## How do you coppy and paste a line in command mode in vi?

<!-- notecardId: 1758561896124 -->

move cursor to line
yy 
move to where you want to paste
p

## How do you save a file in vi in command mode?

<!-- notecardId: 1758561896126 -->

ZZ

## How do you delete a letter in vi in command mode?

<!-- notecardId: 1758561896128 -->

move cursor to intended location
x

## How do you delete a line in vi in command mode?

<!-- notecardId: 1758561896131 -->

move cursor to line
dd

## How do you delete 3 lines from current line in vi in command mode?

<!-- notecardId: 1758561896133 -->

d3d

## How do you undo a change in vi in command mode?

<!-- notecardId: 1758561896136 -->

u

## How do you redo a change in vi in command mode?

<!-- notecardId: 1758561896138 -->

ctrl + r

## How do you search for a string in vi in command mode?

<!-- notecardId: 1758561896140 -->

/sometexttosearch
will search from cursor down
to find next occurence press n
to find previous occurence press N
or 
?sometexttosearch
will search from the cursor up
to find next occurence press n
to find previous occurence press N

## How do you save and exit from last line mode in vi?

<!-- notecardId: 1758561896143 -->

:wq

## How do you quit without saving from last line mode in vi?

<!-- notecardId: 1758561896146 -->

:q!

## What does the /etc/hosts file contain?

hostname-to-IP mappings for that system
the system does not verify whether the system's actual hostname 
matches the alias you defined

## What is the default priority between /etc/hosts and dns?

/etc/hosts takes precedence over dns by default
this can be changed in /etc/nsswitch.conf with config bellow
    hosts:     dns files

## What doest the /etc/resolv.conf file contain?

dns ip, ex:
```console
nameserver 8.8.8.8
```

search domain name
```console
search mycompany.com
```
when using a short hostname (web), the system will sequentially append each search domain until a valid match is found (web.mycompany.com)

## What are the most common DNS record types?

A       map hostnames to IPv4 addresses
```console
web-server  192.168.1.1
```
AAAA    map hostnames to IPv6 addresses
```console
web-server  2001:0db8:85a3:0000:0000:8a2e:0370:7334
```
CNAME   create an alias that maps one hostname to another
        this is useful when a service is accessible by multiple names
```console
food.web-server  eat.web-server,hungry.web-server
```

## What command can you use to query your dns server?

```console
cip@DESKTOP-KJIIPF2:~$ nslookup www.google.com
;; Got recursion not available from 172.26.144.1
Server:         172.26.144.1
Address:        172.26.144.1#53

Non-authoritative answer:
Name:   www.google.com
Address: 142.250.185.68
;; Got recursion not available from 172.26.144.1
Name:   www.google.com
Address: 2a00:1450:4001:80e::2004
```

## What other command besides nslookup can be used for dns query?

```console
cip@DESKTOP-KJIIPF2:~$ dig www.google.com

; <<>> DiG 9.18.39-0ubuntu0.24.04.1-Ubuntu <<>> www.google.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 42776
;; flags: qr rd ad; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0
;; WARNING: recursion requested but not available

;; QUESTION SECTION:
;www.google.com.                        IN      A

;; ANSWER SECTION:
www.google.com.         0       IN      A       142.250.185.68

;; Query time: 0 msec
;; SERVER: 172.26.144.1#53(172.26.144.1) (UDP)
;; WHEN: Fri Sep 26 10:24:46 EEST 2025
;; MSG SIZE  rcvd: 62
```