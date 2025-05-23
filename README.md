# Lab Report №9
Topic: “User and Group Management & System Security in Linux”

### Objective:
### The aim of this session was to gain practical experience with the Bash shell and to perform essential user and group management operations. The tasks also introduced core security principles associated with user access and permissions in Linux.

### Preparation Phase
### Key Terms and Definitions

| **Term**   | **Explanation**                                                                     |
| ---------- | ----------------------------------------------------------------------------------- |
| `sudo`     | Grants temporary administrator privileges to run a command.                         |
| `su`       | Allows a user to assume another user’s identity, usually for administrative access. |
| `id`       | Outputs UID, GID, and all groups associated with a specific user.                   |
| `groupadd` | Creates a new group on the system.                                                  |
| `usermod`  | Alters a user’s account details (e.g., groups, shell).                              |
| `getent`   | Fetches entries from system-wide databases like users or groups.                    |
| `chage`    | Controls password aging and expiration policies for user accounts.                  |

---

### Theoretical Review
### 1. What is a User Private Group (UPG)?
A UPG is a personal group created for each user when the account is added. This group has the same name as the user and is exclusive to that individual. It is commonly used when a system enforces strict file and directory access control per user. It enhances data isolation and simplifies permission handling in collaborative environments.

### 2. How are user groups created in Linux?
The groupadd command is the standard tool for defining new groups.
### **Example**:
groupadd admins  
groupadd trainees  
groupadd students

### 3. How can user group properties be modified?
To change a group’s attributes:

Use groupmod to rename or reassign a GID.

Use gpasswd to add or remove users from a group.
### Examples:
groupmod -n devs admins  
gpasswd -a user1 devs  
gpasswd -d user1 devs

### Overview of Key Commands
| **Command** | **Function**                                  |
| ----------- | --------------------------------------------- |
| `id`        | Shows the user and group IDs.                 |
| `who`       | Lists users currently logged in.              |
| `w`         | Shows logged-in users and their processes.    |
| `last`      | Displays login history.                       |
| `groupadd`  | Adds new groups.                              |
| `groupmod`  | Renames or reassigns GIDs.                    |
| `groupdel`  | Removes groups from the system.               |
| `useradd`   | Creates new user accounts.                    |
| `passwd`    | Changes user passwords.                       |
| `usermod`   | Modifies user attributes.                     |
| `userdel`   | Deletes users.                                |
| `groups`    | Lists group memberships for a user.           |
| `getent`    | Queries entries in NSS databases.             |
| `grep`      | Searches files for specific text or patterns. |
| `chage`     | Adjusts password expiration rules.            |
| `sudo`      | Executes commands with elevated privileges.   |
| `su`        | Switches to another user or root.             |Hands-On Tasks

### 1. Viewing Current User Details
Executed standard ID commands to identify current session user details including UID and GID.

### 2. Session Monitoring
Compared outputs of last, w, and who to analyze user logins and session activity:

last: Historical login data.

w: Current user sessions with process info.

who: Lists logged-in users only.

### 3. Creating User Groups
Defined three groups using groupadd. Confirmed creation with getent and grep.

### 4. Creating Users with Passwords
Three individual accounts were created and assigned passwords using passwd.

### 5. Assigning Users to Groups
Used usermod or gpasswd to associate users with specific groups.

### 6. Verifying Group Memberships
Checked group files and user memberships through getent group.

### 7–9. User Removal and Group Check
Sequentially removed users using userdel and verified their group associations were also removed.

### 10. Listing All Groups
Displayed all existing groups using getent group and filtered as needed.

### 11. Deleting Groups
Erased the previously created groups with groupdel.

### 12. Final Group Verification
Confirmed deletion by querying the group database to ensure no traces remained.

Control Questions Summary
### Why are passwords not stored in plain text?
To prevent exposure of sensitive data. Hashing ensures they are unreadable without proper decryption.

### Why avoid using the root account for daily tasks?
It carries risk due to full system access. Any mistakes can critically damage the system.

### Difference between su and sudo?
su switches the session user; sudo temporarily runs a command as another user without switching.

### Why is root’s home directory not in /home?
To isolate it from regular user directories for security and organizational clarity.

### Purpose of getent?
To access user, group, or network database information via NSS.

### How is a password changed?
Use passwd <username>, then enter and confirm a new password.

### How to remove a group and what remains?
groupdel removes it fully. If successful, no metadata or membership should remain.

### Why use chage?
To enforce password expiration and aging policies on user accounts.

Most useful usermod options?

-aG (add to groups)

-d (change home directory)

-s (change default shell)

#  Control Questions and Answers
###  Why are passwords not stored in plain text in configuration files?

Passwords are kept in a non-readable format to bolster security measures. By encrypting or hashing passwords, unauthorized individuals are prevented from easily accessing user credentials. If an attacker were to access the configuration files, they would not be able to retrieve the actual passwords.

### Why is it not recommended to perform everyday operations using the root account?

Utilizing the root account for routine tasks is not advisable due to the heightened security risks involved. The root account possesses unrestricted access to all system files and commands, which raises the chances of unintentional modifications or deletions that could adversely affect the system. Furthermore, if malware or an intruder gains control of the root account, they could inflict significant damage.

### What is the difference between the privilege escalation mechanisms su and sudo?

su (substitute user): This command enables a user to switch to another user account, typically the root account. When using su, the user must enter the password of the target account.
sudo (superuser do): This command allows an authorized user to execute a command as the superuser or another specified user, according to the security policy. With sudo, the user does not need to know the password of the target user; instead, they enter their own password. Additionally, sudo logs the executed commands, creating an audit trail.

### Why is the home directory of the root user not located in the /home directory?

The root user's home directory is situated in /root rather than /home because /home is reserved for standard user accounts. This distinction helps maintain security and organization within the file system, ensuring that the root user's files are kept separate from those of regular users.

### What is the purpose of the getent command?

The getent command is utilized to fetch entries from system databases, such as user accounts and groups, as well as other information stored in the Name Service Switch (NSS) databases. It can query data from various sources, including local files and network services.

### How can a user's password be changed?

A user's password can be modified using the passwd command followed by the username. For instance:
passwd username
The system will prompt for the new password and require confirmation.

### How can existing user groups be deleted? Will any information about them remain in the system?

Existing user groups can be removed using the groupdel command followed by the group name. For example:

groupdel groupname
Once a group is deleted, all associated information is purged from the system, and it will no longer exist in the group database.

### What is the purpose of the chage command?

The chage command is employed to modify user password expiration settings. It allows administrators to establish parameters such as the minimum and maximum lifespan of a password, warning periods prior to expiration, and the inactivity duration after which the account will be disabled.

### What parameters of the usermod command do you consider the most commonly used?

### The most frequently utilized parameters of the usermod command include:
-aG: Adds a user to additional groups without removing them from existing ones.
-l: Changes the user's username.
-d: Modifies the user's home directory.
-s: Alters the user's login shell.

# Conclusion
In this practical work, we examined user and group management in a Linux environment, focusing on the significance of User Private Groups (UPGs) for enhancing security and privacy. Through hands-on exercises, we learned to create user groups, add users, and manage accounts effectively. This experience provided essential skills for managing user permissions and improving system security, which will be valuable for future system administration tasks in Linux.
