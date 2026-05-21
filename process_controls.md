# Process Controls

This guide covers essential terminal commands for checking, running, pausing, backgrounding, and terminating processes on macOS and Linux systems.

---

## 1. `ps` - Process Status
Provides snapshots of information concerning active processes.

* **Syntax:** `ps [options]`
* **Example Usage:**
  ```bash
  # Standard Linux system-wide process listing showing user and command details
  ps aux

  # Search for a specific process (e.g., python)
  ps aux | grep python
  ```
* **Useful Output Columns:**
  * `USER`: Owner of the process.
  * `PID`: Process Identification number (critical for killing/managing).
  * `%CPU` & `%MEM`: Percentage of resource usage.
  * `STAT`: Process state (e.g., `R` for Running, `S` for sleeping, `T` for stopped, `Z` for zombie).
* **Common Flag Combos:**
  * `ps aux` (BSD style): Lists all running processes for all users.
  * `ps -ef` (System V style): Lists all processes with full formatting.

---

## 2. `kill` - Terminate Process by PID
Sends signals to active processes, most commonly to terminate them.

* **Syntax:** `kill [options] <PID>`
* **Example Usage:**
  ```bash
  # Gracefully terminate process (SIGTERM)
  kill 1234

  # Forcefully kill process immediately (SIGKILL)
  kill -9 5678
  ```
* **Common Signals:**
  * `1` / `SIGHUP`: Hang up (reloads configuration).
  * `9` / `SIGKILL`: Kill signal (non-catchable, terminates process immediately).
  * `15` / `SIGTERM`: Termination signal (default, allows process to clean up and exit).

---

## 3. `killall` - Kill Processes by Name
Terminates processes matching a specified program name.

* **Syntax:** `killall [options] <process_name>`
* **Example Usage:**
  ```bash
  # Forcefully close all Google Chrome instances
  killall -9 "Google Chrome"
  ```
* **Useful Flags:**
  * `-i`: Interactively ask for confirmation before killing.
  * `-u [user]`: Kill processes belonging only to a specific user.

---

## 4. `pkill` - Process Signal Lookup/Kill
Looks up or signals processes based on name and other attributes. More versatile than `killall` as it supports pattern matching.

* **Syntax:** `pkill [options] <pattern>`
* **Example Usage:**
  ```bash
  # Kill all processes containing "python" in the name
  pkill -f python
  ```
* **Useful Flags:**
  * `-f`: Match against full command line instead of process name only.
  * `-u <username>`: Kill processes owned by specified user.

---

## 5. `bg` & `fg` - Job Control (Background/Foreground)
Resumes stopped jobs in the background (`bg`) or brings a background/stopped job to the foreground (`fg`).

* **Syntax:**
  * `bg %[job_number]`
  * `fg %[job_number]`
* **Example Usage:**
  ```bash
  # 1. Start a task (e.g., compressing files)
  tar -czf backup.tar.gz /data

  # 2. Press Ctrl+Z to pause the job
  # Output: [1]+  Stopped                 tar -czf backup.tar.gz /data

  # 3. Resume the job in the background
  bg %1

  # 4. Bring it back to the foreground to interact with it
  fg %1
  ```

---

## 6. `jobs` - List Shell Jobs
Lists active, stopped, or background jobs spawned from the current terminal shell session.

* **Syntax:** `jobs [options]`
* **Example Usage:**
  ```bash
  # List jobs with process IDs
  jobs -l
  ```
* **Useful Flags:**
  * `-l`: List PIDs in addition to normal information.
  * `-s`: Display only stopped jobs.
  * `-r`: Display only running jobs.

---

## 7. `nohup` - No Hangup Execution
Runs a command immune to hangups, allowing it to continue running even after the user logs out.

* **Syntax:** `nohup <command> [args] &`
* **Example Usage:**
  ```bash
  # Run a long script in background, logging outputs to a file
  nohup python long_script.py > output.log 2>&1 &
  ```
* **Note:** By default, if stdout/stderr are not redirected, they are outputted to a file named `nohup.out`.

---

## 8. `disown` - Remove Job from Shell
Instructs the shell not to send a SIGHUP signal to the specified jobs when the shell session terminates.

* **Syntax:** `disown [options] %[job_number]`
* **Example Usage:**
  ```bash
  # Start a process in the background
  node server.js &

  # Disown the most recent background job so it survives terminal closing
  disown
  ```
* **Useful Flags:**
  * `-a`: Disown all jobs.
  * `-h`: Do not remove the job from active list, but do not send SIGHUP when the shell exits.

---

## 9. `systemctl` & `service` - System Service Manager
Used to inspect and manage systemd services on Linux. macOS uses `launchctl` as its native service manager, but `service` and `systemctl` are the standard on Linux.

* **Syntax:** `systemctl [action] <service_name>`
* **Example Usage:**
  ```bash
  # Check status of Nginx service
  systemctl status nginx

  # Restart Apache service
  sudo systemctl restart apache2

  # Enable a service to start on system boot
  sudo systemctl enable docker
  ```
* **Common Actions:**
  * `start` / `stop` / `restart`: Control service runtime.
  * `status`: Inspect logs and current status.
  * `enable` / `disable`: Enable or disable start on system boot.
  * `reload`: Reload configuration files without stopping the service.
