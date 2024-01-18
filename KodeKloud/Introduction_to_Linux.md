* Shell: Linux Command Line
  * A program that allows text base interaction between OS and the user.
  * Directories
    * /home
      * Home directory allows users to store their personal files. It is a dediacated store for users.
      * Indicator for /home directory is ~
    * /dev -> Devices
      *  newly added usb disk is visible here. It goes through Kernel Driver and then User Space to be visible in the user space.
  * Commands
    * Internal (Built-in) Commands
      * 30 such commands like cd, export, echo, pwd, set
    * External Commands
      * They are usually preinstalled or user defined
      | Note: To determine the type of a command use ``type <command>``

### Basic Commands

* ``pwd``
* ``cd``
* ``mkdir -p <directory_path>``
* ``pushd`` -> saves directories to directory stack
* ``popd`` -> calls back from directory stack
* ``more``
* ``less``
* ``dmesg``: messages created by Kernel itself
* ``udevadm info``: to determine to newly added devices
* ``lspci``: detecting network related components
* ``lsblk``: disks and partitions related information
* ``lscpu``: detailed info about cpu architecture
* ``lsmem --summary`` or ``free -m``: memory info
* ``runlevel``: There are several other modes than graphical one.
  * ``systemctl get-default`` this comand looks up the file``/etc/systemd/system/default.taget``
  * ``systemctl set-default multi-user.target``is equivalent to change runlevel from 5 to 3
    * runlevel 0 -> poweroff.target
    * runlevel 1 -> rescue.target
    * runlevel 2 -> multi-user.target
    * runlevel 3 -> multi-user.target
    * runlevel 4 -> multi-user.target
    * runlevel 5 -> graphical.target
    * runlevel 6 -> reboot.target
* ``df -hP`` -> show all mounted filesystems
* ``du -sh filename`` -> shows the file size in humanreadable
* ``tar -cd test.tar file1 file2 file3``: archive the specified file or directory
* ``tar -tf test.tar``: see the content of the tarball
* ``tar -xf filename``: extract the files from tarball
  * ``gzip -d filename``
* ``tar -zcvf <destination_dir> file1 file2 file3`` -> compress the archive file.
* ``zcat`` -> to read .gz files without unzipping
* ``bzip2``
* ``gzip``
* ``xz``

* ``grep -i capital sample.txt``: case insensitive mode
* ``grep -r 'third line' /``: search for a pattern in a recursive mode
* ``grep -v pattern path``: not matching results
* ``grep -w exam example.txt``: matching the full pattern
* ``grep -A pattern file``: row numbers of lines that are after the matching line
* ``grep -B pattern file``: opposite of above
* ``grep -Rnw '/path/to/somewhere/' -e 'pattern'`` -> finding a pattern in a directory
  
### Linux Kernel

It is an interface between Applications and Hardware of the device. It is responsible for;

1. Memory Management
   1. Kernel Space: This space is private for the Kernel
      1. Kernel Services
      2. Device Drivers
   2. User Space: This space has restiricted access to hardware
      1. Programs in C, Java, Python...
      2. Docker Containers
      3. ...
   Programs from User Space reach out the Kernel via "System Calls". For instance, opening a file with ``cat /etc/os-release`` creates a system call  
2. Process Management
3. Device Drivers
4. System Calls and Security


### Linux Boot Sequence
1. BIOS POST
   1. Power On Self Test
2. BOOT LOADER (GRUB2)
   1. Once the selection is made, the boot loader boots the kernel into the memory.
3. Kernel Initialization
4. Init Process
   1. Init function calls systemd deamon. Systemd is responsible for mounting file systems, starting and managing file systems.
   2. ``ls -l /sbin/init`` -> ``x.xxx.xxx.xxx /sbin/init -> /lib/systemd/systemd``

### File Types

Everything in linux is file!

* Regular Files
  * Images
  * Scripts
  * Configurations / Data Files
* Directory
  * /home/kasim
* Special Files
  * Character Files
    * Represents the devices defined in /dev
    * Mouse, Keyboards
  * Block Files
    * Also in /dev
    * Represents block files
    * lsblk command looks for here
    * Hard Disks and RAM
  * Links
    * Hard Link: associates to files to the same block of data from the physical disk altough behaves as independent files. Deleting one will delete the data. 
    * Symbolik Name: Shortcut in Windows.
  * Socker Files
  * Named Pipes

### File System Hierarchy

* /
  * /bin
    1. binary files  
  * /boot
  * /dev
    * physical devices stored here.
    * 
  * /etc
    1.  Configuration files
  * /home
    1. Directory for home directories of all users except for the root user
  * /lib
  * /media
    1. All external media mounted here. 
  * /mnt
    1. Temporary place
  * /opt
    1. Install all the third party applications here
  * /tmp
    1. store temporary data
  * /usr  
    1.  User land applications stored here like Mozilla, Vi Test Editor... 
  * /var
    1.  This is directory where system chache data and logs.

### Linux Package Management

One of the common way of categorizing Linux Distribution is by its package manager

* ``apt`` or ``dpkg`` Based Distros
  * Debian
  * Ubuntu
  * ARch Linux
  * Linux Mint
* ``rpm`` and ``yum`` Based Distros
  * RHEL
    * Community Version
    * Free Version
    * Community Support
  * Centos
    * Community Version
    * Paid Version
    * Technical Support
  * Fedora

#### ``rpm``

* installation
  * ``rpm -ivh telnet.rpm``
* Uninstall
  * ``rpm -e telnet.rpm``
* Upgrade
  * ``rpm -Uvh telnet.rpm``
* Query the packages
  * rpm database is stored in ``/var/lib/rpm``
  * ``rpm -q telnet.rpm``
* Verification
  * ``rpm -Vf <path_to_package>``
  
#### ``yum``

Works with rpm based distros. Depends on rpm in the background.

* ``yum install httpd``: Checks if it is already installed. If not checks for the ``repos.d``
* Trnasaction Summary

* ``yum reposlist``
* ``yum provides scp``

* ``yum remove httpd``

* ``yum update httpd``

#### ``dpkg`` -> debian package manager

* Installation / upgrade -> ``dpkg -i telnet.deb``
* Uninstall &rarr; ``dpkg -r telnet.deb``
* list &rarr; ``dpkg -l telnet``
* status &rarr; ``dpkg -s telnet``
* verify &rarr; ``dpkg -p <path_to_file>``


* Software Package is a compressed archive that contains all the files that are required by a particular software to run. For instance, Gimp.
* Package Manager is a software in Linux that is responsible for installing and maintaining packages

### IO Redirection

* Std  Input
* Std Output
* Std Error

## Networking

* An ip address to the ``/etc/hosts`` file.
* DNS Server address to ``/etc/resolv.conf``
* When we try to open connections to another host, system looks for addresses from 2 destinations; first from ``/etc/hosts`` and the second from DNS Server under ``/etc/resolv.conf``. **We can change the order!**; by changing ``/etc/nssswitch.conf``. If no ip addresses found in both of these files, we can direct the requests to ``8.8.8.8`` -Google's DNS Server-.
* Look Domain Names with ``nslookup``

* Subdomains? www.google.com

### Switching and Routing

* By switches, we create networks or LAN
  * to connect to a switch we need an interface for each device in the network. This means if want a device to connected to a network there should be interface on it attained to this exact network.
  * ``ip link`` shows the interfaces for the host
  * ``ip addr`` to show the ip addresses asigned to these interfaces
  * We need to assign an ip address to the interface by ``ip addr add <HOST_IP> dev ens0``
  * to bring up a network interface ``sudo ip link set dev eth0 up``
  NOT: To make these changes persistent be sure to configure these from ``/etc/network/interfaces``
* By routers, we can communicate internetworks.
  * ``route -n`` command shows configured routers (or gateways)
  * To add new route to linux, ``ip route add <NETWORK_ADDRESS> via <ROUTER_ENTRANCE_IP>``
  * To add default gateway ``sudo ip r add default via <ROUTER_ENTRANCE_IP>``
  * To delete the default route, ``sudo ip r del default``
  * ``traceroute`` shows all the routers and switches between destination and source subject to the connection

## Security and File Permissions

### SSH

* Secure Shell
  * ``ssh <user>@<IP_ADDRESS>``
  * Requires ssh server running on the remote service accessible from the client.
  * ``ssh-copy-id <user>@<REMOTE_SERVER>`` to send public key to the remote server
  *  ``scp <FILENAME_TO_BECOPIED> <USER>@<REMOTE_SERVER>:<PATH_TO_BE_COPIED>`` to copy files serverwide.

#### IPTABLES
* ``iptables -L`` list the iptables
* ``iptables -A INPUT -p tcp -s <SRC_IP> --dport <DEST_PORT> -j <ACTION>`` adding rule to iptables
* __Biraz çalış buna!!!__

## Service Management With SYSTEMD

example application -> ``/usr/bin/project-mercury.sh``

* Start Python App after Postgres DB
* Use Service Account project_mercury
* Auto Restart on Failure
* Restart Interval 10 seconds
* Log Service Events
* Load when booting into Graphical Mode

To run the example app on the background;
* We need to run it as a service -> create a service unit file on ``/etc/systemd/system/project-mercury.service`` as [here](./project-mercury.sh_file)
* to start the service ``systemctl start <SERVICE NAME>``
* to check the status of the service ``systemctl status <SERVICE_NAME>``
* to stop the service ``systemctl stop <SERVIC_NAME>``
* to detect the new changes for the system run ``systemctl deamon-reload``
* start the service again

* ``systemctl start docker`` start a service
* ``systemctl stop docker`` stop a server
* ``systemctl restart docker`` restart the service
* ``systemctl reload docker`` reload the service without interrupting the normqal functionality
* ``systemctl enable docker`` make a service persistent across reboots
* ``systemctl disable docker``
* ``systemctl status docker ``
* ``systemctl deamon-reload`` reloads the system configuration after changing the service unit files and makes the systemd aware of the changes
* ``systemctl edit <SERVICE_NAME> --full`` this will open a text editor. Units editted this way will apply the changes without needed for deamon-reload
* ``systemctl ger-default`` to get the runlevel
* ``systemctl list-units --all`` this print all units
* ``journalctl`` is usefull when troubleshooting systemd units
* ``journalctl -b``
* ``journalctl -u <UNIT_NAME>``

## Storage in Linux

To use files in the disk

1. Partition Disk
2. Create Filesystem
3. Mount Filesystem

### Disk Partitions

* ``lsblk`` shows the block devices.
  * sda -> schasy device (physical disk)
  * Block device is a device under the /dev directory.
    * SSD, Flash
    * ls -l /dev/ | grep "^b" -> block devices start with b.
* ``fdisk -l /dev/sda`` prints the partition table.

* ``gdisk /dev/sdb`` to create partition on a disk

### File System in Linux (ext2 - ext4)

* ext2
  * 2TB File Size
  * 4TB volume size
  * support compression
  * support linux permissions
  * long crash recovery
* ext3
  * 2TB File Size
  * 4TB volume size
  * Uses Journal
  * Backwards compatible
* ext4
  * 16TB File Size
  * 1 Exabyte
  * Uses Journal
  * Uses chksum for journal
  * backwards compatible


* ``mkfs.ext4 /dev/sdb1``
* ``mkdir /mnt/data``
* ``mount /dev/sdb1 /mnt/data``

* To make the mount operation persistent accross system reboot,
  * ``echo "/dev/sdb /mnt/data ext4 rw 0 0" >> /etc/fstab``

### External Storage Devices - DAS, NAS and SAN

These are external storages.

* DAS: Direct Attached Storage
  * connected as a block device
  * it is fast
* NAS: Network Attached Storage
  * 
* SAN: Storage Area Network
  * Best

### NFS

* Works on a server client model
* ``/etc/exports`` define the clients that should access to the directory
* ``exportfs -a`` will share the directory to the clients defined above
* on the client side ``mount <NFS_SERVER>:/shareddata/ /mnt/shareddata``
* 

### Logical Volume Manager LVM

* ``apt-get install lvm2``
* ``pvcreate /dev/sdb``
* ``vgcreate <vgroup_name> /dev/sdb``
* ``pvdisplay``
* ``vgdisplay``

* ``lvcreate -L <VOLUME_SIZE> -n <VOLUME_NAME> <VOLUME_GROUP_NAME>``
* ``lvdisplay``
* ``lvs`` -> list lvs
* ``mkfs.ext4 /dev/caleston_vg/vol1`` create filesystem on logical volume
* ``mount -t ext4 /dev/caleston_vg/vol1 /mnt/vol1``
* resize lvm while it is mounted, 
  * firstly check if there is enough space on volume_group ``vgs``
  * ``lvresize -L +1G -n /dev/caleston_vg/vol1`` logical volume has been resized not the file system
  * ``resize2fs /dev/caleston_vg/vol1``

* Unmount a File System
  * ``umount <DIRECTORY>``
  If the file system is in use the umount command will fail to detach the file system. In those situations, use the below commsnd to see which processes are accessing file system
  * ``fuser -m <DIRECTORY>``
  * Use lazy unmoount to wait for the procccesses to finnish their work on the file system
    * ``umount -l <DIRECTORY>``