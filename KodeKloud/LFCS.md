# Linux Foundation Certified System Administrator
11.12.2023
---

1. Essential Commands (%25)
  1. Logging System and Working with Files and Directories
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
      * Archive, Bacup Operations
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
        *  ``#!/bin/bash`` -> To run the scripts in the file, ad this line as the first line in the file.
        * ``#`` -> Comment line in the bash script
        * ``cat /proc/version`` -> Prints the kernel version in linux
        * ``help`` -> to see the bash default commands
        * ``cat /etc/cron.hourlv/0anacron`` -> Cheatsheet for bash scripts!!!!!!!
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
        * ``ps lax`` -> all processes not just the user we are running as
        * ``ps fax`` ->  process tree
        * 
   3. Managing Critical Resources of Processes
3. User and Group Management (%10)
   1. Creating and Managing User Accounts
   2. Set Resource Quotas
   3. Configuring Advance Authentication Options
4. Networking(12%)
   1. Network
   2. Services
   3. Routing
   4. Packet Filtering
5. Service Configuration (%20)
   1. Linux Cost Necessary Services
   2. DNS
   3. SSH
   4. Mail Server
6. Storage Management (%13)
   1. Logical Volume Management
   2. Advanced File System PermissionLFCS



| Consider RHCSA Eam
