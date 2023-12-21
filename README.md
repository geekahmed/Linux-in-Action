# Linux in Action

This is my summary of the Linux in Action, by David Clinton. This book is considered a great introduction to linux adminstartion with practical exercises as found in the real-world projects.

Contributions: Issues, comments and pull requests are super welcome 😃

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->
# Table of Contents
- [Linux in Action](#linux-in-action)
- [Table of Contents](#table-of-contents)
- [Chapter 1. Welcome to Linux](#chapter-1-welcome-to-linux)
- [Chapter 2. Linux virtualization: Building a Linux working environment](#chapter-2-linux-virtualization-building-a-linux-working-environment)
- [Chapter 3. Remote connectivity: Safely accessing networked machines](#chapter-3-remote-connectivity-safely-accessing-networked-machines)
    - [Section 1: The importance of encryption](#section-1-the-importance-of-encryption)
    - [Section 2: Getting started with OpenSSH](#section-2-getting-started-with-openssh)
    - [Section 3: Logging in to a remote server with SSH](#section-3-logging-in-to-a-remote-server-with-ssh)
	- [Section 4: Password-free SSH access](#section-4-password-free-ssh-access)
	- [Section 5: Safely copying files with SCP](#section-5-safely-copying-files-with-scp)
	- [Section 6: Using remote graphic programs over SSH connections](#section-6-using-remote-graphic-programs-over-ssh-connections)
	- [Section 7: Linux process management](#section-7-linux-process-management)
	- [Security best practices](#security-best-practices)
	- [Command-line review](#command-line-review)
- [Chapter 4. Archive management: Backing up or copying entire file systems](#chapter-4-archive-management-backing-up-or-copying-entire-file-systems)
	- [Section 1: Why archive?](#section-1-why-archive)
	- [Section 2: What to archive?](#section-2-what-to-archive)
	- [Section 3: Where to back up?](#section-3-where-to-back-up)
	- [Section 4: Archiving files and file systems using tar](#section-4-archiving-files-and-file-systems-using-tar)
	- [Section 5: Archiving partitions with dd](#section-5-archiving-partitions-with-dd)
	- [Section 6: Synchronizing archives with rsync](#section-6-synchronizing-archives-with-rsync)
	- [Section 7: Planning considerations](#section-7-planning-considerations)
	- [Security best practices](#security-best-practices-1)
	- [Command-line review](#command-line-review-1)
- [Chapter 5. Automated administration: Configuring automated offsite backups](#chapter-5-automated-administration-configuring-automated-offsite-backups)
	- [Section 1: Scripting with Bash](#section-1-scripting-with-bash)
	- [Section 2: Backing up data to AWS S3](#section-2-backing-up-data-to-aws-s3)
	- [Section 3: Scheduling regular backups with cron](#section-3-scheduling-regular-backups-with-cron)
	- [Section 4: Scheduling irregular backups with anacron](#section-4-scheduling-irregular-backups-with-anacron)
	- [Section 5: Scheduling regular backups with systemd timers](#section-5-scheduling-regular-backups-with-systemd-timers)
	- [Security best practices](#security-best-practices-2)
	- [Command-line review](#command-line-review-2)
<!-- /TOC -->

# Chapter 1. Welcome to Linux
- Linux use pseudo file systems to expose data on the hardware environment to processes and users.
- Authorized users can invoke `sudo` to gain administration persmissions for individual commands.
- A file system is made up of data files indexed in a way that allows the perception of a directory-based organization.
- A process is an active instance of a running software program.
- A disk partition is the logical devision of a physical storage device that can be made to work excatly like a standalone device.
- Bash is a command-line user interface for executing system actions.
- Plain text that is usable for administration purposes is text made up of a limited set of characters and contains no extraneous formatting code.
- File globbing involves using wildcard characters to refer to multiple files with a single command.
- Tab completion employs the Tab key to suggest possible completions of a partially typed command.
- Pseudo file systems are directories containing files with dynamic data automatically generated at or after system boot.
- Avoid working on linux machine as the root user. Use a regular user account instead, and, when you need to perform administation tasks, use `sudo`.
- `ls -lh /var/log` lists the contents and full, human-friendly details of the `/var/log` directory.
- `cd` returns you to your home directory.
- `cp file1 newdir` copies a file called `file1` to the directory named `newdir`.
- `mv file? /some/other/directory/` moves all files containing the letter `file` and one more character to the target location.
- `rm -r *` deletes all files and directories beneath the current location.
- `man sudo` opens the man documentation file on using `sudo` with commands.
# Chapter 2. Linux virtualization: Building a Linux working environment

- Hypervisors like VirtualBox provide an environment where virtual operating systems can safely access hardware resources, whereas lightweight containers share their host’s software kernel.
- Linux package managers like APT and RPM (Yum) oversee the installation and administration of software from curated online repositories using regularly updated index that mirrors the state of the remote repository.
- Getting a VM going in VirtualBox requires defining its virtual hardware environment, downloading an OS image, and installing the OS on your VM.
- You can easily clone, share, and administer VirtualBox VMs from the command line.
- LXC containers are built on predefined, distribution-based templates.
- LXC data is stored within the host file system, making it easy to administer containers.
- Virtualization is the logical sharing of compute, storage, and networking resources among multiple processes, allowing each to run as if it was a standalone physical computer.
- A hypervisor is software running on a host machine that exposes system resources to a guest layer, allowing the launching and administration of full-stack guest VMs.
- A container is a VM that, instead of full-stack, lives on top of (and shares) the host machine’s core OS kernel. Containers are extremely easy to launch and kill, according to short-term need.
- A dynamically allocated virtual drive in VirtualBox takes up only as much space on your physical drives as the VM actually uses. A fixed-size disk, by contrast, takes up the maximum space no matter how much data is there.
- A software repository is a location where digital resources can be stored. Repositories are particularly useful for collaboration and distribution of software packages.
- Allowing an official package manager to install and maintain the software on your Linux system is preferred over doing it manually. Online repositories are much more secure, and downloading is properly encrypted.
- Always scan the checksum hashes of downloaded files against the correct hash strings, not only because packages can be corrupted during download, but because they can also sometimes be switched by man-in-the-middle attackers.
- `apt install virtualbox` uses APT to install a software package from a remote repository.
- `dpkg -i skypeforlinuz-64.deb` directly installs a downloaded Debian package on a Ubuntu machine.
- `wget https://example.com/document-to-download` uses the wget command- line program to download a file.
- `dnf update` , `yum update` , or `apt update` syncs the local software index with what’s available from online repositories.
- `shasum ubuntu-16.04.2-server-amd64.iso` calculates the checksum for a
downloaded file to confirm that it matches the provided value. This means that the contents haven’t been corrupted in transit.
- `vboxmanage clonevm Kali-Linux-template --name newkali` uses the vboxmanage tool to clone an existing VM.
- `lxc-start -d -n myContainer` starts an existing LXC container.
- `ip addr` displays information on each of a system’s network interfaces (including their IP addresses).
- `exit` leaves a shell session without shutting down the machine.
- `shutdown -h now` It shutdowns the operating system immediately.
- `sudo su` makes the shell in the sudo mode to write the commands that needs `sudo` without writing `sudo` everytime.
- By default, `/var/lib/lxc/` directory contains the container's file system.
- The backslash character (\\) can be used to conveniently break a long command into multiple lines on the command line.
-  `APT` systems let you directly search for the availability of packages using `apt search` command.
-  The package manager, which comes with Linux by default, has a number of jobs:
   -  Maintain a local index to track repositories and their contents.
   -  Tracks the status of all the software that's installed on your local machine.
   -  Ensures that all available updates are applied to installed software.
   -  Ensures that software dependencies are met for new applications before they are installed.
   -  Handles installing and removing softwar packages.
-  Here are some basic guidelines for choosing virtualization technologies:
   -  Full-sized hypervisors like Xen and KVM are normally used for enterprise-sized deployments involving large fleets of Linux VMs.
   -  VirtualBox and VMWare's Player are perfect for testing and experimenting with live operating systems, on or two at a time, without the need to install them to actual PCs. Their relatively high overhead makes them unsuitable for most production environments.
   -  Container technologies like LXC and Docker are lightweight and can be provisioned and launched in mere seconds.
  
# Chapter 3. Remote connectivity: Safely accessing networked machines
## Section 1: The importance of encryption
- Telnet is a network protocol used on the Internet or local area networks to provide a bidirectional interactive text-oriented communication facility using a virtual terminal connection. It was historically one of the earliest methods for remote terminal access to computers and networking devices.
- Telnet Protocol: Telnet uses the Telnet protocol to establish a connection between a client (local machine) and a server (remote machine) over a TCP/IP network. 
  - It establishes the connection using port 23 or 2323.
- Client-Server Model: Telnet follows a client-server model. The client initiates a connection to the server, and once the connection is established, the server provides a virtual terminal on the client's machine.
- Text Transmission: Telnet transmits data, including keyboard input and output, in plain text. It is a simple, text-oriented protocol without encryption or security features.
- Remote Terminal Access: One of the primary use cases for Telnet is remote terminal access. It allows users to log in to a remote system as if they were physically present at that system's terminal.
- Network Configuration and Troubleshooting: Telnet is often used for configuring and troubleshooting network devices, such as routers and switches. It allows network administrators to connect to these devices remotely and make configuration changes.
- Testing Network Services: Telnet is used to test the accessibility of network services such as web servers, mail servers, and FTP servers. For example, you can use Telnet to check if a web server is responding by connecting to it on port 80.
- Unencrypted Communication: Telnet transmits data in plain text, including usernames and passwords. This lack of encryption poses a security risk, especially when used over untrusted networks like the Internet.
- SSH (Secure Shell): Due to security concerns with Telnet, Secure Shell (SSH) has largely replaced Telnet for remote terminal access. SSH encrypts the communication between the client and server, providing a more secure alternative.
- An encryption key is a small file containing random sequence of characters. This key can be applied as part of an encryption algorithm to convert plain text, readable data into what amounts to total gibberish.
  - The encryption key can be used to reverse this operation and decrypt the data to its real meaning.

## Section 2: Getting Started with OpenSSH
- The `dpkg` command-line tool manages and quries software packages that are part of the Advanced Package Tool (APT) system.
  - Running `dpkg` with `-s` flag and the name of the package returns the current installed and update status.
- The server version of the openssh includes all the tools in the client package.

## Section 3: Logging in to a remote server with SSH

- `ping {ip}` is used to check if two computers can talk to each other.


## Section 4: Password-free SSH access

 - Passwords are not the best choice for protection as they are either
    too short and/or easy to guess.
 - AWS disables password authentication by default on their cloud
    instances.
 - `/etc/ssh/sshd_config` is the configuration file whose settings control how remote clients will be able to log in to youe machine.
 - `/etc/ssh/ssh_config` is the configuration file whose settings control how users in this machine will log in to remote hosts as clients. 
 - You can enable password-free SSH access by sharing the public key of a key pair.
 - A password is a string of regular characters, while a passphrase can include spaces and punctuation.
 - `ssh-keygen` program is used in generating public/private key pair.
 - The fingerprint and randomart are used in preventing man-in-the-middle attacks.
 - Besides RSA, OpenSSH supports the ECDSA and ED25519 signature algorithms.
 - Public and private keys are a fundamental concept in asymmetric cryptography, which is widely used for secure communication and digital signatures. 
 - It doesn't matter where a key pair was generated as long as the client has access to a copy of the private key, and the server holds a copy of the public key.
   - It is generally safer tp generate key pairs on the client, as the private keys never have to be copied across the network.
 - Passwordless SSH access does not work until copying the public key over to the host.
	 - The Mechanism of the last point
		 - Generate key pair (Client PC).
		 - Transfer public key to host.
		 - Private key used to sign a challenge and generate a message.
		 - Message transfered to host PC
		 - Message authenticity verified using public key, and access is granted
 - We could build different collections of key for different hosts and specify a key to ssh using `-i` flag and providing the private key path.
   - `ssh -i .ssh/myKey.pem ubutu@192.168.2.2` 
## Section 5: Safely copying files with SCP
 - The cp command is not suitable for copying files accross network as the file contents  would be exposed to anyone else who happened to be hanging around the network that day, or anyone who happened to be browsing through network log data some time later.
 - The SCP program copies files of any sort hither and yon using the SSH protocol for file transfer, relying on all the same keys, passwords, and passphrases.
 - The `ssh-copy-id` command is used to safely copy the public key to a remote host.
 - `rsync` is a widely used command-line utility for data synchronization and file transfer between systems. 
 - The difference between `scp` and `rsync` is mainly about the effieciency of file transfers.
## Section 6: Using remote graphic programs over SSH connections
 - The OpenSSH package also allows for secure file copying and remote
     graphic sessions.
 - X11 forwarding allows graphic programs to be run over a remote
     connection.
## Section 7: Linux process management
 - A process is an instance of a running software program.
 - An operating system is a tool for organizing and managing those instances/processes to effectively use a computer's hardware resources.
 - The first process to wake up and get everything else going when a Linux compuer boots is called init.
 - A parent shell is shell environment from within which new (child) shells can subsequently be launched and through which programs run.
 - `pstree -p` visualizes parent and child shells/processes.
 - The `file` command in Linux is used to determine the type of a file.
 - `systemd` primary role is to control the ways individual processes are born, live their lives, and then die.
 - On most modern Linux distributions, processes are managed by systemd through the systemctl tool.
 - You can pipe data between commands using the | (pipe) character and filter streaming data with grep.
 - A Linux process is all the ongoing activity that’s associated with a single running program.
 - A shell is a terminal environment that provides a command-line interpreter (like Bash) to allow a user to execute commands. When you’re working from a Linux desktop PC or laptop, you’ll generally access a shell by opening a terminal program (like GNOME Terminal).
 - A parent shell is an initial environment, from within which new child shells can subsequently be launched and through which programs run. A shell is, for all intents and purposes, also a process.
## Security best practices
 - Always encrypt remote login sessions running over a public network.
 - Avoid relying on passwords alone; like people, they’re fallible.
 - Key-based, passwordless SSH sessions are preferable to simple password logins.
 - Never transfer files across public networks in plain text.
## Command-line review
 - `dpkg -s openssh-client` checks the status of an APT-based software
   package.
 - `systemctl status ssh` checks the status of a system process (systemd).
 - `systemctl start ssh` starts a service.
 - `ip addr` lists all the network interfaces on a computer.
 - `ssh-keygen` generates a new pair of SSH keys.
 - `cat .ssh/id_rsa.pub | ssh ubuntu@10.0.3.142 "cat >>
   .ssh/authorized_keys"` copies a local key and pastes it on a remote
   machine.
 - `ssh-copy-id -i .ssh/id_rsa.pub ubuntu@10.0.3.142` safely copies
   encryption keys (recommended and standard).
 - `ssh -i .ssh/mykey.pem ubuntu@10.0.3.142` specifies a particular key
   pair.
 - `scp myfile ubuntu@10.0.3.142:/home/ubuntu/myfile` safely copies a
   local file to a remote computer.
 - `ssh -X ubuntu@10.0.3.142` allows you to log in to a remote host for
   graphics-enabled session.
 - `ps -ef | grep init` displays all currently running system processes
   and filters results using the string init.
 - `pstree -p` displays all currently running system processes in a visual
   tree format.

# Chapter 4. Archive management: Backing up or copying entire file systems

## Section 1: Why archive?
 - What is archive?
	- A single file containing a collection of objects: files, directories, or a combination of both.
	- Importance of bundling objects within a single file
		- Facilitate moving, sharing, and storing multiple objects.
 - Compression is a software tool that applies an algorithm to a file or archive to reduce the amount of disk space it takes.
	- Compression can reduce transmission times significantlry and also saves bandwidth if the transmission over the network.
 - Reasons to create archives
	- Build reliable file system images.
		- Like .ISO files, which are images for complete OS specially organized to make it easy to copy the included files to a target computer.
		- Use cases:
			- Providing identical system setup to multiple users.
			- Rescue a complex installation from a failing hard drive. 
	- Create efficient data backups.
		- Backups protect from:
			- Hardware failure.
			- Mistakes in configurations files.
			- Insecure public cloud.
			- Ransomware.
		- Generating and monitoring log messages can help you spot the problems in untested backup.
			- A solution is to make a trial restore for the data on a matching machine.
## Section 2: What to archive?
 - Pseudo file systems aren't actually saved to disk but live in volatile memory and disappear when the machine shuts down.
 - Running `df` on an LXC container displays the partitions associated with LXC host.
## Section 3: Where to back up?
 - We could back-up files on:
	- Tape drives.
	- USB-mounted SATA storage drives.
	- Network-attached storage (NAS).
	- Storage area networkd (SAN).
	- Cloud storage solution.
 - Back-ups best practices:
	- Reliable: Using only storage media that are reasonably likely to retain their integrity for the length of time you intend to use them.
	- Tested: Test restoring as many archive runs as possible in simulated production environments.
	- Rotated: Maintain at least a few historical archives older than the current backup in case the latest one should somehow fail.
	- Ditributed: Make sure that at least some of your archives are stored in a physically remote location. In case of fire or other disaster.
	- Secure: Never expose your data to insecure networks or storage sites at any time during the process.
	- Compliant: Honor all relevant regulatory and industry standards at all times.
	- Up to date: What's the point keeping archives that are weeks or months behind the current live version?
	- Scripted: Never rely on a human being to remember to perform an ongoing task. Automte it.
## Section 4: Archiving files and file systems using tar
 - To create an archive:
	- Find and identify the files you want to include.
	- Identify the location on a storage drive that you want your archive to use.
	- Add your files to an archive, and save it to its storage location.
 - The tar command will never move or delete any of the original directories and files you feed it; it only makes archives copies.
	- Usinf a (.) instead of (*) in the command will include even the hidden files in the archive.
 - Streaming file system archive avoids the overhead of a middle step which is storing a local copy of the archive.
 - The find command searches through a file system looking for objects that match provided rules.
 - Locate command runs the search string on a pre-existing index which is updated on system boot or manullly using updatedb.
 - Permissions are the attributes assigned to an object that determine who may see it and how.
 - Permissions numeric representation:
	- Read
		- Character: r
		- Number: 4
	- Write
		- Character: w
		- Number: 2
	- Execute
		- Character: x
		- Number: 1
 - A group is an account used to manage permissions for multiple users.
 - Ownership is the owner and group that have authority over an object.
 - Only users with administrator powers can work with resources in other users' accounts.
 - Using sudo on archiving and extracting commands in order to restore the ownership of each archived file.
## Section 5: Archiving partitions with dd
 - Using dd command can make perfect byte-for-byte images of just about anything digital.
 - dd command needs some thinking before hiiting return key as any mistake may wipe the whole drive.
## Section 6: Synchronizing archives with rsync
 - rsync is used to synhcronize a directory on local or remote server.
 - rsync -av * "remote target"
	- -a argument means to syncronize recursively.
## Section 7: Planning considerations
 - Questions to ask while planning backup strategy
	- How often should you create new archives, and how long will you retain old copies?
	- How many layers of validation will you build into your backup process?
	- How many concurrent copies of your data will you maintain?
	- How important is maintaining geographically remote archives?
	- Should you consider incremental or diffrential backups?
## Security best practices
 - Create an automated, reliable, tested, and secure recurring process
   for backing up all of your important data.
 - Where appropriate, separate file systems with sensitive data by
   placing them on their own partitions and mounting them to the file
   system at boot time.
 - Always ensure that file permissions are accurate, and allow only the
   least access necessary.
 - Never assume the data on an old storage drive is truly deleted.
## Command-line review
- `df -h` displays all currently active partitions with sizes shown in a human readable format.
- `tar czvf archivename.tar.gz /home/myuser/Videos/*.mp4` creates a compressed archive from video files in a specified directory tree.
- `split -b 1G archivename.tar.gz archivename.tar.gz.part` splits a large file into smaller files of a set maximum size.
- `find /var/www/ -iname "*.mp4" -exec tar -rvf videos.tar {} \;` finds files meeting a set criteria and streams their names to tar to include in an archive.
- `chmod o-r /bin/zcat` removes read permissions for others.
- `dd if=/dev/sda2 of=/home/username/partition2.img` creates an image of the sda2 partition and saves it to your home directory.
- `dd if=/dev/urandom of=/dev/sda1` overwrites a partition with random characters to obscure the old data.
- `rsync -av * username@10.0.3.141:syncdirectory` synchronizes recursively a folder in remote machine with local one.

# Chapter 5. Automated administration: Configuring automated offsite backups
## Section 1: Scripting with Bash
 - A linux script is a plain text file containing one or more commands compliant with Bash.
	- Important in creating executable routines that can rival programming languages in complexity and versatility.
 - The # charavter in shell scripting introduces a comment that wouldn't be read by the interpreter.
	- Using ! character besides the # character will make the interpreter read the value of the comment (shebang line).
 - Exit codes are passed when a Linux command completes. A 0 will be pased to indicate success, whereas different numbers can be configured to specify some kind of error.
 - Cron, by default, will always run as root.
 - Scripts saved to the /etc/cron.daily/ directory will be executed each day.
## Section 2: Backing up data to AWS S3
 - AWS S3 is widely used between Linux administrators.
 - AWS CLI is used to interact with AWS from the terminal.
 - `aws configure` command is used to add the account credentials.
 - `aws s3 ls` command is used to show all  S3 buckets in the aws account.
 - A new s3 bucket is creates using `aws s3 mb "name of the bucket"`
	- The bucket name should be unique in the entire S3 system.
 - `aws sync sourcePath s3://"bucket name"` command is used to backup files and directories to the S3 bucket and is similar to rsync.
 - To write backup using shell scripting

    #!/bin/bash
    /usr/local/bin/aws s3 sync /home/geekahmed/test s3://geekahmed12345
 - `whereis aws` command is used to find the location of aws cli.
## Section 3: Scheduling regular backups with cron
 - Copying an executable script to one of the /etc/cron.? directories causes it to be run at the appropriate interval.
## Section 4: Scheduling irregular backups with anacron
 - Adding a directive to the anacrontab file executes commands relative to system boots, rather than at absolute times.
## Section 5: Scheduling regular backups with systemd timers
 - systemd timers can be set to run based on both absolute time and in reaction to system events, like changes to hardware states.
## Security best practices
 - Lock down your system accounts (like syslog and, ideally, even root) to prevent their being used for remote logins.
 - Include off-site backups in your security planning, which adds another layer of data reliability.
 - Always protect your (AWS) access keys, not to mention passwords and encryption key pairs, from public exposure of any kind.
## Command-line review
 - `#!/bin/bash` (the so-called “shebang line”) tells Linux which shell interpreter you’re going to be using for a script.
 - `||` inserts an or condition into a script. Think of this as either “the command to the left is successul” or “execute the command to the right.”
 - `&&` - inserts an and condition into a script. Think of this as “if the command to the left is successful” and “execute the command to the right.”
 - `test -f /etc/filename` tests for the existence of the specified file or directory name.
 - `chmod +x upgrade.sh` makes a script file executable.
 - `pip3 install --upgrade --user awscli` installs the AWS command-line interface using Python’s pip package manager.
 - `aws s3 sync /home/username/dir2backup s3://linux-bucket3040` synchronizes the contents of a local directory with the specified S3 bucket.
 - `21 5 * * 1 root apt update && apt upgrade` (a cron directive) executes two apt commands at 5:21 each morning.
 - `NOW=$(date +"%m_%d_%Y")` assigns the current date to a script variable.
 - `systemctl start site-backup.timer` activates a systemd system timer.
