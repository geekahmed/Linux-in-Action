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
<!-- /TOC -->

# Chapter 1. Welcome to Linux

# Chapter 2. Linux virtualization: Building a Linux working environment

# Chapter 3. Remote connectivity: Safely accessing networked machines
## Section 4: Password-free SSH access

 - Passwords are not the best choice for protection as they are either
    too short and/or easy to guess.
 - AWS disables password authentication by default on their cloud
    instances.
 - You can enable password-free SSH access by sharing the public key of
    a key pair.
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
 A- Generate key pair (Client PC)
 B- Transfer public key to host
 C- Private key used to sign a challenge and generate a message
 D- Message transfered to host PC
 E- Message authenticity verified using public key, and access is granted  
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
 - You can pipe data between commands using the | (pipe) character and
     filter streaming data with grep.
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
