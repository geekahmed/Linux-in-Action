

This is my summary of the Linux in Axction, by David Clinton. This book is considered a great introduction to linux adminstartion with practical exercises as found in the real-world projects.

Contributions: Issues, comments and pull requests are super welcome 😃

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->
# Table of Contents
- [Table of Contents](#table-of-contents)
- [Chapter 1. Welcome to Linux]()
	- [1.-What makes Linux different from other operarting systems]()
	- [2.-Basic survival skills]()
	- [3.-Getting help]()
- [Chapter 2. Linux virtualization: Building a Linux working environment]()
	- [1.-What is virtualization?]()
	- [2.-Working with VirtualBox]()
	- [3.-Working with Linux containers (LXC)]()
- [Chapter 3. Remote connectivity: Safely accessing networked machines](#Chapter-3-Remote-connectivity-Safely-accessing-networked-machines)
	- [1.-The importance of encryption]()
	- [2.-Getting started with OpenSSH]()
	- [3.-Logging in to a remote server with SSH]()
	- [4.-Password-free SSH access]()
	- [5.-Safely copying files with SCP]()
	- [6.-Using remote graphic programs over SSH connections]()
	- [7.-Linux process management]()
- [Chapter 4. Archive management: Backing up or copying entire file systems](#Chapter-4-Archive-management-Backing-up-or-copying-entire-file-systems)
	- [1.-Why archive?]()
	- [2.-What to archive]()
	- [3.-Where to back up]()
	- [4.-Archiving files and file systems using tar]()
	- [5.-Archiving partitions with dd]()
	- [6.-Synchronizing archives with rsync]()
	- [7.-Planning considerations]()
<!-- /TOC -->

# Chapter 1. Welcome to Linux

# Chapter 2. Linux virtualization: Building a Linux working environment

# Chapter 3. Remote connectivity: Safely accessing networked machines
## Section 4: Password-free SSH access

 - Passwords are not the best choice for protection as they are either
    too short and/or easy to guess.
 - AWS disables password authentication by default on their cloud
    instances.
 - You can enable password-free SSH access by sharing the public key of a key pair.
 - A password is a string of regular characters, while a passphrase can
    include spaces and punctuation.
 - ssh-keygen program is used in generating public/private key pair.
 - The fingerprint and randomart are used in prevening
    man-in-the-middle attacks.
 - Besides RAS, OpenSSH supports the ECDSA and ED25519 signature
    algorithms.
 - Passwordless SSH access does not work until copying the public key
    over to the host.
	 - The Mechanism of the last point
		 - Generate key pair (Client PC).
		 - Transfer public key to host.
		 - Private key used to sign a challenge and generate a message.
		 - Message transfered to host PC
		 - Message authenticity verified using public key, and access is granted
 - We could build different collections of key for different hosts and
     specify a key to ssh using -i flag and providing the private key
     path
## Section 5: Safely copying files with SCP
 - The cp command is not suitable for copying files accross network as the file contents  would be exposed to anyone else who happened to be hanging around the network that day, or anyone who happened to be browsing through network log data some time later.
 - The SCP program copies files of any sort hither and yon using the SSH protocol for file transfer, relying on all the same keys, passwords, and passphrases.
 - The ssh-copy-id command is used to safely copy the public key to a remote host.
## Section 6: Using remote graphic programs over SSH connections
 - The OpenSSH package also allows for secure file copying and remote
     graphic sessions.
 - X11 forwarding allows graphic programs to be run over a remote
     connection.
## Section 7: Linux process management
 - On most modern Linux distributions, processes are managed by
     systemd through the systemctl tool.
 - You can pipe data between commands using the | (pipe) character and filter streaming data with grep.
 - A Linux process is all the ongoing activity that’s associated with
     a single running program.
 - A shell is a terminal environment that provides a command-line
     interpreter (like Bash) to allow a user to execute commands. When
     you’re working from a Linux desktop PC or laptop, you’ll generally
     access a shell by opening a terminal program (like GNOME Terminal).
 - A parent shell is an initial environment, from within which new
     child shells can subsequently be launched and through which
     programs run. A shell is, for all intents and purposes, also a
     process.
## Security best practices
 - Always encrypt remote login sessions running over a public network.
 - Avoid relying on passwords alone; like people, they’re fallible.
 - Key-based, passwordless SSH sessions are preferable to simple
   password logins.
 - Never transfer files across public networks in plain text.
## Command-line review
 - dpkg -s openssh-client checks the status of an APT-based software
   package.
 - systemctl status ssh checks the status of a system process (systemd).
 - systemctl start ssh starts a service.
 - ip addr lists all the network interfaces on a computer.
 - ssh-keygen generates a new pair of SSH keys.
 - $ cat .ssh/id_rsa.pub | ssh ubuntu@10.0.3.142 "cat >>
   .ssh/authorized_keys" copies a local key and pastes it on a remote
   machine.
 - ssh-copy-id -i .ssh/id_rsa.pub ubuntu@10.0.3.142 safely copies
   encryption keys (recommended and standard).
 - ssh -i .ssh/mykey.pem ubuntu@10.0.3.142 specifies a particular key
   pair.
 - scp myfile ubuntu@10.0.3.142:/home/ubuntu/myfile safely copies a
   local file to a remote computer.
 - ssh -X ubuntu@10.0.3.142 allows you to log in to a remote host for
   graphics-enabled session.
 - ps -ef | grep init displays all currently running system processes
   and filters results using the string init.
 - pstree -p displays all currently running system processes in a visual
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
