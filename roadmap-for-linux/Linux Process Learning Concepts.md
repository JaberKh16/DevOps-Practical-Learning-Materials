# Linux Process Management – Complete Guide

## 1. What Is a Process?

A **process** is a running instance of a program.  
When you launch a command, the kernel:

1. Loads the executable into memory
    
2. Creates a process (with a unique PID)
    
3. Assigns CPU, memory, permissions
    
4. Manages scheduling and termination
    

### Two types

- **Foreground processes** – controlled by terminal
    
- **Background processes** – run independently
    

---

# 2. Key Process Concepts

## PID (Process ID)

Unique identifier for each process.

## PPID (Parent Process ID)

Every process is created by another (parent process), except PID 1.

## UID / EUID

- **UID** = owner of the process
    
- **EUID** = effective privileges  
    Used for authorization.
    

## Scheduling + CPU time

Kernel decides which process gets CPU via schedulers like:

- CFS (Completely Fair Scheduler)
    
- BFS
    
- Deadline scheduler
    

## Process States (ps)

- **R** = Running
    
- **S** = Sleeping
    
- **D** = Uninterruptible sleep
    
- **T** = Stopped
    
- **Z** = Zombie
    
- **X** = Dead (should not appear)
    

---

# 3. Core Commands

## View processes

### Full detailed process list

`ps aux`

### Tree view (parent-child hierarchy)

`ps axjf`

### Show processes of specific user

`ps -u username`

### Display process tree

`pstree -p`

---

# 4. Real-Time Monitoring Tools

## top

Interactive system monitor:

`top`

### Key interactions:

- `P` – sort by CPU
    
- `M` – sort by memory
    
- `k` – kill a process
    
- `r` – renice a process
    

## htop (better UI)

`sudo dnf install htop   # Fedora htop`

## glances (multi-system monitor)

`sudo dnf install glances glances`

---

# 5. Starting Processes

## Run a program normally (foreground)

`program`

## Run in background

`program &`

## Prevent hangup after logout

`nohup program &`

## Using disown (bash/zsh)

`program & disown`

---

# 6. Managing Background & Foreground Jobs

### List jobs

`jobs`

### Move job to background

`bg %1`

### Move job to foreground

`fg %1`

---

# 7. Kill, Stop, Continue Processes

## kill by PID

`kill PID`

## Force kill

`kill -9 PID`

## Graceful stop

`kill -15 PID`

## Kill by name

`pkill processname`

## Kill all processes of a user

`pkill -u username`

## Stop process

`kill -STOP PID`

## Resume process

`kill -CONT PID`

---

# 8. Finding Processes

## Search by name

`pgrep firefox`

## Search dynamically

`ps aux | grep ssh`

## Search by port (network-linked processes)

`sudo lsof -i :8080`

---

# 9. Process Priorities (nice & renice)

## Nice value range

- `-20` = highest priority
    
- `0` = default
    
- `19` = lowest priority
    

### Start a process with lower priority

`nice -n 10 program`

### Increase priority of running process

`sudo renice -5 PID`

---

# 10. CPU, Memory, I/O Analysis

## Memory usage of a process

`ps -o pid,ppid,cmd,%mem,rss -p PID`

## CPU usage

`ps -o pid,cmd,%cpu -p PID`

## List open files (very powerful)

`lsof -p PID`

## Show process I/O usage

`sudo iotop`

---

# 11. Process Control with systemd

## Start a system service

`sudo systemctl start service`

## Stop service

`sudo systemctl stop service`

## Enable on boot

`sudo systemctl enable service`

## Check running status

`systemctl status service`

## View service logs

`journalctl -u service`

---

# 12. Zombie & Orphan Processes

## Zombie process

A child finished but parent didn’t collect status.  
Identified by state **Z**.

Solution:

- Restart parent process
    
- Kill parent, letting `systemd` adopt and clean up
    

## Orphan process

Parent died; `systemd` adopts it.

---

# 13. Daemons

Background system services with no user interaction.

Examples:

- sshd
    
- docker
    
- cron
    
- systemd services
    

---

# 14. Using cgroups (control groups)

Control CPU/memory limits.

### Limit CPU

`systemd-run --scope -p CPUQuota=20% process`

### Limit memory

`systemd-run --scope -p MemoryMax=500M program`

---

# 15. Process Debugging & Tracing

### strace – trace system calls

`strace -p PID`

### gdb – debug running processes

`gdb -p PID`

### Observe process scheduling

`ps -o pid,ppid,ni,pri,rtprio,cmd`

---

# 16. Process Persistence (Supervisor Tools)

### systemd services

### PM2 (Node apps)

`pm2 start app.js`

### Supervisor

`sudo systemctl enable supervisord`

---

# 17. Important Files

|File|Purpose|
|---|---|
|`/proc/<PID>/`|Detailed process info|
|`/proc/cpuinfo`|CPU details|
|`/proc/meminfo`|Memory info|
|`/proc/loadavg`|Load averages|

---

# 18. Key Workflows (Practical Examples)

## Find and kill a high-CPU process

`top kill -9 PID`

## Check which process uses a port

`sudo lsof -i :3000 kill PID`

## Background long tasks safely

`nohup python script.py & disown`

## Restart a frozen service

`sudo systemctl restart service`

---

# Want this in a Markdown file?

I can generate:

- A `.md` file
    
- A PDF
    
- A cheat sheet (1 page)
    
- A flowchart diagram of process lifecycle