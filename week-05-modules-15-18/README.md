# Week 5: Linux Security, Users, Permissions and Challenge Labs

## Overview

Week 5 was the final week of my Linux Essentials learning journey. The focus was on Linux user security, user and group administration, file ownership and permissions, special permissions, and practical system administration challenges.

This week helped me move from simply using Linux commands to understanding how a Linux administrator controls users, protects files, manages access, and automates repetitive tasks.

---

# Module 15: System and User Security

This module introduced Linux user and account security.

I learned that every Linux user has an account identified by a User ID (UID) and belongs to one or more groups identified by Group IDs (GIDs).

Important system files include:

```bash
/etc/passwd
/etc/shadow
/etc/group
```

`/etc/passwd` contains user account information, while `/etc/shadow` stores protected password information.

Useful commands included:

```bash
whoami
id
who
w
last
getent passwd username
getent group groupname
```

I also learned the difference between `su` and `sudo`. Using `sudo` allows an authorised user to execute administrative commands without permanently logging in as root.

---

# Module 16: Creating Users and Groups

This module focused on Linux account administration.

Important commands included:

```bash
groupadd
groupmod
groupdel
useradd
usermod
userdel
passwd
chage
```

Example:

```bash
sudo groupadd engineering
sudo useradd -m -s /bin/bash -g engineering enguser1
sudo passwd enguser1
```

The options used mean:

```text
-m            Create the user's home directory
-s /bin/bash  Assign Bash as the login shell
-g            Set the user's primary group
```

I also learned how to verify accounts using:

```bash
id username
getent passwd username
getent group groupname
```

---

# Module 17: Ownership and Permissions

Linux files and directories have both a user owner and a group owner.

I used:

```bash
ls -l
ls -ld
chown
chgrp
chmod
stat
```

Linux permissions are divided into:

```text
User   Group   Others
rwx    rwx     rwx
```

Where:

```text
r = Read
w = Write
x = Execute
```

Numeric permissions include:

```text
7 = rwx
6 = rw-
5 = r-x
4 = r--
0 = ---
```

For example:

```bash
chmod 770 directory
```

gives full access to the owner and group while giving no access to others.

I also practised changing ownership:

```bash
sudo chown username:groupname directory
```

---

# Module 18: Special Directories and Files

This module introduced special Linux permissions and links.

The three important special permissions were:

```text
setuid
setgid
sticky bit
```

The sticky bit is useful for shared directories because it helps prevent users from deleting files owned by other users.

Example:

```bash
chmod 1770 directory
```

I also learned about hard links and symbolic links.

Hard link:

```bash
ln original_file hard_link
```

Symbolic link:

```bash
ln -s original_file symbolic_link
```

A hard link points to the same inode as the original file, while a symbolic link points to the path of another file or directory.

---

# Challenge Lab 1: Department User and Permission Management

## Task

I configured a Linux server for three new departments:

```text
Engineering
Sales
IS
```

Each department required:

- One group
- One administrator
- Two normal users
- One department directory
- Appropriate ownership and permissions
- A confidential document

Groups were created using:

```bash
sudo groupadd engineering
sudo groupadd sales
sudo groupadd is
```

Users were created with Bash as their login shell and their department as their primary group.

Example:

```bash
sudo useradd -m -s /bin/bash -g engineering engadmin
sudo useradd -m -s /bin/bash -g engineering enguser1
sudo useradd -m -s /bin/bash -g engineering enguser2
```

Department directories were created:

```bash
sudo mkdir /engineering /sales /is
```

Ownership was assigned:

```bash
sudo chown engadmin:engineering /engineering
sudo chown salesadmin:sales /sales
sudo chown isadmin:is /is
```

Permissions were configured using:

```bash
sudo chmod 3770 /engineering /sales /is
```

The configuration provided full access to the department administrator and group, no access to outsiders, group inheritance using setgid, and deletion protection using the sticky bit.

Confidential files used:

```bash
chmod 640 confidential.txt
```

This allowed the administrator to read and modify the file, department members to read it, and everyone else to have no access.

Verification commands included:

```bash
getent group engineering
id engadmin
ls -ld /engineering
ls -l /engineering/confidential.txt
```

---

# Challenge Lab 2: Automated User Management Bash Script

The second challenge was to automate user and group administration.

Instead of manually entering several commands for every new employee, I created a Bash script that:

- Accepts any group name
- Checks whether the group already exists
- Creates the group if it is unique
- Accepts any username
- Checks whether the username already exists
- Creates the user with Bash
- Assigns the user's primary group
- Creates a password
- Creates a directory under `/`
- Assigns ownership
- Configures permissions
- Verifies the final configuration

Duplicate groups were checked using:

```bash
getent group "$groupname"
```

Duplicate users were checked using:

```bash
getent passwd "$username"
```

The script also used:

```bash
$?
```

to check whether the previous command executed successfully.

The script was made executable using:

```bash
chmod +x user_management.sh
```

and executed with:

```bash
sudo ./user_management.sh
```

This challenge demonstrated how Bash scripting can make Linux administration faster, repeatable, and less prone to manual errors.

---

# Challenge Lab 3: Archiving Linux Log Files

The objective was to preserve `.log` files from `/var/log`.

The required directories were created:

```bash
mkdir -p ~/archive ~/backup
```

I moved to the log directory:

```bash
cd /var/log
```

The files were archived using:

```bash
sudo tar -cvf ~/archive/log.tar *.log
```

The archive contents were checked without extracting them:

```bash
tar -tf ~/archive/log.tar
```

The files were then extracted into the backup directory:

```bash
tar -xf ~/archive/log.tar -C ~/backup
```

Finally, I verified the result:

```bash
ls ~/backup
```

This challenge provided practical experience with Linux backup and archive operations using `tar`.

---

# Challenge Lab 4: Extracting Unique Linux Service Names

The final challenge involved processing `/etc/services` without creating intermediary files.

The command used was:

```bash
grep -E '^[A-Za-z]' /etc/services | awk '{print $1}' | sort -u > ~/uniqueservices.txt && wc -l ~/uniqueservices.txt
```

This command combines several Linux tools.

```text
grep       Filters valid service lines
awk        Extracts the service name
sort -u    Sorts and removes duplicates
>          Saves the final output
&&         Runs the next command only if the previous command succeeds
wc -l      Counts the resulting service names
```

The result was verified using:

```bash
head ~/uniqueservices.txt
tail ~/uniqueservices.txt
```

This challenge strengthened my understanding of pipes, redirects, text processing, sorting, and conditional command execution.

---

# Key Commands Practised

```bash
whoami
id
getent
groupadd
useradd
usermod
passwd
mkdir
ls
chown
chgrp
chmod
tar
grep
awk
sort
wc
head
tail
ln
ln -s
```

---

# Key Lessons from Week 5

By completing Week 5, I gained practical experience in:

- Managing Linux users and groups
- Assigning primary groups
- Understanding UID and GID information
- Managing file and directory ownership
- Applying symbolic and numeric permissions
- Protecting shared directories
- Using special permissions
- Creating hard and symbolic links
- Automating administrative tasks using Bash
- Creating and extracting archives
- Processing text using pipes and redirects
- Verifying system configurations before considering a task complete

---

# Final Reflection

Week 5 brought together many of the concepts covered throughout the Linux Essentials programme.

The challenge labs were particularly useful because they required me to combine several Linux commands to solve realistic administrative problems rather than using each command independently.

I am now more comfortable working with Linux users, groups, permissions, directories, Bash scripts, archives, and command-line text processing. I also better understand the importance of verifying every administrative change after making it.

This final week strengthened my foundation for further learning in Linux system administration, cloud computing, DevOps, and infrastructure management.
