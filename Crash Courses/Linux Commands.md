# ✨ Linux Command‑Line Crash Course – Popular Commands in Depth

> **Scope**: Focus on everyday, must‑know GNU/Linux utilities.  
> **Audience**: New to intermediate users who want practical mastery.  
> **Shell**: Assumes Bash, but commands work in any POSIX shell unless noted.

---

## 1. Orientation & Navigation

### 1.1 `pwd` – Print Working Directory

```bash
pwd          # show full absolute path of current directory
```

_Tip: combine with the prompt (`PS1`) so you always see where you are._

### 1.2 `cd` – Change Directory

```bash
cd /etc      # absolute path
cd ..        # parent
cd -         # jump back to previous dir
cd ~         # home (also just `cd` with no args)
```

### 1.3 `ls` – List Directory Contents

```bash
ls                # bare listing
ls -l             # long (permissions, owner, size, date)
ls -a             # include dotfiles
ls -lh            # human‑readable sizes (K/M/G)
ls -lt            # sort by mtime, newest first
```

_Alias idea: `ll='ls -alFh --color=auto'`_

---

## 2. File & Directory Manipulation

### 2.1 `touch` – Create/Update Time‑stamp

```bash
touch file.txt            # create empty or update mtime
```

### 2.2 `mkdir` / `rmdir`

```bash
mkdir newdir              # single directory
mkdir -p a/b/c            # make parents as needed
rmdir emptydir            # only if directory is empty
```

### 2.3 `cp`, `mv`, `rm`

```bash
cp source.txt dest.txt          # copy file
cp -r dirA dirB                 # copy recursively
mv old.txt new.txt              # rename/move
mv *.jpg ~/Pictures/            # move group
rm temp.txt                     # delete file
rm -r old_backup/               # recursive delete
rm -rf /path/to/dir             # force delete (use with caution!)
```

---

## 3. Viewing & Inspecting Files

### 3.1 `cat`, `tac`, `nl`

```bash
cat file          # dump to stdout
tac file          # reverse order (lines)
nl  file          # add line numbers
```

### 3.2 `less` (preferred pager)

```bash
less file         # space / b = page fwd / back; /pattern = search
```

### 3.3 `head`, `tail`

```bash
head -n 20 file           # first 20 lines
tail -n 50 file           # last 50 lines
tail -f /var/log/syslog   # follow appended data (Ctrl‑C to stop)
```

### 3.4 `file`

```bash
file my.bin        # identify file type via magic numbers
```

---

## 4. Text Processing Power Trio

> These three can handle 80 % of one‑liners.

### 4.1 `grep` – Filter Lines by Pattern

```bash
grep "error" file.log
grep -i "warn" *.log          # case‑insensitive, across files
grep -R --line-number "TODO" src/
```

### 4.2 `awk` – Field‑Oriented Processor

```bash
awk '{print $1, $3}' data.txt                  # default FS=space
awk -F, '$4 > 100 {print $1,$4}' sales.csv     # comma‑sep, numeric filter
```

### 4.3 `sed` – Stream Editor

```bash
sed 's/foo/bar/g' file.txt                     # replace all on each line
sed -n '10,20p' bigfile                        # print only lines 10‑20
```

---

## 5. Sorting, Uniqueness & Counting

```bash
sort names.txt                       # alphabetic
sort -n numbers.txt                  # numeric
sort -u list.txt                     # sort & deduplicate
uniq -c                              # counts for consecutive duplicates
wc -l file                            # line count
```

---

## 6. Permissions & Ownership

### 6.1 `chmod` – Change Mode

```bash
chmod 644 file          # rw‑r‑‑r‑‑
chmod +x script.sh      # add execute bit for all
chmod -R o-rwx dir/     # recurse, remove all perms for others
```

### 6.2 `chown`, `chgrp`

```bash
sudo chown alice:users  file
sudo chown -R root:root /opt/app
```

---

## 7. System Monitoring & Processes

### 7.1 `ps`, `pgrep`, `top`, `htop`

```bash
ps aux | grep nginx                 # snapshot
pgrep -l ssh                        # list PIDs matching name
top                                 # interactive live view
htop                                # nicer top (may need install)
```

### 7.2 `free`, `vmstat`, `uptime`

```bash
free -h         # RAM usage
vmstat 1        # system stats every second
uptime          # load averages & uptime
```

### 7.3 `df`, `du`

```bash
df -h                           # disk free, per FS
du -sh /var/log                 # disk used by dir
du -h --max-depth=1 /home       # per subdir
```

### 7.4 Process Control

```bash
kill -SIGTERM 1234              # gracefully stop PID 1234
kill -9 1234                    # force kill
pkill -HUP nginx                # send HUP to all nginx pids
jobs                            # list background jobs
fg %1                           # bring job 1 to foreground
```

---

## 8. Networking Essentials

|Need|Command & Example|
|---|---|
|Connectivity|`ping -c 4 8.8.8.8`|
|DNS lookup|`dig example.com` (or `host`)|
|Route trace|`traceroute example.org`|
|Interfaces|`ip a` (modern) / `ifconfig` (legacy)|
|Open ports|`ss -tulpn` (better than `netstat`)|
|Download|`curl -O URL` or `wget URL`|
|Copy remote|`scp file user@host:/path/`|
|Sync dirs|`rsync -av --progress src/ user@host:dst/`|
|SSH login|`ssh -i key.pem user@server`|

---

## 9. Archiving & Compression

```bash
tar -czf backup.tgz dir/          # create gzipped archive
tar -xvf backup.tgz               # extract
gzip bigfile                      # compress (adds .gz)
gunzip bigfile.gz                 # decompress
zip -r archive.zip folder/        # zip
unzip archive.zip
```

---

## 10. Package Management (Debian‑based)

```bash
sudo apt update                   # refresh package lists
sudo apt upgrade                  # upgrade all
sudo apt install htop curl        # install
sudo apt remove nano              # uninstall
```

_On RHEL/Fedora use `yum` or `dnf`; on Arch use `pacman`._

---

## 11. User & Group Management

```bash
whoami              # current user
id                  # uid, groups
sudo command        # run command as root
su -                # switch to root (requires root password)
sudo useradd bob    # add user
sudo passwd bob     # set password
sudo usermod -aG sudo bob   # add bob to sudoers
```

---

## 12. Time & Scheduling

```bash
date +"%F %T"              # custom format
cal                        # calendar
crontab -e                 # edit user cron
# m h dom mon dow  command
# 0 2 * * * /usr/local/bin/backup.sh
```

---

## 13. Logs & Services (systemd)

```bash
sudo systemctl status nginx
sudo systemctl start  nginx
sudo systemctl enable nginx      # auto‑start at boot
journalctl -u nginx -f           # follow service logs
```

---

## 14. Disk Utilities

```bash
lsblk                 # block devices & mount pts
sudo fdisk -l         # partition tables
blkid                 # UUIDs & FS types
mount /dev/sdb1 /mnt  # mount device
umount /mnt           # unmount
```

---

## 15. Miscellaneous Gems

```bash
history | grep ssh        # search command history
alias gs='git status'     # create shortcut (put in ~/.bashrc)
xargs -n1 echo            # build command lines from stdin
printf "%s\n" "line1"     # safer than echo for raw data
date -d '@1700000000'     # convert epoch
yes | sudo apt upgrade    # auto‑confirm (careful!)
```

---

## 16. Combining Commands: Pipelines & Subshells

```bash
grep -i "error" *.log | sort | uniq -c | sort -nr | head
# 1) filter     2) sort alpha  3) collapse dupes w/count
# 4) sort numeric desc  5) show top results
```

---

## 17. Best Practices & Tips

1. **Man pages**: `man grep` (or `tldr grep` for examples).
    
2. **Tab completion**: saves typos & time.
    
3. **Quote your variables** to avoid word‑splitting: `"$var"`.
    
4. **Use `--help`**: almost every GNU utility explains itself briefly.
    
5. **Practice**: create a playground directory and try each command.
    

---

### 🚀 Next Steps

- Work through the **“Linux Command‑Line & Shell Scripting Bible”** book’s exercises.
    
- Explore interactive sites like **overthewire.org** (Bandit wargame) to reinforce skills.
    
- Write small scripts: log rotation, automatic backups, server health checks.
    

Master these commands and you’ll navigate, troubleshoot, and automate with confidence on any Linux box. Happy hacking!