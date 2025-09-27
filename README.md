# linux-activity
this is my activity
LP-Activity This is my LP Activity 1 and 2

Activity 1

Q1:Using “man command” can you provide me the explanations of the output for the following commands: ls -b, ls -c, ls -d, …., ls -z Ans: ls -a, --all

Man excerpt: -a, --all — do not ignore entries starting with . Description: Show all directory entries, including hidden files that start with .. Meaning / Use: Use to view dotfiles (e.g., .bashrc, .profile) and the special entries . and ... Useful for troubleshooting/configuration. Effect on output: Adds . (current directory), .. (parent), and any other dotfiles to the listing. Example: ls Desktop Documents Downloads ls -a . .. .bashrc .profile Desktop Documents Downloads

ls -b, --escape

Man excerpt: -b, --escape — print C-style escapes for nongraphic characters Description: Replace nonprintable characters in filenames with backslash escapes (octal like \040 for space). Meaning / Use: Helpful for identifying filenames that contain spaces, newlines, tabs or other weird characters. Effect on output: Filenames are shown with escape sequences instead of invisible/control characters. Example: ls -b My\040File normal.txt ls -lb -rw-r--r-- 1 alice staff 1024 Aug 25 My\040File

ls -c

Man excerpt: -c — with -l/-t: use ctime (status change time) Description: Use file ctime (time of last status change) for sorting/display when combined with other flags. Meaning / Use: Find files whose metadata changed recently (permissions, owner, link count). Effect on output: When combined with -l or -t, the timestamp and/or sort order reflect ctime instead of modification time. Example: ls -lc -rw-r--r-- 1 root root 512 Aug 26 11:40 perms_changed.conf

ls -d, --directory

Man excerpt: -d, --directory — list directories themselves, not their contents Description: Show directory entries rather than expanding and listing their contents. Meaning / Use: Inspect directory metadata (permissions/owner/size of the directory entry) without listing files inside. Effect on output: For a directory argument, prints a single line for that directory (like a file). Example: ls -ld /etc drwxr-xr-x 250 root root 12288 Aug 26 /etc

ls -e (implementation note)

Man excerpt: -e / --full-time (implementation dependent) — print full timestamp (including seconds/nanoseconds) Description: Show complete timestamp with seconds and fractional seconds (on systems that support it). On many systems --full-time is the explicit option; -e may be supported in some ls versions for extended time output. Meaning / Use: Use when you need very precise time information. Effect on output: Time column shows full date/time including seconds and fractional seconds. Example: ls -le file.txt -rw-r--r-- 1 alice staff 123 Aug 26 2025 12:34:56.123456789 file.txt

If ls -e is not recognized, use ls --full-time on GNU coreutils.

ls -f

Man excerpt: -f — do not sort; output in directory order (implies -a) Description: Disable sorting; list in filesystem/directory order. Implies -a (shows hidden files). Meaning / Use: Fast listing for very large directories; see entries in the raw order directory stores them. Effect on output: Names appear unsorted; hidden files are shown. Useful to see the exact directory order. Example: ls -f . .. .hidden file3 file1 file2

ls -F, --classify

Man excerpt: -F, --classify — append indicator (one of /=>@|) to entries Description: Append a character to entry names showing their type: / for directories, * for executables, @ for symlinks, | for FIFOs, = for sockets (varies slightly by system). Meaning / Use: Quickly see which entries are directories/executables/symlinks. Effect on output: Names include a trailing indicator. Example: ls -F bin/ script.sh link@ notes.txt

ls -g

Man excerpt: -g — like -l but do not show owner Description: Produce long listing but omit the owner (user) column — usually used when the owner is irrelevant. Meaning / Use: Space saver when group and perms matter but not username. Effect on output: -l format without the owner column. Example: ls -lg -rw-r--r-- 1 staff 1.2K Aug 25 notes.txt drwxr-xr-x 2 staff 4.0K Aug 26 projects/

ls -h, --human-readable

Man excerpt: -h, --human-readable — with -l, print sizes in human readable format (e.g., 1K 234M) Description: Convert byte counts into human-friendly units. Meaning / Use: Easier to read file sizes than raw bytes. Effect on output: The size column displays K, M, G units. Example: ls -lh -rw-r--r-- 1 alice staff 1.2K Aug 25 notes.txt -rw-r--r-- 1 alice staff 10M Aug 20 video.mp4

ls -i, --inode

Man excerpt: -i, --inode — print the index number (inode) of each file Description: Show the filesystem inode number before the filename. Meaning / Use: Useful for identifying files, finding hard links, or low-level filesystem checks. Effect on output: An extra numeric column (inode) appears at line start. Example: ls -li 3054199 -rw-r--r-- 1 alice staff 1024 Aug 25 report.txt 3054200 -rw-r--r-- 1 alice staff 512 Aug 24 summary.txt

ls -l (reference — long listing)

Man excerpt: -l — use a long listing format Description: Show file type & permissions, hard link count, owner, group, size, timestamp, and filename. Meaning / Use: Inspect detailed file metadata. (Your earlier example is same format.) Effect on output: Seven main fields: perms links owner group size time name. Example: ls -l -rw-r--r-- 1 alice staff 1024 Aug 25 12:00 notes.txt drwxr-xr-x 2 root root 4096 Aug 26 projects lrwxrwxrwx 1 bob users 11 Aug 20 link -> /etc/hosts

ls -L, --dereference

Man excerpt: -L, --dereference — when listing a symbolic link, show info for the file it points to Description: Follow symlink(s) and display the target file’s metadata rather than the symlink itself. Meaning / Use: Use when you want the real file’s info instead of the link’s attributes. Effect on output: ls -lL symlink prints the target’s permissions/size/etc. (instead of l type and -> target). Example: ls -l link lrwxrwxrwx 1 bob users 11 Aug 20 link -> /etc/hosts ls -lL link -rw-r--r-- 1 root root 500 Aug 02 /etc/hosts

ls -m

Man excerpt: -m — stream output format; fill width with a comma separated list Description: Print filenames across the screen separated by commas. Meaning / Use: Useful for compact, single-line lists for copy/paste or quick scanning. Effect on output: Names are printed in a comma-separated stream. Example: ls -m file1, file2, file3, projects

ls -n, --numeric-uid-gid

Man excerpt: -n, --numeric-uid-gid — like -l, but show numeric user and group IDs Description: Show numeric UID and GID instead of resolving them to names. Meaning / Use: Useful for scripts or when usernames/groups are not resolvable. Effect on output: Owner and group columns are numbers (UID/GID). Example: ls -ln -rw-r--r-- 1 1000 100 1024 Aug 25 notes.txt

ls -o

Man excerpt: -o — like -l but do not show group information Description: Long listing without the group column. (Similar to -g which omits owner.) Meaning / Use: Cleaner -l output when group is not required. Effect on output: -l fields minus the group column. Example: ls -lo -rw-r--r-- 1 alice 1024 Aug 25 notes.txt

ls -p

Man excerpt: -p — append / indicator to directories Description: Add a / after directory names in the name column. Meaning / Use: Quick visual recognition of directories in a name-only listing. Effect on output: Directory names end with a /. Example: ls -p file.txt projects/ scripts/

ls -q

Man excerpt: -q — print ? for nongraphic characters Description: Replace control/nonprintable characters in names with ? for safe display. Meaning / Use: Makes output readable when filenames contain control characters. Effect on output: Nonprintable characters replaced with ?. Example: ls -q My?File normal.txt

ls -Q, --quote-name

Man excerpt: -Q, --quote-name — enclose entry names in double quotes Description: Put filenames in double quotes in output. Meaning / Use: Useful for clearly identifying names that contain spaces or special chars. Effect on output: Names are printed like "my file.txt". Example: ls -Q "my file.txt" "notes.txt"

ls -r, --reverse

Man excerpt: -r, --reverse — reverse order while sorting Description: Reverse whatever the sorted order would be (alphabetical, time, size). Meaning / Use: Useful to change newest→oldest or Z→A ordering. Effect on output: Sort order reversed. Example: ls -ltr -rw-r--r-- 1 alice staff 256 Aug 25 older.txt -rw-r--r-- 1 alice staff 512 Aug 26 newest.txt

ls -R, --recursive

Man excerpt: -R, --recursive — list subdirectories recursively Description: Descend into subdirectories and list their contents too. Meaning / Use: Get a full tree of all files beneath a directory. For large trees, output can be lengthy. Effect on output: ls prints each directory path followed by its content. Example: ls -R .: file1 dir1 ./dir1: file2 sub/

ls -s, --size

Man excerpt: -s, --size — print allocated block counts (in blocks) before each file Description: Show the number of filesystem blocks used by each file (block size depends on system). Meaning / Use: Quick view of disk usage in block units. For exact bytes, use other tools (du, stat). Effect on output: A block count column appears at start of each line. Example: ls -ls total 12 4 -rw-r--r-- 1 alice staff 1024 Aug 25 notes.txt 8 -rw-r--r-- 1 alice staff 8192 Aug 20 video.mp4

ls -S

Man excerpt: -S — sort by file size, largest first Description: Order entries by size rather than name/time. Meaning / Use: Find large files quickly. Combine with -h to read sizes easily. Effect on output: Entries sorted descending by file size. Example: ls -lS -rw-r--r-- 1 alice staff 10M Aug 20 video.mp4 -rw-r--r-- 1 alice staff 1.2K Aug 25 notes.txt

ls -t

Man excerpt: -t — sort by modification time, newest first Description: Order files so the most recently modified appear at the top. Meaning / Use: Quickly identify recently changed files. Combine with -l for timestamps. Effect on output: Entries sorted by modification time descending. Example: ls -lt -rw-r--r-- 1 alice staff 512 Aug 26 newest.txt -rw-r--r-- 1 alice staff 256 Aug 25 older.txt

ls -T, --tabsize

Man excerpt: -T, --tabsize=COLS — set tab size used to format output Description: Change the assumed width of a tab character when aligning columns. Meaning / Use: Tweak column alignment if filenames contain tabs or for custom formatting. Effect on output: Alters spacing/alignment in multi-column displays. Example: ls -T 4

(affects column alignment; visual effect depends on file names)
ls -u

Man excerpt: -u — use access time (atime) instead of modification time (mtime) for sorting/display Description: Show/sort by last access time (when file was last read). Meaning / Use: Useful to find files that were recently read/opened (e.g., cache files). Effect on output: Timestamp column and -t sort refer to atime. Example: ls -lu -rw-r--r-- 1 alice staff 512 Aug 26 08:00 recently_read.log

ls -v

Man excerpt: -v — natural sort of (version) numbers within text Description: Sorts strings with embedded numbers in a way humans expect (e.g., file2 before file10). Meaning / Use: Useful for versioned filenames like file1 file2 file10. Effect on output: Orders numeric parts naturally, not lexicographically. Example: ls -v file1 file2 file10

ls -w, --width (implementation dependent)

Man excerpt: -w, --width=COLS — set output width (implementation may vary) Description: Some ls implementations support setting the output width for multi-column display. Meaning / Use: Control wrapping/column layout for terminals or for capturing output. Effect on output: Changes how many columns are used; visual effect depends on terminal and filenames. Example: ls -w 80

(affects column wrapping; output depends on environment)
ls -x

Man excerpt: -x — list entries by lines across the page, sorted horizontally Description: Print entries in rows across the screen (row-major), rather than down columns. Meaning / Use: Alternative layout that can be easier to scan horizontally. Effect on output: Layout changed; content unchanged. Example: ls -x file1 file2 file3 file4

ls -X

Man excerpt: -X — sort alphabetically by extension Description: Sort files grouped by file extension (e.g., .txt together). Meaning / Use: Useful when you want files with same extension grouped. Effect on output: Ordering by suffix/extension rather than whole name. Example: ls -X a.txt b.txt a.c b.c image.png

ls -Z / --context (SELinux), and notes about -z

Man excerpt: -Z, --context — print any SELinux security context of each file (if available) Description: Show SELinux security context (user:role:type:level) for files on SELinux-enabled systems. Some implementations also offer -z or use uppercase -Z; check man ls on your system. Meaning / Use: Important for administrators managing SELinux labels and permissions. Effect on output: An extra field with the SELinux context is shown (often before size or after permissions). Example: ls -lZ -rw-r--r--. 1 root root system_u:object_r:etc_t:s0 1234 Aug 26 /etc/hosts drwxr-xr-x. 2 root root system_u:object_r:etc_t:s0 4096 Aug 26 /etc/

Note: On many systems the option is -Z (capital). If your ls accepts -z for this purpose, it is implementation dependent — verify with man ls.

Q2:Can you explore the following commands on your own: • whoami, pwd • cd • cd / • cd .. • cd <path Ans:

whoami
Description: The whoami command prints the username of the current logged-in user. Meaning / Use: Useful to confirm which user account you are using. Especially important when working with multiple users or switching with su/sudo. Example Output: //whoami # Print the logged-in user's name whoami student

pwd
Description: The pwd command prints the Present Working Directory — i.e., the full path of the directory you are currently in. Meaning / Use: Lets you know exactly where you are in the filesystem hierarchy. Helpful when navigating deep directory structures. Example Output: pwd # Print the present working directory pwd /home/student/projects

cd (change directory)
Description: The cd command is used to change the current directory in Linux. / Use: Moves you from one location in the filesystem to another. Works with absolute or relative paths.

Variants:

cd / Changes to the root directory /. Example: cd / pwd /

cd .. Moves up one level (parent directory). Example: pwd /home/student/projects cd .. pwd /home/student

cd Moves to the directory specified in . Example: cd /etc pwd /etc

cd (with no arguments) Moves you back to your home directory. Example: cd pwd /home/student

Activity-2

Q3:. Using “man command” can you provide me the explanations of the output for the following commands: tree -a, tree -d, tree -u, …., tree -p.

🔹 tree -a

Explanation: The tree -a command lists all files and directories, including hidden ones (those starting with .). Normally, hidden files are skipped by default. . (dot): Represents the current directory. .. (dot-dot): Represents the parent directory. Hidden files: Such as .bashrc, .config. Sample Output: tree -a . ├── .hidden ├── .config ├── file1.txt └── dir1

🔹 tree -d

Explanation: The tree -d command shows directories only, ignoring regular files. Useful for viewing just the folder structures Sample Output: tree -d . ├── dir1 ├── dir2 └── dir3

🔹 tree -u

Explanation: The tree -u command shows the owner (user) of each file and directory. Displays the username who owns the file. Similar to the Owner column in ls -l. Sample Output: tree -u . ├── [student] file1.txt └── [root] dir1

🔹 tree -g Explanation: The tree -g command shows the group ownership of files and directories. Displays the group name associated with each file. Similar to the Group column in ls -l. Sample Output: tree -g . ├── [staff] file1.txt └── [root] dir1

🔹 tree -p

Explanation: The tree -p command shows permissions for each file and directory. Uses the same format as ls -l (e.g., drwxr-xr-x, -rw-r--r--). Indicates who can read, write, or execute a file/directory. Sample Output: tree -p . ├── [-rw-r--r--] file1.txt └── [drwxr-xr-x] dir1

Q4: Can you explore the following commands on your own: • ifconfig • ping • traceroute • nmap • mkdi Ans: 🔹 ifconfig

Explanation: The ifconfig command (interface configuration) is used to display and configure network interfaces on Linux. Interface Name: The name of the network interface (e.g., eth0, wlan0, lo). IP Address (inet): The IPv4 address assigned to the interface. Netmask: The subnet mask of the network. Broadcast Address: The broadcast address used by the interface. MAC Address (ether): The hardware (physical) address of the network card. RX/TX Packets: Received and transmitted packet statistics. Sample Output:

ifconfig eth0: inet 192.168.1.10 netmask 255.255.255.0 broadcast 192.168.1.255 ether 00:0c:29:5d:6a:4b RX packets 1200 TX packets 800 lo: inet 127.0.0.1 netmask 255.0.0.0

🔹 ping Explanation: The ping command tests connectivity to another host by sending ICMP echo requests. Hostname/IP: The system you are testing connection to. Bytes: Size of the packet sent. Time: The round-trip time for the packet. TTL (Time To Live): The hop limit of the packet. Statistics: At the end, shows packet loss and average time. Sample Output:

ping -c 3 google.com PING google.com (142.250.185.78) 56(84) bytes of data. 64 bytes from 142.250.185.78: icmp_seq=1 ttl=118 time=23.5 ms 64 bytes from 142.250.185.78: icmp_seq=2 ttl=118 time=23.3 ms 64 bytes from 142.250.185.78: icmp_seq=3 ttl=118 time=23.7 ms

--- google.com ping statistics --- 3 packets transmitted, 3 received, 0% packet loss, avg time = 23.5 ms

🔹 traceroute

Explanation: The traceroute command shows the path taken by packets to reach a destination host. Hop Number: Sequence of routers along the path. Router Address: IP or hostname of each hop. Time: Round-trip times for packets to each hop. Sample Output:

traceroute google.com 1 router (192.168.1.1) 1.234 ms 2 isp.net (10.20.30.1) 12.345 ms 3 142.250.185.78 (google.com) 23.456 ms

🔹 nmap

Explanation: The nmap (Network Mapper) command is used to scan hosts for open ports and services. Host: The target system (IP or hostname). Port Number: The communication port being scanned. State: Whether the port is open, closed, or filtered. Service: The service running on that port (e.g., ssh, http). Sample Output:

nmap localhost

Starting Nmap 7.80 ( https://nmap.org ) Nmap scan report for localhost (127.0.0.1) PORT STATE SERVICE 22/tcp open ssh 80/tcp open http 3306/tcp open mysql

🔹 mkdir

Explanation: The mkdir (make directory) command is used to create a new directory. Directory Name: The name of the new folder to be created. Path: If a full path is provided, it creates the directory at that location. Options: -p allows creating parent directories if they do not exist. Sample Output:

mkdir myfolder ls Desktop Documents Downloads myfolder


No packages published
Footer
©
