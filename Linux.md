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
- **Creating ZIP Archives**
  ```bash
  > zip -r file.zip /file/path
  ```
  This command creates a compressed ZIP archive of all files and subdirectories within the specified directory. The `-r` flag stands for \"recursive,\" meaning it includes all nested files.

- **Creating TAR.GZ Archives**
  ```bash
  > tar -zcvf file.tar.gz /file/path
  ```
  This command creates a compressed TAR archive with gzip compression. The `-z` enables gzip compression, `-c` writes the output to a file, and `-v` provides verbose output during the archiving process.

- **Creating GZipped Files with Date Suffix**
  ```bash
  > gzip -9 -c filename > filename.`date+%Y%m%d`.gz
  ```
  This command compresses a single file using maximum compression and appends the current date (YYYYMMDD) to the compressed file's name. This is useful for creating a unique backup file without overwriting the original.

*Note:* Ensure that the destination files do not already exist or that appropriate checks are in place to avoid accidental data loss due to overwrite.

**Explanation of Commands**

1. **ZIP Command**
   - The `zip -r` command recursively creates a ZIP archive, suitable for distributing software or backing up directories.

2. **TAR Command**
   - The `tar -zcvf` command is used for creating TAR archives with optional compression. It's useful when you need to compress files without the ZIP format.

3. **GZIP Command**
   - The `gzip -9` command applies maximum compression, making it ideal for large files or backups. Adding a date suffix helps in keeping track of backup versions over time.
  
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

-**Identify D state Processes**:
  ```bash
  > ps aux | awk '$8 ~ /^D/{print}'
  ```
  - **`ps aux`**: Displays a snapshot of all processes, including system-wide and per-user processes.
  - **Filtering Dead Processes**: The `awk` command looks for lines where the 8th field (`$8`) starts with 'D', indicating a dead (zombie) process. This command prints the entire line of each zombie process, which includes the user ID, PID, etc.

**Terminate D state Processes**:
  ```bash
  > ps aux | awk '$8 ~ /^D/{print $2}' | xargs kill -9
  ```
- **Explanation**:
  - **Filtering**: The `awk` command filters out only the second field (`$2`), which is the username associated with each D state process.
  - **Termination**: The resulting list of usernames is passed to `xargs`, which executes `kill -9` for each username, terminating the corresponding D state processes.

#### Important Notes
- **`kill -9`**: This signal immediately terminates a process without allowing it to clean up resources, which is useful for resolving resource leaks.
- **Permissions**: Ensure you have the necessary permissions to execute these commands. Root access may be required.