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



2. Operations Deployment (%20)
   1. System Boot Processes
   2. Task Automation
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