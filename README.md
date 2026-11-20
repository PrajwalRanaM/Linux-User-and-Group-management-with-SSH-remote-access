# Linux-User-and-Group-management-with-SSH-remote-access Lab

## Overview

This lab demonstrates basic Linux user and group administration using a Kali Linux virtual machine.

The original exercise involved creating a Linux group, creating a user account within that group, setting the user's password, examining Linux account and authentication files, and switching to the newly created account.

As an additional practical step, I configured **PuTTY** to remotely access the Kali Linux virtual machine over SSH. This extended the lab from local terminal administration to remote Linux administration.

## Objectives

- Create a Linux group
- Create a new Linux user account
- Add the user to a specific group
- Configure the user's password
- Verify the group and user entries
- Examine `/etc/group`
- Examine `/etc/passwd`
- Examine `/etc/shadow`
- Switch between Linux users
- Verify the active user
- Remotely access the Kali VM using PuTTY and SSH

## Lab Environment

- **Operating System:** Kali Linux
- **Virtualisation:** Virtual Machine
- **Remote client:** PuTTY
- **Remote protocol:** SSH
- **Linux group:** `hq_admins`
- **Linux user:** `ufour`

## Part 1 — Create the Linux Group

The following command was used to create the `hq_admins` group:

```bash
sudo groupadd hq_admins
```

The group was then verified using:

```bash
tail /etc/group
```

This allowed me to confirm that `hq_admins` had been created and assigned a group ID (GID).

## Part 2 — Create the Linux User

A new user named `ufour` was created with a home directory and assigned to the `hq_admins` group:

```bash
sudo useradd ufour -m -g hq_admins
```

The `-m` option creates a home directory for the user, while `-g` assigns the user's primary group.

## Part 3 — Configure the Password

A password was assigned to the new account:

```bash
sudo passwd ufour
```

For this practice lab, the password specified by the exercise was used.

> **Security note:** Real production systems should follow an organisation's password policy and should never use simple lab passwords.

## Part 4 — Verify the User Account

The `/etc/passwd` file was checked:

```bash
sudo tail /etc/passwd
```

This confirmed that `ufour` was registered as a Linux user.

## Part 5 — Examine `/etc/shadow`

The following command was used:

```bash
sudo tail /etc/shadow
```

The `ufour` account was visible in the file, including password-related information.

The `/etc/shadow` file contains sensitive authentication information and should be protected from unauthorised access.

## Part 6 — Switch to the New User

The newly created account was accessed using:

```bash
su - ufour
```

The `-` performs a full login and loads the user's login environment.

The active account was then verified:

```bash
whoami
```

The expected result was:

```text
ufour
```

The session was then exited using:

```bash
exit
```

## Part 7 — Remote Access Using PuTTY

### Why PuTTY was added

The original exercise was performed through the Kali VM's terminal. To make the lab more representative of real-world Linux administration, I additionally configured **PuTTY** on the host machine to remotely connect to the Kali VM using SSH.

This demonstrated how an administrator can manage a Linux system without directly interacting with the VM's graphical console.

### SSH connection

The Kali VM was configured to accept SSH connections, and PuTTY was used as the SSH client.

The connection process involved:

1. Identifying the Kali VM's IP address.
2. Opening PuTTY on the host machine.
3. Entering the Kali VM's IP address.
4. Selecting **SSH** as the connection type.
5. Connecting to the SSH service.
6. Logging in with a valid Linux account.
7. Running Linux commands through the remote terminal.

After establishing the connection, the same Linux administration commands could be performed remotely.

### Remote verification

The remote session was verified using:

```bash
whoami
```

This confirmed which Linux account was being used through the SSH session.

## What I Learned

This lab provided practical experience with basic Linux account management and remote administration.

Key concepts demonstrated:

- Linux users and groups
- Group IDs (GIDs)
- User accounts
- Home directories
- `/etc/group`
- `/etc/passwd`
- `/etc/shadow`
- Password management
- User switching with `su`
- User verification with `whoami`
- SSH remote administration
- Using PuTTY as an SSH client

The additional PuTTY component helped connect the basic Linux account-management exercise to a real-world administration scenario where a Linux server may be managed remotely rather than through its local console.

## Evidence

Screenshots included in this repository demonstrate:

- Linux group creation
- User creation
- User/group verification
- `/etc/passwd` verification
- `/etc/shadow` verification
- Switching to the `ufour` account
- `whoami` verification
- PuTTY configuration
- Successful SSH connection to the Kali VM
- Remote command execution

## Security Considerations

The commands in this lab were performed in a controlled virtual-machine environment.

In a production environment:

- Strong passwords should be used.
- Passwords should never be documented in repositories.
- `/etc/shadow` should not be exposed unnecessarily.
- SSH should be properly secured.
- Root access should be restricted.
- Unnecessary services should be disabled.
- SSH authentication should preferably use strong authentication mechanisms such as SSH keys where appropriate.

## Conclusion

This lab demonstrated fundamental Linux user and group administration and extended the exercise with remote SSH access using PuTTY.

The combination of local account management and remote administration provided practical experience with tasks that are commonly encountered when managing Linux systems in cybersecurity and IT environments.
