# File Manipulation

This guide covers essential terminal commands for creating, editing, copying, moving, archiving, and editing text contents of files in macOS and Linux.

---

## 1. `mkdir` - Make Directory
Creates one or more new directories.

* **Syntax:** `mkdir [options] <directory_name>`
* **Example Usage:**
  ```bash
  # Create nested directories that do not exist yet
  mkdir -p projects/python/app
  ```
* **Useful Flags:**
  * `-p`: Parent directories are created as necessary; no error is returned if directories exist.

---

## 2. `touch` - Create File / Update Timestamp
Creates an empty file or updates the access and modification times of an existing file.

* **Syntax:** `touch [options] <filename>`
* **Example Usage:**
  ```bash
  # Create a new empty file
  touch config.json
  ```

---

## 3. `cp` - Copy Files and Directories
Copies files or directories from a source to a destination.

* **Syntax:** `cp [options] <source> <destination>`
* **Example Usage:**
  ```bash
  # Copy a folder recursively to a new location, preserving attributes
  cp -rp /src/my-folder /backup/my-folder
  ```
* **Useful Flags:**
  * `-r` or `-R`: Copy directories recursively.
  * `-p`: Preserve file attributes (permissions, owner, group, timestamps).
  * `-v`: Verbose output (shows files as they are copied).
  * `-i`: Interactive mode (prompts before overwriting).

---

## 4. `mv` - Move or Rename Files
Moves files or directories, or renames them if source and destination are in the same directory.

* **Syntax:** `mv [options] <source> <destination>`
* **Example Usage:**
  ```bash
  # Rename a file
  mv old_name.txt new_name.txt

  # Move a file to another directory
  mv document.pdf ~/Documents/
  ```
* **Useful Flags:**
  * `-i`: Prompts before overwriting.
  * `-n`: Do not overwrite an existing file.

---

## 5. `rm` - Remove Files or Directories
Deletes files or directories. **Use with caution!**

* **Syntax:** `rm [options] <target>`
* **Example Usage:**
  ```bash
  # Recursively and forcefully remove a directory
  rm -rf temporary_folder/
  ```
* **Useful Flags:**
  * `-r`: Remove directories and their contents recursively.
  * `-f`: Force removal without prompt, ignoring nonexistent files.
  * `-i`: Prompt before every removal.

---

## 6. `cat` - Concatenate and Display
Converts, concatenates, and displays file content to standard output.

* **Syntax:** `cat [options] [file]`
* **Example Usage:**
  ```bash
  # Display file content with line numbers
  cat -n log.txt
  ```
* **Useful Flags:**
  * `-n`: Number all output lines.

---

## 7. `less` & `more` - Page-by-Page Viewers
Displays file content one screen at a time. `less` is newer and allows both forward and backward navigation.

* **Syntax:** `less <filename>`
* **Example Navigation in `less`:**
  * `Space`: Forward one page.
  * `b`: Backward one page.
  * `G`: Go to end of file.
  * `g`: Go to start of file.
  * `/pattern`: Search forward for pattern.
  * `q`: Quit.

---

## 8. `head` & `tail` - View Ends of Files
Displays the beginning or ending of a file.

* **Syntax:**
  * `head [options] <filename>`
  * `tail [options] <filename>`
* **Example Usage:**
  ```bash
  # View first 15 lines of a file
  head -n 15 app.log

  # Monitor a log file in real time as new entries are appended
  tail -f /var/log/syslog
  ```
* **Useful Flags:**
  * `-n [number]`: Number of lines to print.
  * `-f` (tail only): Output appended data as the file grows.

---

## 9. `chmod` - Change File Permissions
Modifies read (`r`), write (`w`), and execute (`x`) permissions of files and directories.

* **Syntax:** `chmod [options] <permissions> <file>`
* **Example Usage:**
  ```bash
  # Grant owner read/write/execute, group and others read/execute (octal)
  chmod 755 run_script.sh

  # Remove write permission from group and others (symbolic)
  chmod go-w document.txt
  ```
* **Permissions breakdown (Octal):**
  * `4` = Read, `2` = Write, `1` = Execute.
  * `7` (rwx), `6` (rw-), `5` (r-x), `4` (r--).
  * Octal digit order: User (Owner), Group, Others.

---

## 10. `chown` - Change Owner and Group
Changes the owner and/or group of files and directories.

* **Syntax:** `chown [options] [owner][:group] <file>`
* **Example Usage:**
  ```bash
  # Change owner to "alice" and group to "developers" recursively
  sudo chown -R alice:developers /var/www/html
  ```
* **Useful Flags:**
  * `-R`: Operates recursively.

---

## 11. `ln` - Create Links
Creates hard links or symbolic (soft) links.

* **Syntax:** `ln [options] <target> <link_name>`
* **Example Usage:**
  ```bash
  # Create a symbolic link pointing to a config directory
  ln -s /etc/nginx/sites-available/default symlink_to_default
  ```
* **Useful Flags:**
  * `-s`: Create a symbolic (soft) link instead of a hard link.

---

## 12. `grep` - Search Pattern Matching
Searches input files for lines matching a regular expression pattern.

* **Syntax:** `grep [options] "pattern" [file]`
* **Example Usage:**
  ```bash
  # Search recursively for "error" in directory, case-insensitive, displaying line numbers
  grep -rnw -i "error" /var/log/
  ```
* **Useful Flags:**
  * `-i`: Ignore case distinctions.
  * `-r` or `-R`: Search directories recursively.
  * `-n`: Print line numbers of matches.
  * `-w`: Match whole words only.
  * `-v`: Invert match (prints lines that do *not* match).

---

## 13. `sed` - Stream Editor
Used for parsing and transforming text.

* **Syntax:** `sed [options] 'script' [file]`
* **Example Usage:**
  ```bash
  # Replace first occurrence of "localhost" with "127.0.0.1" in config.txt
  sed 's/localhost/127.0.0.1/' config.txt

  # In-place edit (saves changes to file) replacing all "foo" with "bar"
  sed -i 's/foo/bar/g' config.txt
  ```
* **Notes:**
  * On macOS (BSD `sed`), in-place edit requires an empty backup string: `sed -i '' 's/foo/bar/g' config.txt`.

---

## 14. `awk` - Text Processor
A programming language designed for text processing and pattern scanning.

* **Syntax:** `awk 'pattern {action}' [file]`
* **Example Usage:**
  ```bash
  # Print the 1st and 3rd fields of a space-separated file
  awk '{print $1, $3}' data.txt

  # Print second field where first field equals "admin" using ":" delimiter
  awk -F ":" '$1=="admin" {print $2}' /etc/passwd
  ```
* **Useful Flags:**
  * `-F <delimiter>`: Set the field separator.

---

## 15. `tar`, `zip` & `unzip` - Compress/Decompress
Used for archiving and compressing files.

* **Tar Syntax:** `tar [options] <archive_name.tar.gz> <files>`
  * **Create a gzipped tar archive:**
    ```bash
    tar -czvf archive.tar.gz /path/to/folder
    ```
  * **Extract a gzipped tar archive:**
    ```bash
    tar -xzvf archive.tar.gz
    ```
  * **Tar Flags:** `-c` (create), `-x` (extract), `-z` (gzip), `-v` (verbose), `-f` (specify file name).

* **Zip/Unzip Syntax:**
  * **Zip files:**
    ```bash
    zip -r archive.zip folder/
    ```
  * **Unzip files:**
    ```bash
    unzip archive.zip -d /destination/
    ```
