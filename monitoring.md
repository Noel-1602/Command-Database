# Monitoring

This guide covers essential terminal commands for inspecting CPU, Memory, Disk Space, Input/Output status, and reviewing system logs in macOS and Linux.

---

## 1. `top` - Dynamic Process Monitor
Displays real-time system summary information and a list of active tasks/processes.

* **Syntax:** `top [options]`
* **Example Usage:**
  ```bash
  top
  ```
* **Useful Interactive Keys:**
  * `q`: Quit.
  * `M`: Sort by memory usage.
  * `P`: Sort by CPU usage.
  * `u [username]`: Filter by user.

---

## 2. `htop` - Interactive Process Viewer
An interactive, colorful, and user-friendly process manager (replaces `top` in modern setups). (Requires installation).

* **Syntax:** `htop`
* **Example Usage:**
  ```bash
  htop
  ```
* **Useful Features:**
  * Support for mouse interactions.
  * Horizontal and vertical scrolling.
  * Tree view of processes (`F5`).
  * Kill process directly without knowing PID (`F9`).

---

## 3. `df` - Disk Free Space
Displays the amount of disk space available on file systems.

* **Syntax:** `df [options] [path]`
* **Example Usage:**
  ```bash
  # Display disk space in a human-readable format
  df -h
  ```
* **Useful Flags:**
  * `-h`: Human-readable size (e.g., K, M, G).
  * `-T`: Print file system type (Linux only).

---

## 4. `du` - Disk Usage
Estimates file and directory space usage.

* **Syntax:** `du [options] [path]`
* **Example Usage:**
  ```bash
  # Estimate usage of all subdirectories, sorted by size (Linux)
  du -h --max-depth=1 /var | sort -hr
  ```
* **Useful Flags:**
  * `-h`: Human-readable format.
  * `-s`: Summarize (display total size of folder, not individual files).
  * `-d [depth]`: Max depth of subdirectories to traverse (macOS/Linux).
  * `--max-depth=[depth]`: Same as `-d` (Linux).

---

## 5. `free` - Memory Usage
Displays the amount of free and used physical and swap memory in the system. (Linux only).

* **Syntax:** `free [options]`
* **Example Usage:**
  ```bash
  # Display memory statistics in gigabytes
  free -g
  ```
* **Useful Flags:**
  * `-h`: Display in human-readable format.
  * `-m`: Show sizes in megabytes.
  * `-g`: Show sizes in gigabytes.

---

## 6. `vmstat` - Virtual Memory Statistics
Reports information about processes, memory, paging, block IO, traps, disks, and CPU activity.

* **Syntax:** `vmstat [delay] [count]`
* **Example Usage:**
  ```bash
  # Display statistics every 2 seconds, 5 times total
  vmstat 2 5
  ```

---

## 7. `iostat` - Input/Output Statistics
Reports Central Processing Unit (CPU) statistics and input/output statistics for devices and partitions.

* **Syntax:** `iostat [options] [interval] [count]`
* **Example Usage:**
  ```bash
  # Display I/O statistics for disks in human-readable format
  iostat -h -d 2 3
  ```
* **Useful Flags:**
  * `-d`: Display only device utilization report.
  * `-c`: Display only CPU utilization report.

---

## 8. `uptime` - System Running Time
Displays how long the system has been running, along with the current time, number of users, and system load averages.

* **Syntax:** `uptime`
* **Example Usage:**
  ```bash
  uptime
  # Output: 14:23:45 up  2:10,  3 users,  load average: 0.15, 0.08, 0.05
  ```
* **Load Averages Explained:**
  * Reflects CPU/IO demand over 1, 5, and 15-minute intervals. Higher than CPU core count implies resource bottleneck.

---

## 9. `lsof` - List Open Files
Lists information about files opened by processes. In UNIX, everything is a file (including network sockets, directories, pipes, etc.).

* **Syntax:** `lsof [options]`
* **Example Usage:**
  ```bash
  # Find which process is listening on local port 3000
  lsof -i :3000

  # List open files for a specific user
  lsof -u username
  ```
* **Useful Flags:**
  * `-i [:[port]]`: List open internet sockets (filter by port if specified).
  * `-t`: Terse output (returns process IDs only, useful for pipes).
  * `-u <username>`: Filter by user name.

---

## 10. `journalctl` - Query System Logs
Queries and displays logs from the systemd journal service. (Linux only).

* **Syntax:** `journalctl [options]`
* **Example Usage:**
  ```bash
  # View boot logs from the current session
  journalctl -b

  # Follow logs in real time (similar to tail -f)
  journalctl -f

  # View logs for a specific service
  journalctl -u nginx.service
  ```
* **Useful Flags:**
  * `-f`: Follow logs.
  * `-u <unit>`: Filter by systemd service/unit.
  * `-p [level]`: Filter by priority/severity (e.g. `err`, `warning`, `info`).

---

## 11. `dmesg` - Kernel Ring Buffer Messages
Examines or controls the kernel ring buffer, showing bootup kernel alerts, drivers, hardware errors, and crash info.

* **Syntax:** `dmesg [options]`
* **Example Usage:**
  ```bash
  # Show kernel errors and warning messages
  dmesg -T | grep -i "error\|fail\|warn"
  ```
* **Useful Flags:**
  * `-T`: Print human-readable timestamps.
  * `-w`: Wait for new messages (follow mode).
