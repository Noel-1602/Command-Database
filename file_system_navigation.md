# File System Navigation

This guide covers essential terminal commands for navigating and searching the file system in macOS and Linux environments.

---

## 1. `pwd` - Print Working Directory
Displays the absolute path of the current working directory.

* **Syntax:** `pwd [options]`
* **Example Usage:**
  ```bash
  pwd
  # Output: /Users/username/Projects/cmd-db
  ```
* **Useful Flags:**
  * `pwd -P`: Resolve physical path (avoid symbolic links).

---

## 2. `ls` - List Directory Contents
Lists files and directories within the specified directory (defaults to current directory).

* **Syntax:** `ls [options] [path]`
* **Example Usage:**
  ```bash
  # List all files, including hidden ones, in a long format with human-readable sizes
  ls -lah
  ```
* **Useful Flags:**
  * `-l`: Long listing format (shows permissions, owner, size, modification date).
  * `-a`: List all entries including hidden files (those starting with `.`).
  * `-h`: Human-readable sizes (e.g., 1K, 234M, 2G).
  * `-t`: Sort by modification time, newest first.
  * `-R`: Recursively list subdirectories.

---

## 3. `cd` - Change Directory
Changes the current shell working directory.

* **Syntax:** `cd [path]`
* **Example Usage:**
  ```bash
  # Navigate to the home directory
  cd ~

  # Go up one level (parent directory)
  cd ..

  # Go back to the previously visited directory
  cd -

  # Navigate using absolute path
  cd /var/log
  ```

---

## 4. `pushd` & `popd` - Directory Stack Navigation
`pushd` changes the current directory and saves the previous directory to a stack. `popd` returns to the top directory on the stack.

* **Syntax:**
  * `pushd [directory]`
  * `popd`
* **Example Usage:**
  ```bash
  # Save current directory and switch to /var/log
  pushd /var/log

  # Do some work in /var/log, then return to the original directory
  popd
  ```

---

## 5. `tree` - Visual Directory Tree
Recursively displays directories and files in a tree-like format. (May require installation: `brew install tree` or `apt install tree`).

* **Syntax:** `tree [options] [path]`
* **Example Usage:**
  ```bash
  # Display directories only up to 2 levels deep
  tree -d -L 2
  ```
* **Useful Flags:**
  * `-d`: List directories only.
  * `-L [level]`: Max display depth of the directory tree.
  * `-a`: Print all files (including hidden files).

---

## 6. `find` - Search for Files and Directories
Searches for files in a directory hierarchy based on user-specified criteria.

* **Syntax:** `find [path] [expression]`
* **Example Usage:**
  ```bash
  # Find all files with .log extension in /var/log directory
  find /var/log -type f -name "*.log"

  # Find directories modified within the last 24 hours
  find . -type d -mtime -1
  ```
* **Useful Expressions:**
  * `-name [pattern]`: Case-sensitive search by filename.
  * `-iname [pattern]`: Case-insensitive search by filename.
  * `-type [f|d|l]`: Search only for files (`f`), directories (`d`), or symbolic links (`l`).
  * `-mtime [n]`: File's data was last modified n*24 hours ago.
  * `-size [+|-][size]`: Search files by size (e.g., `+100M` for files larger than 100MB).

---

## 7. `locate` - Quick File Search by Name
Finds files by matching names against a prebuilt database of files. Faster than `find`, but may not contain newly created files until the database is updated.

* **Syntax:** `locate [pattern]`
* **Example Usage:**
  ```bash
  # Locate all files containing "nginx.conf"
  locate nginx.conf
  ```
* **Notes:**
  * Update database in macOS: `sudo /usr/libexec/locate.updatedb`
  * Update database in Linux: `sudo updatedb`

---

## 8. `realpath` & `readlink` - Resolve Paths
Returns the resolved absolute path of a file, following symbolic links.

* **Syntax:**
  * `realpath [path]`
  * `readlink -f [path]`
* **Example Usage:**
  ```bash
  # Get absolute path of a symbolic link destination
  realpath my-symlink
  ```
