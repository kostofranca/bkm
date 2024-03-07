# Linux Foundation Certified System Administrator

11.12.2023

---

1. Essential Commands (%25)

    * Logging System and Working with Files and Directories
      * ``man man``
      * ``apropos -s <comma-seper.-list-of-sections> <some-text>`` command searches for matching texts in the man pages. First time we try to use ``apropos``, we need to create the database with this ``sudo mandb``
      * ``cd -`` go to the previous directory
      * Hardlinks;
        * Inodes:
          * Inodes stores the data on disk.
            * ``stat <file_name>``
              * This gives an inode number. File systems such as XFS or Ext4 keep track of data wit hthe help of inodes. Inodes also keeps permissions, last modification date...
        * Links create a bound between Inodes and files in the file system. Links in stat command gives us the hard link count.
        * By links we could store just once and share the same file with hard links.
        * If we delete all the hard links from an inode, the data itself will be removed from the disk.
        * You can not hard link to directories and another file system 
        * ``ln <target_file> <file_to_be_linked>``
      * Softlinks
        * A link that points to a path.
        * ``ln -s <target_file> <file_to_be_linked>``
      * Set, List and Change Standart File Permissions
        * ``chgrp <group_name> <file/directory>`` -> change the group of a file or directory
        * ``groups`` -> see the list of groups that current user belongs to
        * ``chown <user>:<group> <file/directory>``
        * ``chmod [ugo][+-=][rwx] <file_name>``
      * SUID, GUID and Sticky Bit
        * ?
      * Search Files
        * ``find <path> -name '*.jpg`` -> find jpg files
        * ``find <path> -size +10M`` -> files bigger than 10Mb
        * ``find <path> -mmin -1`` -> modifed files in the last minute
      * Compare and Manipulate File Content
        * ``tac some_file.txt`` -> print the file content in reverse order. Reverse order of ``cat``
        * ``tail -n 20 some_file`` -> last 20 line of the file
        * ``head -n 20 some_file`` -> first 20 line of the file
        * ``sed -i 's/tobereplaced/finetext/g' some_file.txt`` -> stream editor command for manipulating some text in a file. ``-i`` tag for replacing in the original file, it stands for ``--in-place``
        * ``cut -d ' ' -f 1 some_file.txt`` -> This will show the first column of a file. ``-d`` is delimeter parameter
        * ``sort some_file | uniq`` -> We need to sort the files before taking the unique elements out
        * ``diff -c file1.txt file2.txt`` -> prints the differences of two files
        * ``diff -y file1.txt file2.txt`` -> side by side difference
      * Searching Files
        * ``grep -i "pattern" /some_file.txt`` -> ``-i`` ignore case sensitivity
        * ``grep -r "pattern" /etc/`` -> ``-r`` stands for recursiveness
      * Regular Expressions
        * ``grep '^A' some_file.txt`` -> The line begins with A.
        * ``grep 'A$' some_file.txt`` -> The line ends with A.
        * ``grep -r 'c.t' /etc/`` -> Match any ONE character in the directory specified recursively.
        * ``grep -r 'let*' /etc/`` -> Match the previous element 0 or more times
        * ``grep -r '0\+' /etc/`` -> Match the previous element 1 or more times
        * Extended Regular Expressions
          * ``egrep -r '0+' /etc/`` -> Match the previous element 1 or more times
          * ``egrep -r '0{3,}' /etc/`` -> The previous element can exists at least {} many times
          * ``egrep -r '0{,3}' /etc/`` -> The previous element can exists at most {} many times
          * ``egrep -r 'disabled?' /etc/`` -> Make the previous element optional
          * ``egrep -ir 'disabled?|enabled?' /etc/`` -> Match one thing or the other with case insensitive
          * ``egrep -r '/dev/[a-z]*[0-9]?' /etc/`` -> Match either of the one in the set
          * ``egrep -r '([a-z][A-Z]*[0-9]?)*'`` -> Subexpressions
          * ``[^]``
      * Archive, Backup Operations
        * Archive
          * ``tar`` -> Tape archive
          * Packing Files and Directories with TAR
            * ``tar cf archive.tar file1`` -> Create tarball of file1
            * ``tar rf archive.tar file2`` -> Append the file to the tarball
            * ``tar --list --file archive.tar`` -> Before extracting a tarball always use a list option
            * ``tar xf archive.tar`` -> Extract the content to the current directory
            * ``tar xf archive.tar -C /some_directory`` -> Extract the content in the specified directory
            * 
        * Compress
          * ``g-un-zip file1`` -> Compress a file
          * ``b-un-zip file2`` -> Compress a file
          * ``-un-xz file3`` -> Compress a file
          * ``-un-zip -r file4`` -> Compress recursively
          * ``tar czf archive.tar.gz file1`` -> Archive and compress the file at the same time with ``tar`` command (gzip)
          * ``tar cjf archive.tar.bzip2 file2`` -> Archive and compress the file at the same time with ``tar`` command (bzip)
          * ``tar cJf archive.tar.xz file3`` -> Archive and compress the file at the same time with ``tar`` command (xz)
      * Send to  a Remote Location
        * ``rsync -a Pictures/ aaron@1.1.1.1:/home/aaron/Pictures`` -> Sync with a remote server

   * I/O Redirection
     * Redirect Output
       * ``cat some_file.txt > redirect_file.txt``
       * stdin, stdout, stderr
         * ``>`` -> stdout
         * ``<`` -> stdin
         * ``2>/dev/null`` -> stderr
         * ``grep -r '^The' /etc/ 2>&1 1>all_output.txt`` -> ???????
       * Heredoc HereString
         * ``sort << EOF`` -> ?????????
     * SSL Certificates
       * Secure Socket Layer -> SSL
     * Git Operations
       * ``git reset file_name`` -> Unstage a file

2. Operations Deployment (%20)

   1. System Boot Processes
      * Boot, Reboot and Shutdown A System Safely
        * ``systemctl reboot``
        * ``systemctl reboot --force``
        * ``systemctl poweroff`` -> Shutdown the server
        * ``systemctl poweroff --force``
        * ``systemctl poweroff --force --force`` -> Unplug the powersouce (Very last resort)
        * ``shutdown 02:00`` -> shutdown a schedule (24-hour based)
        * ``shutdown -r +15`` -> Schedule a reboot in 15 minutes
        * ``shutdown -r +15 "<WALL MESSAGE>"`` -> Prompt a message while shutting down
      * Change Operation Modes
        * ``systemctl get-default`` -> What is our default boot target?
        * ``systemctl set-default multi-user.target`` -> Create new boot target
        * ``systemctl isolate graphical.target`` -> Switch between targets
        * ``systemctl isolate emergency.target`` -> Usefull for debuging it is only read-only (the root user must have a password)
        * ``systemctl isolate rescue.target`` -> We will be directed to the root shell (the root user must have a password)
      * Install, Configure and TroubleShoot Bootloaders
        * A bootlader is to start the linux kernel. GRUB is popular bootloader.
        * Interesting topic, Work more on this.
        * ``/etc/default/grub`` -> Default GRUB configuration file
   2. Task Automation
      * Use Scripting to Automate System Tasks
        * When we log in, "Bash" program opens up ( a command interpreter )
        * ``#!/bin/bash`` -> To run the scripts in the file, ad this line as the first line in the file.
        * ``#`` -> Comment line in the bash script
        * ``cat /proc/version`` -> Prints the kernel version in linux
        * ``help`` -> to see the bash default commands
        * ``cat /etc/cron.hourlv/0anacron`` -> Cheatsheet for bash scripts!!!!!!!
   3. Managing Critical Resources of Processes
      * Manage the Startup Processes
        * Service Unit Files
        * ``systemctl cat <service_name>`` -> Print the content of service unit file to the screen
        * ``systemctl edit --full <service_name>`` -> Edit the service unit file (some trial mode)
        * ``systemectl revert <service_name>`` -> Cancel the changes of the service file edited in ``edit`` option.
        * ``systemctl status <service_name>`` -> Status of the service
        * ``systemctl reload <service_name>`` -> Reload the configuration files of the service
        * ``systemctl reload-or-restart <service_name>`` -> Restart the service if reolad is not supported by the service
        * ``systemctl is-enabled <service_name>`` -> Check if the service is enabled
        * ``systemctl enable --now <service_name>`` -> start and enable the service at the same time
        * ``systemctl mask <service_name>`` -> Sometimes services starts by other services even we stop them. This commmand prevent this
        * ``systemctl mask <service_name>`` -> Obvious
        * ``systemctl --list-units --type service --all`` -> List all the available services on the system
      * Create Systemd Service File
        * ``man systemd.service``
        * ``ls /lib/systemd/system/`` -> List the service unit files available
        * ``ls /lib/systemd/system/ssh.service`` -> Exaample service file
      * Manage System Processes
        * ``ps aux`` -> List the active processes
        * ``ps u -U <user_name>``
        * ``ps -a <process_name>`` -> list all the prcesses that name containing <process_name>
        * ``nice -n <-20 - 20> <program_name>`` -> nice value attachment for processes
        * ``sudo renice 9 <PID>`` -> reassign a nice value to a process
        * ``ps lax`` -> all processes not just the user we are running as with their nice value
        * ``ps fax`` ->  process tree
        * ``pgrep -a bash`` -> All the processes containing name bash with their PIDs
        * ``lsof -p bash`` -> All the files opened by the process
      * Locate and Analyse System Log Files
        * ``/var/log`` directory contains the system logs
        * ``journalctl -p`` -> priority tags list
        * ``journalctl -S <since_date> -U <until_date>`` -> Look for logs in a given time interval
        * ``last`` -> who logged in lastly
        * ``journalctl --unit=sshd.service -n 20 --no-pager`` -> sshd deamon logs
      * Schedule Tasks
        * CRON
          * ``cat /etc/crontab``
          * ``crontab -l`` -> List the entries in the crontable
          * ``crontab -e -u <user>`` -> crontab entries for <user>
          * ``crontab -r`` -> remove entries from crontable of the logged in user
          * ``crontab -r -u <user>`` -> remove entries for a user from crontable
          * Another way to set a cronjob is to add the script in the following directories accordingly
            * ``/etc/cron.hourly``
            * ``/etc/cron.daily``
            * ``/etc/cron.weekly``
            * ``/etc/cron.monthly``
        * ANACRON
          * ``vi /etc/anacrontab`` -> Anacron table for scheduled tasks
          * ``anacron -T`` -> to check if syntax for anacron table is correct
          * ``anacron -n`` -> run all the jobs --now
          * ``at 'now + 1 minutes'`` -> Schedule a command/script to be run in 1 minute
          * ``atq`` -> list scheduled jobs
          * ``atrm <job_id>`` -> remove a job
      * Manage Software Using Package Manager
        * ``dpkg --listfiles nginx`` -> Files downloaded with the software
        * ``dpkg --search /usr/sbin/nginx`` -> wich package the file belongs to
        * ``apt show <package_name>`` -> What use the dependency have for main software
        * ``apt serach --names-only <package_name>`` -> Search for the packages that only names matches not their description
        * ``apt autoremove <package_name>`` -> Remove a package along with its dependencies
      * Repository Configuration for a Package Manager
        * ``/etc/apt/sources.list`` -> Repolist for Ubuntu
        * To install a third party software,
          * ``curl <key_address> -o <key_name>.key`` -> Download the gpg key,
          * ``gpg --dearmor <key_name>.key`` -> text format to binary format so that our package manager can understand
          * ``mv <key_name>.key.gpg /etc/apt/keyrings`` -> This directory keeps third party public keys
          * ``vi /etc/apt/source.list.d/<package_name>.list`` -> Create repo for docker
          * ``echo "deb [signed-by=/etc/apt/keyrings/<key_name>.key.gpg]" <package_address> jammy stable > /etc/apt/source.list.d/<package_name>.list``
          * ``apt update`` -> Update the repositories that we see
          * ``add-apt-repository ppa:user/appplication`` -> Add Personal Package Archive
          * ``add-apt-repository --list`` -> List all repos included ppa
          * ``add-apt-repository --remove <repo_name>`` -> Remove the PPA repo from the list
      * Install a Software by Compiling the Source Code
      * Verify the Integrity and Availibility of Resources
        * ``df -h``
        * ``du -sh`` -> How much disk space files cover
        * ``free -h`` -> RAM Usage
        * ``free --mega`` -> Total memory
        * ``uptime`` -> CPU Usage
          * ``17:24:55 up 32 min, 1 user, load average: 0.05, 0.05, 0.01``
          * First number is the load average in the last minute, second in the last 5 minute, last in the 15 minute
        * ``lscpu`` -> Some specifik CPU info
        * ``lspci`` -> Detail on hardware
        * ``systemctl list-dependencies`` -> Dependencies of a service
      * Kernel Runtime Paramaters
        * ``sysctl -a`` -> List kernel runtime parameters
        * ``sysctl -w <kernel_config>=1`` -> disable some kernel parameter
        * ``sysctl -p`` -> makes the values persistent in the ``/etc/sysctl.conf`` file
      * SElinux !!!!!!!! Important Topic, Did not understand
        * ``ls -Z`` -> SELinux Context Label list
          * ``unconfined_u:object_r:user_home_t:s0`` -> user:role:type:level
        * ``chcon -t <syscontext> <file_path>`` -> Change the selinux context of a file
        * ``getenforce`` -> Get the current SELinux mode
        * ``setenforce 0`` -> Temporarily change the SELinux status to "permissive" on the system
        * ``semanage user -l`` -> SELinux User Table
  
3. User and Group Management (%10)
  1. Creating and Managing User Accounts
    * ``useradd john`` -> Create user
    * All the directories from ``/etc/skel`` will be coppied to the new users home dir
    * ``useradd --defaults`` -> Default settings for creation of new users
    * ``userdel <user_name>`` -> Delete user, This may delete the group also. But home directory will remain
    * ``userdel -remove <user_name>`` -> will delete the home directory as well
    * ``useradd --shell /bin/othershell --home-dir /home/otherdirectory/ john`` or ``useradd -s /bin/othershell -d /home/directory john`` -> add user with custom shell and home directory
    * ``useradd -u <custom_ID> <user_name>`` -> add user with custom id number
    * ``useradd --system <user_name>`` -> add a system user account, their id's are smaller than 1000
    * ``usermod -d /home/otherdirectory -m <user_name>`` -> Move <user_name>'s home directory
    * ``usermod --login <new_user_name> <old_user_name>`` or ``usermod -l <new_user_name> <old_user_name>``-> Change user name for current user
    * ``usermod -s /bin/othershell <user_name>``-> Change the shell for user
    * ``usermod -L <user_name>`` -> Lock user account (User files does not deleted)
    * ``usermod -U <user_name>`` -> Unlock user account
    * ``usermod -e "<YYYY-MM-DD>" <user_name>`` -> Set an expire data for user account. User will not be able to log in to his account. It can be reenabled. To enable the account use the below command
    * ``usermod -e "" <user_name>``
    * ``chage --lastday <day> <user_name>`` or ``chage -d <day> <user_name>`` -> Expiration for password. Unexpire a password with below command
    * ``chage -d -1 <user_name>``
    * ``chage -M <day> <user>`` -> Set a password change period as a day for user
    * ``chage -l <user_name>`` -> to see when the user passsword expires
    * ``groupdel <group_name>`` -> Delete the group
    * ``gpasswd --a <user_name> <group_name>`` -> add user to a secondary group
    * ``groups <user_name>`` -> see the groups that user belongs to
    * ``gpasswd -d <user_name> <group_name>`` delete user's secondary group
    * ``usermod --gid <group_name> <user_name>`` -> Change the user's primary group.
    * ``groupmod -n <new_group_name> <old_group_name>`` -> change the group name
  2. Manage Environment Variables
    * ``env`` or ``printenv`` -> Prints the environment variables
    * ``/etc/profile.d`` -> This are the scripts that run in the startup of the shell
  3. Set Resource Quotas
    * ``/etc/security/limits.conf`` -> User limits
    * ``ulimit -a`` -> List user limits
  4. Configuring Advance Authentication Options
    * ``/etc/sudoers`` has this syntax ``user/%group host=(run_as_user) -NOPASSWD:ALL-command_list``
    * ``visudo`` -> MAke changes to suders file in a safe mode
4. Networking(12%)
  1. Network
    * ``xxx.xxx.xxx.xxx/24`` -> This is called CIDR notation. This means that first 24 bits of this address are the prefix of this network.
    * ``ip a`` -> List all the network interfaces
    * ``ip -c add`` -> list everything in colors
    * ``ip link set dev <interface> up`` -> If you have a network interface down, use this command to get it up. Making up does not give IP.
    * ``ip address add <ip_address_CIDR> dev <interface>`` -> Give ip address to an interface that is up.
    * ``ip address delete <ip_address_CIDR> dev <interface>`` -> Delete an ip address
    * ``ip`` command makes temprary changes. Ass soon as the system is rebooted, the changes are gone.
    * ``netplan try`` -> This command applies the changes in the ``/etc/netplan/*`` files. This also just checks and apply the changes since we are trying to configure the network and this has some serious effects.
    * ``netplan get`` -> list all the configurations for all the interfaces
    * ``resolvectl status`` -> Status of network interfaces and global configurations
    * ``/etc/systemd/resolved.conf`` -> The global congiurations for DNS
    * ``resolvectl dns`` -> Shorter output for DNS
  2. Services
    * ``ss -tulpn`` -> Services waiting for incoming network connections
      * ``-l`` for listening
      * ``-t`` for TCP connections
      * ``-u`` for UDP connections
      * ``-n`` for numeric values like port number
      * ``-p`` for processes, because of this tag we need root privileges
    * Bond and Bridging
      * ``/usr/share/doc/netplan`` -> Contains example files
      * ``ip link set dev <bond_name> down`` -> undervision bond
      * ``ip address add <ip_address_CIDR> dev <bond_name>`` -> Give ip address to an bond.
  3. Routing
  4. Packet Filtering
    * ``ufw`` is an abbreviation for Uncomplicated Firewall
    * ``ufw status verbose`` -> Status of ufw
    * ``ufw enable`` -> Enable the firewall
    * ``ufw allow 22/tcp`` -> allow tcp connection on 22
    * ``ufw allow from <SENDER_IP> to any port <port_number>`` -> from <SENDER_IP> allow to "any" IP addresses' on port 22
    * ``ufw status numbered`` -> We see the rules listed with numbers
    * ``ufw delete <RULE_NUMBER>`` -> delete the rules with their index number
    * ``ufw insert 3 deny <IP>`` -> Insert deny rule to a number 3 in the ufw table
    * ``ufw deny out on <interface> to <target_ip>`` -> Deny all outgoing traffic to a ip address from an interface
    * ``ufw allow in on <interface> from <source_ip> to <dest_ip> port <port_number> proto <protocol(tcp/udp)>``
  5. Port Forwarding
    * ``/etc/sysctl.d/99-sysctl.conf`` -> Change the port forwarding options from here.
    * ``sysctl --system`` -> Make available the above changes to the system.
  6. Create a Reverse Proxy
    * ``apt install nginx`` -> Install nginx
    * ``vi /etc/nginx/sites-available/proxy.conf`` -> Load Balancing options are configured here
    * ``vi /etc/nginx/proxy_params`` -> are the proxy configuration files.
    * ``ln -s /etc/nginx/sites-available/proxy.conf /etc/nginx/sites-enabled/proxy.conf`` -> Enable the configurations
    * ``rm /etc/nginx/sites-enabled/default`` -> To disable the configurations
    * ``nginx -t`` -> check the config files for errors
    * ```ln -s /etc/nginx/sites-available/lb.conf /etc/nginx/sites-enabled/lb.conf`` -> Load Balancing options are configured here, too.
    * ``systemctl restart nginx``
  7. Syncronize Time Using Time Servers
    * ``timedatectl list-timezones``
    * ``timedatectl set-timezone``
5. Service Configuration (%20)
   1. Linux Cost Necessary Services
   2. DNS
   3. SSH
   4. Mail Server
6. Storage Management (%13)
   1. Logical Volume Management
   2. Advanced File System Permission

NOTES

* ``/usr/share/doc`` -> Contains example files for some applications

| Consider RHCSA Eam
