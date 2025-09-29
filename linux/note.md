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

<!-- notecardId: 1758873072759 -->

hostname-to-IP mappings for that system
the system does not verify whether the system's actual hostname 
matches the alias you defined

## What is the default priority between /etc/hosts and dns?

<!-- notecardId: 1758873072762 -->

/etc/hosts takes precedence over dns by default
this can be changed in /etc/nsswitch.conf with config bellow
    hosts:     dns files

## What doest the /etc/resolv.conf file contain?

<!-- notecardId: 1758873072765 -->

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

<!-- notecardId: 1758873072768 -->

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

<!-- notecardId: 1758873072770 -->

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

<!-- notecardId: 1758873072773 -->

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

## How do you inspect a host's interfaces?

<!-- notecardId: 1758873072775 -->

```console
cip@DESKTOP-KJIIPF2:~$ ip link
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group 
default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP mode DEFAULT group default qlen 1000
    link/ether 00:15:5d:12:18:e6 brd ff:ff:ff:ff:ff:ff
```

## How do you view or assign ip adresses to interfaces?

<!-- notecardId: 1758890591091 -->

view
```console
cip@DESKTOP-KJIIPF2:~$ ip addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 
1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 00:15:5d:12:18:e6 brd ff:ff:ff:ff:ff:ff
    inet 172.26.149.45/20 brd 172.26.159.255 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::215:5dff:fe12:18e6/64 scope link
       valid_lft forever preferred_lft forever
```

assign
```bash
ip addr add 192.168.1.10/24 dev eth0
```

## How do you view the kernel's routing table?

<!-- notecardId: 1758890591094 -->

```console
cip@DESKTOP-KJIIPF2:~$ route
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
default         DESKTOP-KJIIPF2 0.0.0.0         UG    0      0        0 eth0 
172.26.144.0    0.0.0.0         255.255.240.0   U     0      0        0 eth0 
```

## How do you configure a default gateway (192.168.2.1)?

<!-- notecardId: 1758890591098 -->

```bash
ip route add default via 192.168.2.1
```

## How do you configure a specific route for network 192.168.1.0 using gateway 192.168.2.1?

<!-- notecardId: 1758890591101 -->

```bash
ip route add 192.168.1.0/24 via 192.168.2.1
```

## What can be used interchangeably with the word default in most networking commands?

<!-- notecardId: 1758890591103 -->

0.0.0.0

## How do you change the state of network interface eth0 to up?

<!-- notecardId: 1758890591106 -->

```bash 
sudo ifconfig eth0 up
```

## Where is the file containing information about a user account?

<!-- notecardId: 1758890591108 -->

```console
/etc/passwd
```

## Where is the file containing information about user groups?

<!-- notecardId: 1758890591110 -->

```console
/etc/group
```

## What command can provide user details?

<!-- notecardId: 1758890591113 -->

```console
cip@DESKTOP-KJIIPF2:~$ id cip
uid=1000(cip) gid=1000(cip) groups=1000(cip),4(adm),20(dialout),24(cdrom),25(floppy),27(sudo),29(audio),30(dip),44(video),46(plugdev),100(users),107(netdev)
```

## How do can you see what accounts are logged in on the machine?

<!-- notecardId: 1758890591115 -->

```console
cip@DESKTOP-KJIIPF2:~$ who
cip      pts/1        2025-09-26 10:48
```

## How can you see a history of who logged in on the machine?

<!-- notecardId: 1758890591118 -->

```cip@DESKTOP-KJIIPF2:~$ last
reboot   system boot  5.15.133.1-micro Fri Sep 26 10:48   still running
reboot   system boot  5.15.133.1-micro Fri Sep 26 09:05   still running
```

## How can you switch from one user to another?

<!-- notecardId: 1758890591120 -->

```bash
su username
```

## Where is the file containing users with sudo rights?

<!-- notecardId: 1758890591122 -->

```console
/etc/sudoers
```

## How can you set a nologin shell for the root user?

<!-- notecardId: 1758890591125 -->

go to 
```console
/etc/passwd
```
add 
```console
/root:x:0:0:root:/root:/usr/sbin/nologin
```
instead of 
```console
root:x:0:0:root:/root:/bin/bash
```

## Given the following row from a sudoers file "%dev ALL=(ALL:ALL) All" explain the first ALL.

<!-- notecardId: 1758890591127 -->

it represents the list of hosts the user can run a list of commands on
in a normal setup there is just one host the localhost

## Given the following row from a sudoers file "%dev ALL=(ALL:ALL) All" explain the part (ALL:ALL).

<!-- notecardId: 1758890591130 -->

it represents the users and groups the user can run commands as

## Given the following row from a sudoers file "%dev ALL=(ALL:ALL) All" explain the last ALL.

<!-- notecardId: 1758890591132 -->

it represents the list of commands the user can run

## In what file are the user passwords stored in?

<!-- notecardId: 1758890591135 -->

```console
/etc/shadow
```

## How can you create a new user?

<!-- notecardId: 1758890591137 -->

```bash
useradd bob
```

## How can you set a password for a user?

<!-- notecardId: 1758890591139 -->

```bash 
passwd bob
```

## How can you change password for the current user?

<!-- notecardId: 1758890591142 -->

```bash
passwd
```

## How can you check the current username?

<!-- notecardId: 1758890591144 -->

```bash
whoami
```

## How can you create a new user and specify a uid?

<!-- notecardId: 1758890591147 -->

```bash
useradd -u 1009 bob
```

## How can you create a new user and specify a guid?

<!-- notecardId: 1758890591149 -->

```bash
useradd -g 1009 bob
```

## How can you create a new user and specify a custom home dir?

<!-- notecardId: 1758890591151 -->

```bash
useradd -d /home/some/project bob
```

## How can you create a new user and specify a custom login shell?

<!-- notecardId: 1758890591154 -->

```bash
useradd -s /bin/bash bob
```

## How can you create a new user and specify a custom comment?

<!-- notecardId: 1758890591157 -->

```bash
useradd -c "nice guy" bob
```

## How do you delete a user?

<!-- notecardId: 1758890591159 -->

```bash
userdel bob
```

## How do you add a new group with custom gid?

<!-- notecardId: 1758890591161 -->

```bash 
groupadd -g 1011 dev
```

## How do you delete a group?

<!-- notecardId: 1758890591164 -->

```bash 
groupdel dev
```

## What is the octal value of the execute permission?

<!-- notecardId: 1759148483362 -->

1

## What is the octal value of the write permission?

<!-- notecardId: 1759148483365 -->

2

## What is the octal value of the read permission?

<!-- notecardId: 1759148483368 -->

4

## What is the order in which file permissions are listed?

<!-- notecardId: 1759148483370 -->

user group others

## If the user is the owner of the file which permissions apply?

<!-- notecardId: 1759148483372 -->

only the user ones

## If the user is not the owner but is in the same group as the owner which permissions apply?

<!-- notecardId: 1759148483375 -->

only the group ones

## If the user is not the owner or in the same group as the owner which permissions apply?

<!-- notecardId: 1759148483377 -->

only the others 

## How do you change the permissions on a file?

<!-- notecardId: 1759148483380 -->

```bash
chmod 777 file
```

## How do you change the ownership of a file?

<!-- notecardId: 1759148483382 -->

```bash
chown user:group some_file
```

## How do you copy an ssh key to a remote server?

<!-- notecardId: 1759148483384 -->

```bash
ssh-copy-id user@hostname
```

## What file contains the public keys that can login to the server?

<!-- notecardId: 1759148483387 -->

```console
/home/some_user/.ssh/authorized_keys
```

## What command can you use to coppy files over ssh?

<!-- notecardId: 1759148483389 -->

```bash
scp some/local/path/file hostname:/some/remote/path
```

## What flags are used by scp to coppy a folder and preserve permissions?

<!-- notecardId: 1759148483391 -->

```bash 
scp -pr some/local/path/file hostname:/some/remote/path
```

-p preserve permissions
-r recursive (for directory)

## How do you see all ip rules in iptables?

<!-- notecardId: 1759148483393 -->

```console
cip@DESKTOP-KJIIPF2:~$ sudo iptables -L
Chain INPUT (policy ACCEPT)
target     prot opt source               destination

Chain FORWARD (policy ACCEPT)
target     prot opt source               destination

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination
```

## Add an incomming rule that permits SSH connections solely from 172.16.238.187 in iptables.

<!-- notecardId: 1759148483396 -->

```bash
iptables -A INPUT -p tcp -s 172.16.238.187 --dport 22 -j ACCEPT
```

## Add a rule that drops all incomming connections with iptables.

<!-- notecardId: 1759148483398 -->

```bash
iptables -A INPUT -j DROP
```

## Add an outgoing rule that permits SSH connections to google.com in iptables at the top of the output chain.

<!-- notecardId: 1759148483400 -->

```bash
iptables -I OUTPUT 1 -p tcp -d google.com --dport 22 -j ACCEPT
```

## What command can you use to schedule a job to run at a certain time?

<!-- notecardId: 1759148483402 -->

```bash
crontab -e
```

## Schedule a job to run at 08:10 AM 19 FEB any weekday.

<!-- notecardId: 1759148483406 -->

```console
10 8 19 2 * job.sh
```

## Schedule a job to run every minute.

<!-- notecardId: 1759148483408 -->

```console
* * * * *
```

## Schedule a job to run every other day (one on one off).

<!-- notecardId: 1759148483410 -->

```console
* * */2 * *
```

## How do you list all jobs scheduled in cron?

<!-- notecardId: 1759148483412 -->

```bash
cron -l
```

## Define a basic service unit file named project-mercury.service the unit file only needs to execute the script /usr/bin/project-mercury.sh in the background using /bin/bash.

<!-- notecardId: 1759153885053 -->

create file in /etc/systemd/system containing :
```console
[Service]
ExecStart=/bin/bash /usr/bin/project-mercury.sh
```

## How do you start a service with systemd?

<!-- notecardId: 1759153885056 -->

```bash
sudo systemctl start project-mercury.service
```

## How do you check a service is active with systemd?

<!-- notecardId: 1759153885058 -->

```bash 
sudo systemctl status project-mercury.service
```

## How do you stop a service with systemd?

<!-- notecardId: 1759153885061 -->

```bash
sudo systemctl stop project-mercury.service
```

## How do you automate the start of a service during boot with systemd?

<!-- notecardId: 1759153885063 -->

add this section to your .service file in /etc/systemd/system
```console
[Install]
WantedBy=graphical.target
```

## How do you ensure the service starts under a particular user with systemd?

<!-- notecardId: 1759153885065 -->

the .service file should contain the following user setting :
```console
[Service]
ExecStart=/bin/bash /usr/bin/project-mercury.sh
User=project_mercury
```

## How do you configure the service to restart automatically if it fails with systemd?

<!-- notecardId: 1759153885067 -->

the .service file should contain the following restart settings:
```console
[Service]
ExecStart=/bin/bash /usr/bin/project-mercury.sh
Restart=on-failure
RestartSec=10
```

## How do you define a dependency on another service with systemd?

<!-- notecardId: 1759153885070 -->

the .service file should contain the following section before the Service section:
```console
[Unit]
After=postgresql.service
```

## How do you ensure all changes to a .service file are applied in systemd?

<!-- notecardId: 1759153885072 -->

```bash 
sudo systemctl daemon-reload
```

## How do you stop and start a service in one command with systemctl?

<!-- notecardId: 1759153885074 -->

```bash
systemctl restart docker
```

## How do you read the config files for a service while it's still running without restarting with systemctl?

<!-- notecardId: 1759153885077 -->

```bash
systemctl reload docker
```

## What command can you use to ensure a service starts at boot every time with systemctl?

<!-- notecardId: 1759153885079 -->

```bash
systemctl enable docker
```

## What command can you use to ensure a service doesn't start at boot every time with systemctl?

<!-- notecardId: 1759153885081 -->

```bash
systemctl disable docker
```

## What are the three main states of a service in systemd?

<!-- notecardId: 1759153885083 -->

Active Innactive Failed

## How do you trigger the edit of service config file with systemctl?

<!-- notecardId: 1759153885086 -->

```bash
systemctl edit project-mercury.service --full
```
--full will provide the entire config file for editing

## How do you list all units currently managed by systemctl?

<!-- notecardId: 1759153885088 -->

```bash
systemctl list-units --all
```

## How do you see the log of systemctl?

<!-- notecardId: 1759153885091 -->

```bash
journalctl
```
-b      see logs from current boot
-u UNIT see logs for a particular unit

