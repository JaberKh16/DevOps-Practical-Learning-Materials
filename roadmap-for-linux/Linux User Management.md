# Linux User, Group, and Privilege Management

This document covers:

1. Creating users
    
2. Deleting users
    
3. Managing groups
    
4. Granting administrative (root-level) privileges
    
5. Understanding how authentication/authorization works
    

---

## 1. Add a User

### Create a new user

`sudo useradd username`

### Create user with a home directory (recommended)

`sudo useradd -m username`

### Set password for the user

`sudo passwd username`

### Create a user with home, shell, and comment

`sudo useradd -m -s /bin/bash -c "Full Name" username`

---

## 2. Remove a User

### Delete a user (account only)

`sudo userdel username`

### Delete user **and** remove home directory + mail

`sudo userdel -r username`

---

## 3. Group Management

### Create a group

`sudo groupadd groupname`

### Delete a group

`sudo groupdel groupname`

### Add a user to a group

`sudo usermod -aG groupname username`

### Add a user to multiple groups

`sudo usermod -aG group1,group2 username`

### Remove a user from a group

(You must rewrite the group list)

`sudo gpasswd -d username groupname`

### View all groups

`getent group`

### View groups of a user

`groups username`

---

## 4. Grant Administrator / Root Privileges

Granting full root access means giving the user **sudo** privileges.

### Add user to the `wheel` or `sudo` group

On Fedora / RHEL / CentOS:

`sudo usermod -aG wheel username`

On Ubuntu / Debian:

`sudo usermod -aG sudo username`

### Verify sudo access

`su - username sudo whoami`

If correct, output:

`root`

---

## 5. Configure Full Root (Passwordless Optional)

### Edit sudoers (safe method)

Use the secure editor:

`sudo visudo`

Add this line to allow passwordless root access:

`username ALL=(ALL) NOPASSWD:ALL`

Allow normal sudo access with password:

`username ALL=(ALL) ALL`

**Important:**  
Never edit `/etc/sudoers` directly without `visudo` because syntax errors can lock you out.

---

## 6. Switch Between Users

### Switch to another user

`su - username`

### Become root

`su -`

or

`sudo -i`

---

## 7. Understanding User Authentication & Authorization

### Authentication

Verifies identity.  
Examples:

- Password in `/etc/shadow`
    
- SSH key
    
- PAM modules
    

### Authorization

Determines _what the user can do_.  
Examples:

- Group membership
    
- Permissions (r/w/x)
    
- sudo rules
    
- ACLs
    

### File permission basics

`r = read   w = write   x = execute`

Ownership:

- User (owner)
    
- Group
    
- Others
    

Change ownership:

`sudo chown user:group file`

Change permissions:

`chmod 755 file chmod 644 file`

---

## 8. Typical Admin Tasks (Examples)

### Create a developer user with sudo access

`sudo useradd -m devuser sudo passwd devuser sudo usermod -aG wheel devuser    # Fedora-based systems`

### Remove a user safely

`sudo userdel -r olduser`

### Add user to docker group (example)

`sudo usermod -aG docker username`

---

If you want, I can generate:

- A cheat sheet version
    
- A `.md` formatted PDF
    
- A step-by-step “create a new admin user” guide
    
- A full sysadmin notes template
    

Tell me what format you want next.