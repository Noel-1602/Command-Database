# Identity

This guide covers essential terminal commands for checking user identity, groups, login sessions, and current accounts on macOS and Linux systems.

---

## 1. `whoami` - Display Effective User Name
Prints the username associated with the current effective user ID.

* **Syntax:** `whoami`
* **Example Usage:**
  ```bash
  whoami
  # Output: alice
  ```

---

## 2. `id` - Display User & Group IDs
Prints real and effective user (UID) and group (GID) information for the current user or a specified user.

* **Syntax:** `id [options] [username]`
* **Example Usage:**
  ```bash
  # Print details for user "bob"
  id bob
  # Output: uid=1001(bob) gid=1001(bob) groups=1001(bob),27(sudo),118(docker)
  ```
* **Useful Flags:**
  * `-u`: Print UID only.
  * `-g`: Print primary GID only.
  * `-G`: Print all group IDs.
  * `-un`: Print name instead of ID number.

---

## 3. `w` & `who` - Display Logged In Users
Shows who is logged on to the system and what they are currently doing (`w` provides more detailed activity; `who` is simpler).

* **Syntax:**
  * `w [options]`
  * `who [options]`
* **Example Usage:**
  ```bash
  # Check active user actions
  w
  ```
* **Useful Flags:**
  * `who -a`: Display extensive log-in details including boot time, run level, and idle processes.

---

## 4. `last` - Login History
Displays the listing of last logged in users, reading from `/var/log/wtmp` (Linux) or `/var/log/utmpx` (macOS).

* **Syntax:** `last [options] [username]`
* **Example Usage:**
  ```bash
  # List last 10 login sessions
  last -n 10
  ```
* **Useful Flags:**
  * `-n [number]`: Limit the output count.
  * `-f [file]`: Read login records from a different log file.

---

## 5. `groups` - List User Groups
Prints the names of the primary and supplementary groups for each specified user, or the current user.

* **Syntax:** `groups [username]`
* **Example Usage:**
  ```bash
  # Print groups for alice
  groups alice
  # Output: alice staff admin wheel
  ```

---

## 6. `finger` - User Information Lookup
Displays information about system users, including real name, home directory, login time, and office details. (Often not installed by default).

* **Syntax:** `finger [username]`
* **Example Usage:**
  ```bash
  # Query info about alice
  finger alice
  ```
