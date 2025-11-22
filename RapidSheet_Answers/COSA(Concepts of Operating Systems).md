# Concepts of Operating System and Administration - Windows Answers (1-15)

1. **What is Hyper-V? Explain.**
   - **Hyper-V:** Microsoft's native hypervisor for creating and running virtual machines on Windows systems.
   - **Features:**
     - Type 1 hypervisor (runs directly on hardware)
     - Supports hardware virtualization (Intel VT-x, AMD-V)
     - Can run multiple operating systems simultaneously
     - Provides isolation between VMs
     - Supports dynamic memory, live migration, and snapshots
   - **Uses:** Server virtualization, development/testing, cloud infrastructure

2. **What is Active Directory? Explain basic features in Active Directory (AD) of Windows server?**
   - **Active Directory:** Microsoft's directory service for Windows domain networks.
   - **Basic Features:**
     - Domain Services: Centralized domain management
     - User and Computer Management: Centralized user/computer accounts
     - Group Policy: Centralized configuration management
     - DNS Integration: Name resolution for domain resources
     - Security: Authentication and authorization services
     - Organizational Units (OU): Hierarchical container structure
     - Trust Relationships: Cross-domain authentication

3. **What are FSMO roles in Windows Active Directory? How to transfer FSMO roles? What is seize FSMO role option? When to use it?**
   - **FSMO Roles:** Flexible Single Master Operations - specialized domain controller roles:
     - Schema Master
     - Domain Naming Master
     - PDC Emulator
     - RID Master
     - Infrastructure Master
   - **Transfer FSMO Roles:**
     - Use `ntdsutil` or Active Directory Users and Computers
     - Planned operation when DC is available
   - **Seize FSMO Roles:**
     - Forced transfer when original role holder is permanently unavailable
     - Use `ntdsutil` with "seize" command
     - Only used when original DC cannot be recovered

4. **How to take active directory backup? What is authoritative and non-authoritative restore of Active Directory?**
   - **AD Backup:** Use Windows Server Backup or `wbadmin` command
     - Command: `wbadmin start systemstatebackup -backupTarget:D:`
   - **Non-authoritative Restore:**
     - Restores AD data but domain replication updates it from other DCs
     - Used when single DC fails but others are available
   - **Authoritative Restore:**
     - Restored data takes precedence over other DCs
     - Use `ntdsutil` after restore to mark objects as authoritative
     - Used when accidental deletions need to be recovered

5. **Explain DNS & DHCP. How to configure in Windows?**
   - **DNS (Domain Name System):** Translates domain names to IP addresses
   - **DHCP (Dynamic Host Configuration Protocol):** Automatically assigns IP addresses to network devices
   - **Configuration in Windows:**
     - Install DNS/DHCP server roles via Server Manager
     - DNS: Create forward/reverse lookup zones, add records
     - DHCP: Create scopes, configure options (gateway, DNS), authorize server

6. **What is the difference between tree domain vs child domain?**
   - **Tree Domain:** New domain tree in existing forest with different DNS namespace
     - Example: company.com (existing) → newcompany.com (tree domain)
     - Two-way transitive trust with forest root
   - **Child Domain:** Subdomain of existing domain, shares contiguous namespace
     - Example: company.com → sales.company.com (child domain)
     - Inherits some policies and trusts from parent

7. **What are built in groups – Domain Admins, Enterprise Admins, Server Operator, Accounts operator, Backup Operator, Domain Users?**
   - **Domain Admins:** Full administrative rights to the domain
   - **Enterprise Admins:** Full administrative rights to entire forest
   - **Server Operators:** Can manage domain controllers (shutdown, backup)
   - **Account Operators:** Can create/modify user accounts and groups
   - **Backup Operators:** Can backup and restore files regardless of permissions
   - **Domain Users:** All domain user accounts are members

8. **How to restore a failed Domain controller?**
   - **Steps:**
     1. If available, remove failed DC metadata using `ntdsutil`
     2. Install Windows Server on new hardware/VMs
     3. Promote to Domain Controller using Server Manager
     4. Choose "Add DC to existing domain"
     5. Select global catalog if needed
     6. Allow AD replication to synchronize
     7. Transfer FSMO roles if this was holding any

9. **Elaborate the concept of Network Policy Server (NPS).**
   - **NPS:** Microsoft's RADIUS server and network policy system
   - **Functions:**
     - Centralized authentication, authorization, accounting
     - Network Access Protection (NAP) policies
     - VPN and wireless access control
     - Integration with Active Directory
   - **Components:** Connection request policies, network policies, accounting

10. **What is File Server Resource Manager (FSRM)?**
    - **FSRM:** Server role for managing and classifying file server data
    - **Features:**
      - Quota management: Limit disk space usage
      - File screening: Block specific file types
      - Storage reports: Generate usage reports
      - Classification: Tag files based on content/properties
      - File management tasks: Automated file operations

11. **What is IIS? Which are the protocols that IIS supports?**
    - **IIS (Internet Information Services):** Microsoft's web server for Windows
    - **Supported Protocols:**
      - HTTP/HTTPS (web traffic)
      - FTP/FTPS (file transfer)
      - SMTP (email relay)
      - WebDAV (distributed authoring)
      - WebSocket protocol

12. **Explain the concept of Network Load Balancing (NLB).**
    - **NLB:** Distributes network traffic across multiple servers
    - **Features:**
      - High availability and scalability
      - No dedicated hardware required
      - Supports up to 32 nodes in cluster
      - Multiple distribution modes (unicast, multicast)
      - Application failover and load distribution

13. **What is PowerShell and what are the features of PowerShell?**
    - **PowerShell:** Task automation and configuration management framework
    - **Key Features:**
      - Object-oriented pipeline
      - Cmdlets (specialized .NET classes)
      - Scripting language with .NET integration
      - Remote management capabilities
      - Desired State Configuration (DSC)
      - Extensive module ecosystem

14. **What is Kerberos? How does Kerberos work?**
    - **Kerberos:** Network authentication protocol using tickets
    - **Authentication Process:**
      1. Client requests TGT from Authentication Server
      2. AS verifies credentials and issues TGT
      3. Client presents TGT to Ticket Granting Server
      4. TGS issues service ticket for specific resource
      5. Client presents service ticket to target server
      6. Server grants access to authenticated client

15. **What is difference between windows server 2016 and 2022?**
    - **Windows Server 2022 New Features:**
      - Enhanced security: Secured-core server, HTTPS and TLS 1.3 by default
      - Improved hybrid cloud: Azure Arc integration
      - Better container support: Smaller container images
      - Storage: Storage Migration Service improvements
      - Networking: UDP performance improvements, HTTP/2
      - Windows Admin Center enhancements
# Concepts of Operating System and Administration - Linux Answers (16-32)

16. **How to recover forgotten root password in Linux?**
    - **Method 1: Single User Mode**
      1. Reboot system and interrupt boot loader (press ESC/shift)
      2. Edit kernel parameters (add `single` or `init=/bin/bash`)
      3. Mount filesystem: `mount -o remount,rw /`
      4. Run `passwd` to change root password
      5. Reboot: `exec /sbin/init`
    - **Method 2: Live CD/USB**
      1. Boot from live media
      2. Mount root partition: `mount /dev/sda1 /mnt`
      3. Chroot: `chroot /mnt`
      4. Run `passwd` and change password

17. **How to create partition and Filesystem? Write Linux commands for it.**
    - **Create Partition:**
      ```bash
      fdisk /dev/sdb
      # Then: n (new), p (primary), 1 (partition number), specify size, w (write)
      ```
    - **Create Filesystem:**
      ```bash
      mkfs.ext4 /dev/sdb1    # For ext4
      mkfs.xfs /dev/sdb1     # For XFS
      ```

18. **Explain Linux Directory Structure in detail.**
    - **/:** Root directory
    - **/bin:** Essential user binaries
    - **/boot:** Boot loader files
    - **/dev:** Device files
    - **/etc:** Configuration files
    - **/home:** User home directories
    - **/lib:** Essential shared libraries
    - **/mnt:** Mount point for temporary filesystems
    - **/opt:** Optional application software
    - **/proc:** Process and kernel information
    - **/root:** Root user's home
    - **/sbin:** System administration binaries
    - **/tmp:** Temporary files
    - **/usr:** User utilities and applications
    - **/var:** Variable data (logs, spools)

19. **What is SSH? What is its default port? Why SSH is secure?**
    - **SSH (Secure Shell):** Protocol for secure remote access and file transfer
    - **Default Port:** 22
    - **Security Features:**
      - Encryption of all data (AES, 3DES, Blowfish)
      - Host authentication to prevent MITM attacks
      - User authentication (password, key-based)
      - Data integrity protection
      - Port forwarding capability

20. **Explain each field of /etc/passwd. What is /etc/shadow?**
    - **/etc/passwd Fields (colon-separated):**
      1. Username
      2. Password (x indicates shadowed)
      3. UID (User ID)
      4. GID (Group ID)
      5. GECOS (User information)
      6. Home directory
      7. Login shell
    - **/etc/shadow:** Secure file containing encrypted passwords and password aging information

21. **Why we use LVM in Linux & what are its benefits?**
    - **LVM (Logical Volume Manager):** Abstraction layer between physical storage and file systems
    - **Benefits:**
      - Flexible storage management
      - Online resizing of logical volumes
      - Snapshots for backups
      - Striping for performance
      - Mirroring for redundancy
      - Easy storage migration

22. **Explain Postfix Mail Server. What is default port used for postfix? What Is Dovecot? Can it be used with Postfix?**
    - **Postfix:** Open-source Mail Transfer Agent (MTA)
    - **Default Ports:** 25 (SMTP), 587 (Submission)
    - **Dovecot:** Open-source IMAP/POP3 server for mailbox access
    - **Integration:** Yes, Postfix handles mail delivery, Dovecot handles mailbox access

23. **What is mounting in Linux? Write a command to mount FAT formatted pen-drive in /mnt? How can you auto-mount it each time you boot the system?**
    - **Mounting:** Attaching a filesystem to the directory tree
    - **Mount Command:**
      ```bash
      mount -t vfat /dev/sdb1 /mnt
      ```
    - **Auto-mount:** Add to `/etc/fstab`:
      ```bash
      /dev/sdb1 /mnt vfat defaults 0 0
      ```

24. **What is hard link and symbolic link? How to create them?**
    - **Hard Link:** Direct reference to inode, same file with multiple names
      ```bash
      ln file1 file2_hardlink
      ```
    - **Symbolic Link:** Pointer to another file path
      ```bash
      ln -s file1 file2_symlink
      ```
    - **Differences:** Hard links can't cross filesystems, symlinks can; Hard links reference same inode, symlinks are separate files

25. **What is SELinux?**
    - **SELinux (Security-Enhanced Linux):** Mandatory Access Control system
    - **Features:**
      - Fine-grained access control policies
      - Process and file security contexts
      - Three modes: Enforcing, Permissive, Disabled
      - Prevents privilege escalation attacks

26. **What is NFS? What is root_squash?**
    - **NFS (Network File System):** Protocol for sharing files over network
    - **root_squash:** Security feature that maps root user (UID 0) from client to nobody user on server, preventing root access to shared files

27. **What is Network Information Service (NIS) in Linux?**
    - **NIS:** Client-server directory service protocol for distributing system configuration data
    - **Purpose:** Centralized management of users, groups, hosts across network
    - **Components:** NIS master server, NIS slave servers, NIS clients

28. **What is .bashrc and .profile in Linux?**
    - **.bashrc:** Bash configuration file executed for interactive non-login shells
    - **.profile:** User-specific environment and startup programs for login shells
    - **Usage:** .bashrc for aliases, functions; .profile for PATH, environment variables

29. **Explain Linux architecture. What is name of kernel?**
    - **Linux Architecture Layers:**
      1. Hardware
      2. Kernel (Linux kernel)
      3. Shell (Command interface)
      4. Applications/Utilities
    - **Kernel Name:** Linux kernel (monolithic kernel)

30. **What is user? What are groups? How to change the logged in user?**
    - **User:** Account with specific privileges and home directory
    - **Groups:** Collection of users with shared permissions
    - **Change User:**
      ```bash
      su - username        # Switch user with environment
      sudo -i              # Switch to root with sudo
      ```

31. **What is root user and general user? How to create a user? How to add user in group? How to change user's privileges?**
    - **Root User:** Superuser with full system access (UID 0)
    - **General User:** Regular user with limited privileges
    - **Create User:**
      ```bash
      useradd username
      passwd username
      ```
    - **Add to Group:**
      ```bash
      usermod -aG groupname username
      ```
    - **Change Privileges:** Use `sudo` configuration or change group membership

32. **What is default permission of directory and file? How to change it? What is umask in Linux?**
    - **Default Permissions:**
      - Files: 666 (rw-rw-rw-)
      - Directories: 777 (rwxrwxrwx)
    - **umask:** Value subtracted from default permissions
      - Common umask: 022 (results in files: 644, directories: 755)
    - **Change umask:**
      ```bash
      umask 0022
      ```

