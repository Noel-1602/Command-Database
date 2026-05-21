# Others

This guide covers essential terminal commands for productivity, shell customization, job scheduling, parameter manipulation, and general system utilities in macOS and Linux.

---

## 1. `man` - System Reference Manuals
Displays user manuals and document references for command-line tools.

* **Syntax:** `man <command>`
* **Example Usage:**
  ```bash
  # View manual pages for the grep command
  man grep
  ```
* **Useful Navigation:**
  * Use arrow keys or `Page Up`/`Page Down` to scroll.
  * Press `/` followed by search text to look up keywords.
  * Press `q` to exit manual pages.

---

## 2. `alias` - Create Custom Commands
Defines shortcuts or alternative names for commands, saving typing time.

* **Syntax:** `alias [name="command"]`
* **Example Usage:**
  ```bash
  # Create a shortcut for listing hidden files in list format
  alias la="ls -la"

  # List all currently configured aliases in the shell session
  alias
  ```
* **Persistent Aliases Note:** To make aliases persistent, add them to your shell's startup file (e.g., `~/.zshrc` or `~/.bashrc`).

---

## 3. `history` - Command History List
Lists commands entered in the current and past shell sessions.

* **Syntax:** `history [number]`
* **Example Usage:**
  ```bash
  # View last 15 commands used
  history 15

  # Search command history for git commands
  history | grep git
  ```
* **Tip:** Execute a specific historical command by its index using the exclamation mark, e.g., `!402` to run line 402 in history.

---

## 4. `clear` - Clear Screen
Clears the terminal screen of command inputs and outputs, restoring a clean workspace.

* **Syntax:** `clear`
* **Shortcut alternative:** Press `Ctrl + L` on most terminals.

---

## 5. `echo` - Print Text to Standard Output
Prints arguments or environment variables to the standard output terminal.

* **Syntax:** `echo [options] [string]`
* **Example Usage:**
  ```bash
  # Display the current shell path
  echo $SHELL

  # Append text directly to a file
  echo "nameserver 8.8.8.8" >> /etc/resolv.conf
  ```
* **Useful Flags:**
  * `-n`: Do not output the trailing newline character.
  * `-e`: Enable interpretation of backslash escapes (e.g., `\n` for newline, `\t` for tab).

---

## 6. `export` - Set Environment Variables
Sets environment variables so that child processes of the current shell session can access them.

* **Syntax:** `export [name=[value]]`
* **Example Usage:**
  ```bash
  # Set a custom API key for application runtime
  export STRIPE_API_KEY="sk_test_12345"
  ```
* **Persistent Export Note:** Like aliases, persistent exports belong in configuration scripts (`~/.zshrc` or `~/.bashrc`).

---

## 7. `date` & `cal` - Date, Time & Calendar
Displays or sets the system date, time (`date`), and prints a calendar format (`cal`).

* **Syntax:**
  * `date [options] [+format]`
  * `cal [options]`
* **Example Usage:**
  ```bash
  # Display date in ISO 8601 format
  date +"%Y-%m-%d %H:%M:%S"

  # Show calendar of the current month
  cal
  ```

---

## 8. `xargs` - Argument Builder
Reads items from standard input (separated by blanks or newlines) and executes a command using these items as arguments.

* **Syntax:** `<command_generating_input> | xargs [command]`
* **Example Usage:**
  ```bash
  # Find all temp files and delete them in one command
  find . -name "*.tmp" | xargs rm

  # Download URLs listed inside a text file using curl in parallel (up to 4 at a time)
  cat urls.txt | xargs -n 1 -P 4 curl -O
  ```
* **Useful Flags:**
  * `-I <placeholder>`: Replace occurrences of placeholder in command arguments with names read from stdin.
  * `-n [number]`: Use at most number arguments per command line.
  * `-P [number]`: Run up to number processes in parallel.

---

## 9. `crontab` - Cron Jobs Scheduler
Schedules recurring tasks (cron jobs) to run at specified intervals.

* **Syntax:** `crontab [options]`
* **Example Usage:**
  ```bash
  # Edit the user's crontab schedule
  crontab -e

  # List scheduled cron jobs
  crontab -l
  ```
* **Useful Flags:**
  * `-e`: Edit user's crontab file.
  * `-l`: List user's crontab entries.
  * `-r`: Remove all user's crontab entries.
* **Cron Pattern Format:** `* * * * * command_to_execute` (Minute, Hour, Day of Month, Month, Day of Week).
