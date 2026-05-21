# Networking

This guide covers essential terminal commands for inspecting networks, troubleshooting connectivity, copying data securely, and querying domain and port statuses in macOS and Linux.

---

## 1. `ping` - Network Diagnostics
Sends ICMP ECHO_REQUEST packets to network hosts to check for basic connectivity and latency.

* **Syntax:** `ping [options] <host>`
* **Example Usage:**
  ```bash
  # Send 4 ping requests to google.com
  ping -c 4 google.com
  ```
* **Useful Flags:**
  * `-c [count]`: Stop after sending count ECHO_RESPONSE packets.
  * `-i [seconds]`: Wait interval seconds between sending each packet.

---

## 2. `curl` - URL Client Request Tool
Transfers data to or from a server using supported protocols (HTTP, HTTPS, FTP, etc.).

* **Syntax:** `curl [options] <url>`
* **Example Usage:**
  ```bash
  # Fetch API response and display headers only
  curl -I https://api.github.com

  # Download a file and save it with the remote server filename
  curl -O https://example.com/file.zip

  # Send a POST request with JSON payload
  curl -X POST -H "Content-Type: application/json" -d '{"key":"val"}' https://httpbin.org/post
  ```
* **Useful Flags:**
  * `-I`: Fetch headers only.
  * `-O`: Save file to current directory with remote name.
  * `-o <filename>`: Save file with specified name.
  * `-L`: Follow redirects.
  * `-X <METHOD>`: Specify request method (GET, POST, PUT, DELETE, etc.).
  * `-d <data>`: Send data in POST request.

---

## 3. `wget` - File Downloader
Downloads files from the web. Unlike `curl`, `wget` is optimized for background downloading and recursive retrieving.

* **Syntax:** `wget [options] <url>`
* **Example Usage:**
  ```bash
  # Download page and all assets for offline reading
  wget --mirror --convert-links --adjust-extension --page-requisites --no-parent https://example.com
  ```
* **Useful Flags:**
  * `-O <filename>`: Save output under specified name.
  * `-c`: Resume partially-downloaded files.
  * `-b`: Run in the background.

---

## 4. `ifconfig` & `ip` - Interface Configuration
Used to configure or display network interface parameters. `ifconfig` is standard in macOS and older Linux distros; `ip` is preferred on newer Linux installations.

* **Syntax:**
  * macOS / Old Linux: `ifconfig`
  * Linux: `ip [options] <object> [command]`
* **Example Usage:**
  ```bash
  # Show all interface information (macOS / generic)
  ifconfig

  # Show all IP addresses (Linux)
  ip a

  # Show routing tables (Linux)
  ip route
  ```

---

## 5. `netstat` & `ss` - Socket Statistics
Prints network connections, routing tables, interface statistics, masquerade connections, and multicast memberships. `ss` is the modern replacement for `netstat` on Linux.

* **Syntax:**
  * `netstat [options]`
  * `ss [options]`
* **Example Usage:**
  ```bash
  # Show all active listening TCP and UDP ports with process IDs (Linux)
  sudo netstat -tulnp

  # Modern ss command to list all listening TCP ports
  ss -tln
  ```
* **Useful Flags:**
  * `-t`: TCP ports.
  * `-u`: UDP ports.
  * `-l`: Listening ports.
  * `-n`: Numeric formatting (show IP addresses/port numbers instead of hostnames/service names).
  * `-p`: Show process ID and name associated with sockets (requires root privileges).

---

## 6. `nslookup` & `dig` - DNS Lookup
Queries Domain Name Servers for DNS records. `dig` is modern and provides more verbose, detailed answers than `nslookup`.

* **Syntax:**
  * `nslookup <domain>`
  * `dig [type] <domain>`
* **Example Usage:**
  ```bash
  # Find MX (Mail Server) records for a domain
  dig MX google.com +short

  # Simple nslookup
  nslookup github.com
  ```
* **Useful Dig Types:**
  * `A`: IPv4 address.
  * `AAAA`: IPv6 address.
  * `TXT`: Text record.
  * `MX`: Mail exchange record.
  * `NS`: Name servers.

---

## 7. `traceroute` & `mtr` - Packet Route Tracing
Tracks the path packets take to reach a destination host. `mtr` combines `traceroute` and `ping` features into a single diagnostic interface.

* **Syntax:**
  * `traceroute <host>`
  * `mtr <host>`
* **Example Usage:**
  ```bash
  # Track route to google dns
  traceroute 8.8.8.8
  ```

---

## 8. `ssh` - Secure Shell
Secures remote logins and command executions.

* **Syntax:** `ssh [options] [user]@<host>`
* **Example Usage:**
  ```bash
  # Login with specific private key on custom port
  ssh -i ~/.ssh/my_key.pem -p 2200 admin@192.168.1.50
  ```
* **Useful Flags:**
  * `-i <identity_file>`: Path to SSH private key.
  * `-p <port>`: Port to connect to on the remote server.
  * `-L <local_port>:<dest_host>:<dest_port>`: Local port forwarding.

---

## 9. `scp` - Secure Copy
Copies files securely between local and remote hosts using SSH protocol.

* **Syntax:** `scp [options] <source> <destination>`
* **Example Usage:**
  ```bash
  # Copy local file to a remote server
  scp -P 2200 document.txt user@remote-host:/var/www/uploads/

  # Copy remote directory to local workspace
  scp -r user@remote-host:/var/log/nginx/ ./local-nginx-logs/
  ```
* **Useful Flags:**
  * `-P <port>`: Remote host connection port (note: capitalized).
  * `-r`: Recursively copy directories.
  * `-p`: Preserve modification/access times and modes.

---

## 10. `rsync` - Remote Synchronization
Synchronizes files and directories between locations efficiently, sending only diffs.

* **Syntax:** `rsync [options] <source> <destination>`
* **Example Usage:**
  ```bash
  # Sync directories locally with progress bar, compression, and delete files in dest that do not exist in src
  rsync -avz --delete --progress /src/dir/ /backup/dir/
  ```
* **Useful Flags:**
  * `-a` (archive): Recursively copies files, preserving symlinks, permissions, ownership, and timestamps.
  * `-v`: Verbose.
  * `-z`: Compress file data during transfer.
  * `--delete`: Delete files at destination that do not exist at source.
  * `--dry-run`: Perform a trial run without modifying files.

---

## 11. `nc` (Netcat) - Arbitrary Connection Handler
Reads and writes data across network connections. Often referred to as a Swiss Army knife.

* **Syntax:** `nc [options] <host> <port>`
* **Example Usage:**
  ```bash
  # Scan for open port 80 and 443 with 2 second timeout
  nc -zv -w 2 google.com 80 443

  # Start listener on port 9000
  nc -l 9000
  ```
* **Useful Flags:**
  * `-l`: Listen mode.
  * `-z`: Zero-I/O mode (used for scanning).
  * `-v`: Verbose.
  * `-w [seconds]`: Timeout for connections.

---

## 12. `nmap` - Port Scanner
Network scanner used to discover hosts and services on a computer network. (Requires installation).

* **Syntax:** `nmap [options] <target>`
* **Example Usage:**
  ```bash
  # Fast scan of the most common 100 ports
  nmap -F 192.168.1.1

  # Perform OS and service detection scan
  sudo nmap -A 192.168.1.100
  ```
