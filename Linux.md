## Linux Commands
### File Management
- **Check file system usage**:
  ```bash
  > df -h <file-system>
  ```
- **Show and sort file size in descending order**:
  ```bash
  > du -sh * | sort -hr
  ```
- **Find files with more than specific days**:
  ```bash
  > find /path -type f -mtime +(days)
  ```
  
### Permissions
- **Change owner of file**:
  ```bash
  > chown <owner> <file-name>
  ```
- **Change owner of folder and all files within it**:
  ```bash
  > chown -R <owner> /folder/path
  ```
- **Modify permission of a file**:
  ```bash
  > chmod XXX <file-name>
  ```
  *Explanation:* A three-digit number specifying access rights for the **user**, **group**, and **other** categories.
  - 0: (000) No permission.
  - 1: (001) Execute permission.
  - 2: (010) Write permission.
  - 3: (011) Write and execute permissions.
  - 4: (100) Read permission.
  - 5: (101) Read and execute permissions.
  - 6: (110) Read and write permissions.
  - 7: (111) Read, write, and execute permissions.

### System Logs
- **Check false credentials logins**:
  ```bash
  > pam_tally2
  > pam_tally2 --reset
  > faillock
  > faillock --user <username> --reset
  ```
- **Check login log**:
  ```bash
  > cat /var/log/secure | grep <username>
  ```
- **Check system log**:
  ```bash
  > cat /var/log/messages | grep <keyword>
  ```
- **Follow system logs in real-time**:
  ```bash
  > tail -f /var/log/messages
  ```
- **Linux vi editor**:
  ```bash
  > vi <file-name>
  ```
  *Explanation:* A powerful text editor with specific keystrokes:
  - `i` to enter edit mode.
  - Esc to go back to command mode.
  - `:q` to quit vi (only executable in command mode).
  - `:q!` to quit vi without saving (only executable in command mode).
  - `:wq` to save and quit vi (only executable in command mode).

### Mounting
- **Unmount a specific path**:
  ```bash
  > umount -l /file/path # Normally used when mount hung [strace df -h]
  ```
- **Unmount all mounted file systems**:
  ```bash
  > umount /file/path
  ```
- **Mount a specific path**:
  ```bash
  > mount /file/path
  ```
- **Mount all available file systems**:
  ```bash
  > mount -a
  ```
- **Check available mounts on the server**:
  ```bash
  > cat /etc/fstab
  ```
- **Show disk info**:
  ```bash
  > lsbik
  ```
- **Disk partition information**:
  ```bash
  > fdisk -l
  ```

### Process Monitoring and Management

-**Check Running Processes**:
  ```bash
  > top
  ```
- When you run `top`, it displays a list of processes along with their status. Pressing 1 will show more details about CPU utilization.

-**Identify Dead Processes (Zombies)**:
  ```bash
  > ps aux | awk '$8 ~ /^D/{print}'
  ```
  - **`ps aux`**: Displays a snapshot of all processes, including system-wide and per-user processes.
  - **Filtering Dead Processes**: The `awk` command looks for lines where the 8th field (`$8`) starts with 'D', indicating a dead (zombie) process. This command prints the entire line of each zombie process, which includes the user ID, PID, etc.

**Terminate Zombie Processes**:
  ```bash
  > ps aux | awk '$8 ~ /^D/{print $2}' | xargs kill -9
  ```
- **Explanation**:
  - **Filtering**: The `awk` command filters out only the second field (`$2`), which is the username associated with each zombie process.
  - **Termination**: The resulting list of usernames is passed to `xargs`, which executes `kill -9` for each username, terminating the corresponding zombie processes.

#### Important Notes
- **Zombie Processes**: These are processes that have been terminated but haven't been properly cleaned up, often due to parent processes still running.
- **`kill -9`**: This signal immediately terminates a process without allowing it to clean up resources, which is useful for resolving resource leaks.
- **Permissions**: Ensure you have the necessary permissions to execute these commands. Root access may be required.