# Privilege Escalation

This guide covers essential terminal commands for executing commands with administrative/root privileges and switching user environments in macOS and Linux.

---

## 1. `sudo` - Superuser Do
Allows a permitted user to execute a command as the superuser (root) or another user, as security privileges dictate.

* **Syntax:** `sudo [options] <command>`
* **Example Usage:**
  ```bash
  # Install package as root
  sudo apt install curl

  # Switch to root interactive shell, loading root user profile
  sudo -i

  # Run command as another user (e.g., "www-data")
  sudo -u www-data php artisan migrate
  ```
* **Useful Flags:**
  * `-i`: Start an interactive shell as target user (defaults to root).
  * `-s`: Run shell specified by SHELL environment variable.
  * `-u [user]`: Run command as a specific user instead of root.
  * `-l`: List the user's privilege specification.

---

## 2. `su` - Switch User / Substitute User
Changes the login shell user ID to that of a specified user (defaults to root).

* **Syntax:** `su [options] [username]`
* **Example Usage:**
  ```bash
  # Switch to user bob (will prompt for bob's password)
  su bob

  # Switch to root, simulating full login (inherits root environment variables)
  su -
  ```
* **Useful Flags:**
  * `-` or `-l` or `--login`: Starts the shell as a login shell. This imports the target user's profile configuration and directories.
  * `-c <command>`: Pass a single command to the shell.

---

## 3. `visudo` - Edit sudoers Configuration
Safely edits the `/etc/sudoers` file, validating file syntax before saving to prevent configurations that could permanently lock out administrator access.

* **Syntax:** `sudo visudo [options]`
* **Example Usage:**
  ```bash
  # Edit sudoers file using default terminal editor
  sudo visudo
  ```
* **Useful Flags:**
  * `-c`: Check-only mode (validates existing `/etc/sudoers` file syntax without editing).

---

## 4. `doas` - Dedicated OpenBSD Application Submitter
A minimal, lightweight alternative to `sudo` originally created for OpenBSD, but now available on various Linux and macOS environments.

* **Syntax:** `doas [options] <command>`
* **Example Usage:**
  ```bash
  # Edit configuration as root
  doas vi /etc/doas.conf
  ```
* **Useful Flags:**
  * `-s`: Run interactive shell.
  * `-u [user]`: Execute command as specified user.

---

## 5. `pkexec` - PolicyKit Executive Helper
Executes a command as another user (typically root) using the Polkit (formerly PolicyKit) framework. It is common on graphical Linux environments.

* **Syntax:** `pkexec <command> [args]`
* **Example Usage:**
  ```bash
  # Run visual text editor as root using Polkit authentication window
  pkexec gedit /etc/fstab
  ```
