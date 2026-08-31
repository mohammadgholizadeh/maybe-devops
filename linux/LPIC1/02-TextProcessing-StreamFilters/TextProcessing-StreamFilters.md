# Linux Text Processing & Stream Filters

## 1. File Viewing & Paging

| Command / Option | Description | Practical Command |
| :--- | :--- | :--- |
| `cat filename` | Concatenate and display full file contents to standard output | `cat /etc/environment` |
| `cat -n filename` | Display line numbers alongside all output lines | `cat -n pipeline.yaml` |
| `cat -E filename` | Display a `$` at the end of each line to spot trailing whitespace/line endings | `cat -E deployment.yaml` |
| `cat -T filename` | Display TAB characters explicitly as `^I` | `cat -T Makefile` |
| `cat -s filename` | Squeeze multiple consecutive blank lines into a single blank line | `cat -s raw_build.log > clean_build.log` |
| `cat -v filename` | Display non-printing characters (except TAB and newline) | `cat -v entrypoint.sh` |
| `tac filename` | Concatenate and display files in reverse line order (bottom to top) | `tac /var/log/dpkg.log` |
| `head -n [num] filename` | Output the first specified number of lines of a file | `head -n 5 users_export.csv` |
| `tail -n [num] filename` | Output the last specified number of lines of a file | `tail -n 20 /var/log/nginx/error.log` |
| `tail -f filename` | Follow and output appended data in real-time as the file grows | `tail -f /var/log/application.log` |
| `less filename` | Interactive file pager supporting forward/backward navigation and search | `less /var/log/syslog` |
| `od` / `hexdump` / `xxd` | Dump files in octal, hexadecimal, or custom byte formats | `hexdump -C server.crt \| head -n 10` |

---

## 2. Text Extraction & Line Counting

| Command / Syntax | Description | Practical Command |
| :--- | :--- | :--- |
| `wc filename` | Print newline, word, and byte counts for a file | `wc metrics.csv` |
| `wc -l filename` | Print the total number of newlines (line count) | `docker ps -q \| wc -l` |
| `wc -w filename` | Print the total word count | `wc -w CHANGELOG.md` |
| `wc -c filename` | Print the total byte count | `wc -c payload.json` |
| `cut -d '<delim>' -f <n>` | Extract specific delimited fields from each line | `cut -d ',' -f 1 users.csv` |
| `paste file1 file2` | Merge lines of files sequentially separated by TABs | `paste hosts.txt ips.txt` |
| `split -l [lines] filename` | Split a file into fixed-size chunks based on line count | `split -l 10000 massive_dump.sql chunk_` |

---

## 3. Sorting & Deduplication

| Command / Syntax | Description | Practical Command |
| :--- | :--- | :--- |
| `sort filename` | Sort text lines alphabetically | `sort hostnames.txt` |
| `sort -n filename` | Compare according to numerical string value | `ps -ef \| awk '{print $2}' \| sort -n` |
| `sort -r filename` | Reverse the result of comparisons | `sort -r versions.txt` |
| `sort -k [num]` | Sort via a key at a specific column position | `sort -k 9,9 access.log` |
| `sort file \| uniq` | Filter out adjacent repeated duplicate lines | `cut -d ' ' -f 1 access.log \| sort \| uniq` |
| `sort file \| uniq -c` | Prefix lines by the number of occurrences | `grep "ERROR" app.log \| sort \| uniq -c` |
| `uniq -d filename` | Only print duplicate lines present in sorted input | `sort uids.txt \| uniq -d` |
| `uniq -u filename` | Only print unique lines (never repeated) | `sort nodes.txt \| uniq -u` |

---

## 4. I/O Redirection & Stream Handling

| Redirection Operator | Description | Practical Command |
| :--- | :--- | :--- |
| `> file` | Redirect standard output (stdout) and overwrite target file | `generate-config > generated.conf` |
| `>> file` | Redirect standard output (stdout) and append to target file | `echo 'export PATH="$PATH:/usr/local/bin"' >> ~/.bashrc` |
| `2> file` | Redirect standard error (stderr) and overwrite target file | `make build 2> build_errors.log` |
| `2>> file` | Redirect standard error (stderr) and append to target file | `certbot renew 2>> /var/log/certbot_errors.log` |
| `&> file` | Redirect both stdout and stderr (overwrite) | `docker build -t app:v1 . &> build.log` |
| `&>> file` | Redirect both stdout and stderr (append) | `helm upgrade --install web app/ &>> deploy.log` |
| `command < file` | Feed file content directly into command standard input (stdin) | `mysql -u root -p production_db < schema.sql` |
| `cmd1 \| cmd2` | Pipe stdout of cmd1 directly into stdin of cmd2 | `ps aux \| grep "nginx"` |

---

## 5. Pattern Matching with Grep & Regex

| Command / Syntax | Description | Practical Command |
| :--- | :--- | :--- |
| `grep "pattern" file` | Search for lines matching basic regular expression pattern | `grep "FATAL" application.log` |
| `grep -i "pattern" file` | Perform case-insensitive pattern matching | `grep -i "unauthorized" auth.log` |
| `grep -v "pattern" file` | Invert match to select non-matching lines | `grep -v "kube-probe" access.log` |
| `grep -c "pattern" file` | Print only a count of selected lines per file | `grep -c "Connection refused" app.log` |
| `grep -n "pattern" file` | Prefix each line of output with its 1-based line number | `grep -n "FAIL" test_results.log` |
| `grep -E "pattern" file` | Interpret pattern as an Extended Regular Expression (ERE) | `grep -E "404\|500" access.log` |
| `grep -r "pattern" /path` | Read all files under each directory recursively | `grep -r "10.0.0.1" /opt/configs/` |

---

## 6. Regular Expressions Reference

### 6.1 Core Metacharacters

| Symbol | Description | Practical Command |
| :--- | :--- | :--- |
| `^` | Match pattern anchored strictly to line start | `grep "^server_name" /etc/nginx/nginx.conf` |
| `$` | Match pattern anchored strictly to line end | `grep "sh$" /etc/passwd` |
| `.` | Match any single character except newline | `grep -E "v1\.2\.[0-9]" release_manifest.json` |
| `*` | Match preceding element zero or more times | `grep -E "listen[[:space:]]*" /etc/nginx/nginx.conf` |
| `\` | Escape next character to treat it literally | `grep -E "api\.example\.com" access.log` |

### 6.2 Character Sets & Ranges

| Syntax | Description | Practical Command |
| :--- | :--- | :--- |
| `[abc]` | Match any single character contained within brackets | `grep -E "web-[psd]" cluster_hosts.txt` |
| `[^abc]` | Match any single character NOT contained within brackets | `grep -E "[^0-9]" metrics_raw.txt` |
| `[a-z]` | Match any single character within character range | `grep -E "192\.168\.1\.[0-9]+" network_scan.log` |

### 6.3 Extended Metacharacters (`grep -E`)

| Symbol | Description | Practical Command |
| :--- | :--- | :--- |
| `+` | Match preceding element one or more times | `grep -E "ERROR +[0-9]+" app.log` |
| `?` | Match preceding element zero or one time (optional) | `grep -E "https?://" endpoint_list.txt` |
| `{n,m}` | Match preceding element at least `n` and at most `m` times | `grep -E "AKIA[0-9A-Z]{16}" credentials.txt` |
| `\|` | Logical OR operation between two patterns | `grep -E "CRITICAL\|FATAL\|EMERGENCY" syslog` |

---

## 7. Stream Transformation & Editing

| Command / Syntax | Description | Practical Command |
| :--- | :--- | :--- |
| `tr '[a-z]' '[A-Z]'` | Translate lowercase characters to uppercase | `echo "database_url" \| tr '[a-z]' '[A-Z]'` |
| `tr -d '[chars]'` | Delete specified set of characters from stdin | `tr -d '\r' < script.sh > script_unix.sh` |
| `tr -s '[char]'` | Squeeze repeated occurrences of characters into a single instance | `cat server.log \| tr -s ' '` |
| `sed 's/old/new/' file` | Substitute first occurrence of pattern per line | `sed 's/localhost/db.internal/' config.json` |
| `sed 's/old/new/g' file` | Substitute all occurrences of pattern globally across all lines | `sed 's/v1.0.0/v1.1.0/g' deployment.yaml` |
| `sed '/pattern/d' file` | Delete lines matching the specified pattern | `sed '/^#/d' /etc/redis/redis.conf` |

---

## 8. File Integrity Verification

| Command / Syntax | Description | Practical Command |
| :--- | :--- | :--- |
| `md5sum filename` | Compute 128-bit MD5 message digest / checksum | `md5sum app_linux_amd64_v1.0.0.zip` |
| `md5sum -c checksums.txt` | Read checksums from file and verify match against actual files | `md5sum -c CHECKSUMS.md5` |
`

