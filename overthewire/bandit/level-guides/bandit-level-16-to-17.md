# Bandit Level 16 to Level 17

In this level, you will learn how to scan a range of ports, identify open services, test SSL/TLS services, extract a returned SSH private key, and use that key to log in as the next Bandit user.

This level is a noticeable jump from the previous networking levels. Earlier, you were given a specific port. In this level, you are given a port range. You have to discover the open services, test them, identify the correct one, save the returned private key, download it to your local WSL environment, and then use it to authenticate as `bandit17`.

This guide does not publish active passwords or private keys. The goal is to help you understand the method, the command behavior, and the real-world lesson behind the exercise.

## 1. Level Information

<table>
  <tr>
    <th width="35%">Field</th>
    <th width="65%">Response</th>
  </tr>
  <tr>
    <td>Wargame</td>
    <td>OverTheWire Bandit<br><br></td>
  </tr>
  <tr>
    <td>Level</td>
    <td>Bandit Level 16 to Level 17<br><br></td>
  </tr>
  <tr>
    <td>Category</td>
    <td>Linux fundamentals, networking, service discovery, port scanning, SSL/TLS, OpenSSL, temporary workspaces, SCP, SSH private keys<br><br></td>
  </tr>
  <tr>
    <td>Difficulty</td>
    <td>Intermediate<br><br></td>
  </tr>
  <tr>
    <td>Spoiler posture</td>
    <td>Teaching notes with guided walkthrough. The active password and private key are not published.<br><br></td>
  </tr>
  <tr>
    <td>Password policy</td>
    <td>This guide explains how to retrieve and use the next credential but does not include the password or private key value.<br><br></td>
  </tr>
</table>

## 2. Learning Objective

By the end of this level, you should understand how to scan a local port range, identify open ports, test candidate SSL/TLS services, extract a private key from command output, protect the key with file permissions, download it to your local machine, and use it to authenticate as another user.

<table>
  <tr>
    <th width="30%">Learning Layer</th>
    <th width="70%">Objective</th>
  </tr>
  <tr>
    <td>Beginner</td>
    <td>You will learn how to create a temporary working directory, scan ports with <code>nmap</code>, and identify open services.<br><br></td>
  </tr>
  <tr>
    <td>Practitioner</td>
    <td>You will practice using a shell loop to test multiple ports with <code>openssl s_client</code> and search the results for a returned private key.<br><br></td>
  </tr>
  <tr>
    <td>Advanced</td>
    <td>You will connect this exercise to a broader security workflow: discovery, enumeration, protocol testing, credential handling, local versus remote context, and secure transfer of sensitive material.<br><br></td>
  </tr>
</table>

## 3. Level Summary

The official level goal says there is a service listening on one of the ports between `31000` and `32000` on `localhost`.

The correct service will return credentials for the next level after you submit the current `bandit16` password. However, not every open service is the correct service. Some services may simply echo input back to you, and some ports may not return anything useful.

That gives you several useful facts:

```text
Current user: bandit16
Current password file: /etc/bandit_pass/bandit16
Target host: localhost
Target port range: 31000-32000
Connection type: SSL/TLS for the useful service
Expected result: private SSH key for bandit17
```

A high-level workflow is:

```bash
cd "$(mktemp -d)"
nmap -p 31000-32000 localhost
nmap -p 31000-32000 --open -oG - localhost | awk '/Ports:/{print $0}'
```

Then test the open ports with `openssl s_client`, search the output files for the private key, extract the key, protect it, download it to your local WSL environment, and use it to log in as `bandit17`.

Official level reference:

```text
https://overthewire.org/wargames/bandit/bandit17.html
```

## 4. Concepts Introduced

<table>
  <tr>
    <th width="30%">Concept</th>
    <th width="70%">Explanation</th>
  </tr>
  <tr>
    <td>Temporary workspace</td>
    <td>The Bandit home directories are not writable. A temporary directory under <code>/tmp</code> gives you a safe place to create output files and save the returned key.<br><br></td>
  </tr>
  <tr>
    <td><code>mktemp -d</code></td>
    <td><code>mktemp -d</code> creates a randomly named temporary directory. This is better than manually creating a predictable folder name under <code>/tmp</code>.<br><br></td>
  </tr>
  <tr>
    <td>Port scanning</td>
    <td>Port scanning checks which network ports are open on a host. In this level, you scan ports <code>31000</code> through <code>32000</code> on <code>localhost</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>nmap</code></td>
    <td><code>nmap</code> is a network scanning tool used to discover hosts, open ports, and sometimes service information.<br><br></td>
  </tr>
  <tr>
    <td>Open port</td>
    <td>An open port means a service is listening. It does not automatically mean that the service is useful for the level.<br><br></td>
  </tr>
  <tr>
    <td><code>openssl s_client</code></td>
    <td><code>openssl s_client</code> connects to SSL/TLS-enabled services. In this level, it is used to submit the current password to candidate ports.<br><br></td>
  </tr>
  <tr>
    <td>Shell loop</td>
    <td>A shell loop lets you repeat a command for multiple values. Here, it lets you test each open port without manually typing the same command over and over.<br><br></td>
  </tr>
  <tr>
    <td><code>grep</code></td>
    <td><code>grep</code> searches text. In this level, it helps identify which output file contains the private key.<br><br></td>
  </tr>
  <tr>
    <td><code>sed</code></td>
    <td><code>sed</code> can extract a specific range of lines. Here, it extracts only the private key block from the service output.<br><br></td>
  </tr>
  <tr>
    <td>SCP</td>
    <td><code>scp</code> securely copies files over SSH. In this level, it downloads the private key from the Bandit server to your local WSL environment.<br><br></td>
  </tr>
  <tr>
    <td>Private SSH key</td>
    <td>A private SSH key is credential material. It must be protected, redacted from screenshots, and never committed to GitHub.<br><br></td>
  </tr>
</table>

## 5. What You Should Notice

As you work through the level, pause on the observations that matter. The goal is not only to run the right command, but to understand why that command is appropriate.

<table>
  <tr>
    <th width="35%">Observation</th>
    <th width="65%">Why It Matters</th>
  </tr>
  <tr>
    <td>The home directory is not writable.</td>
    <td>You need to work in a temporary directory under <code>/tmp</code>. This is why the guide starts with <code>cd "$(mktemp -d)"</code>.<br><br></td>
  </tr>
  <tr>
    <td>You are given a port range, not a specific port.</td>
    <td>This level requires discovery. You must scan the range to identify which ports are open.<br><br></td>
  </tr>
  <tr>
    <td>Multiple services are open.</td>
    <td>Not every open service is the correct one. You need to test the services and inspect their responses.<br><br></td>
  </tr>
  <tr>
    <td>Some output files may be empty.</td>
    <td>An empty output means that port did not return useful content through the command you ran. That is part of the discovery process.<br><br></td>
  </tr>
  <tr>
    <td>One service returns a private key.</td>
    <td>The returned key is the credential for the next level. It must be extracted carefully and protected.<br><br></td>
  </tr>
  <tr>
    <td>The key should be downloaded locally.</td>
    <td>Current OverTheWire behavior may prevent logging in from one level to another through <code>localhost</code>. Downloading the key to local WSL and connecting to the public Bandit host is a more reliable workflow.<br><br></td>
  </tr>
</table>

## 6. Guided Hints

Use these hints progressively. Try Hint 1 first. Move to the next hint only if you are stuck.

<table>
  <tr>
    <th width="20%">Hint Level</th>
    <th width="80%">Hint</th>
  </tr>
  <tr>
    <td>Hint 1</td>
    <td>Create a temporary working directory first. The home directory is not the right place to save files.<br><br></td>
  </tr>
  <tr>
    <td>Hint 2</td>
    <td>Scan ports <code>31000</code> through <code>32000</code> on <code>localhost</code>.<br><br></td>
  </tr>
  <tr>
    <td>Hint 3</td>
    <td>Make a list of only the open ports. Testing only open ports is easier than testing every port in the range.<br><br></td>
  </tr>
  <tr>
    <td>Hint 4</td>
    <td>Use a loop to submit the current password to each open port with <code>openssl s_client</code>.<br><br></td>
  </tr>
  <tr>
    <td>Hint 5</td>
    <td>Search the output files for <code>BEGIN RSA PRIVATE KEY</code>.<br><br></td>
  </tr>
  <tr>
    <td>Hint 6</td>
    <td>Extract only the private key block, save it to a key file, and protect it with <code>chmod 600</code>.<br><br></td>
  </tr>
  <tr>
    <td>Hint 7</td>
    <td>Download the key to local WSL with <code>scp</code>, then use it with <code>ssh -i</code> to log in as <code>bandit17</code>.<br><br></td>
  </tr>
</table>

## 7. Commands Introduced

These commands are not just things to memorize. Each one teaches you something about discovery, automation, text processing, or credential handling.

<table>
  <tr>
    <th width="30%">Command or Tool</th>
    <th width="70%">Explanation</th>
  </tr>
  <tr>
    <td><code>ssh bandit16@bandit.labs.overthewire.org -p 2220</code></td>
    <td>Connects to the Bandit server as <code>bandit16</code> using the password retrieved in the previous level.<br><br></td>
  </tr>
  <tr>
    <td><code>cd "$(mktemp -d)"</code></td>
    <td>Creates a random temporary directory and immediately moves into it. This gives you a writable workspace under <code>/tmp</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>nmap -p 31000-32000 localhost</code></td>
    <td>Scans the specified port range on <code>localhost</code> and reports which ports are open.<br><br></td>
  </tr>
  <tr>
    <td><code>nmap -p 31000-32000 --open -oG - localhost</code></td>
    <td>Runs the scan in a cleaner output format and shows open ports. The <code>-oG -</code> option writes grepable output to the terminal.<br><br></td>
  </tr>
  <tr>
    <td><code>awk '/Ports:/{print $0}'</code></td>
    <td>Filters the grepable <code>nmap</code> output to show the line containing the open port list.<br><br></td>
  </tr>
  <tr>
    <td><code>ports="31046 31518 31691 31790 31960"</code></td>
    <td>Stores the open port numbers in a shell variable so a loop can test them one by one. Your open ports may differ, so use the ports from your own scan.<br><br></td>
  </tr>
  <tr>
    <td><code>for port in $ports; do ... done</code></td>
    <td>Runs the same command once for each port in the <code>ports</code> variable.<br><br></td>
  </tr>
  <tr>
    <td><code>openssl s_client -connect localhost:$port -quiet</code></td>
    <td>Connects to each candidate SSL/TLS service and submits the current password.<br><br></td>
  </tr>
  <tr>
    <td><code>grep -l "BEGIN RSA PRIVATE KEY" raw-key-output-*.txt</code></td>
    <td>Searches the output files and prints the filename that contains a private key.<br><br></td>
  </tr>
  <tr>
    <td><code>sed -n '/BEGIN RSA PRIVATE KEY/,/END RSA PRIVATE KEY/p'</code></td>
    <td>Extracts the private key block from the output file, starting at the BEGIN line and ending at the END line.<br><br></td>
  </tr>
  <tr>
    <td><code>chmod 600 bandit17.key</code></td>
    <td>Restricts the private key so only the owner can read and write it.<br><br></td>
  </tr>
  <tr>
    <td><code>scp -P 2220 ...</code></td>
    <td>Downloads the private key from the Bandit server to your local WSL environment. For <code>scp</code>, the port option is uppercase <code>-P</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>ssh -i bandit17.key bandit17@bandit.labs.overthewire.org -p 2220</code></td>
    <td>Uses the downloaded private key to authenticate as <code>bandit17</code>.<br><br></td>
  </tr>
</table>

## 8. Walkthrough Without Credential Disclosure

This walkthrough assumes you are working from a local terminal, such as Windows Subsystem for Linux, macOS Terminal, or a Linux shell. The examples below use WSL because it gives Windows users a Linux-like command-line environment.

### Step 1

Connect to the Bandit server as `bandit16`.

```bash
ssh bandit16@bandit.labs.overthewire.org -p 2220
```

When prompted, enter the password you retrieved from the previous level. The terminal may not show characters while you type the password. That is normal behavior.

After you log in successfully, your commands are running inside a remote Linux shell on the Bandit server.

### Step 2

Create a temporary working directory.

```bash
cd "$(mktemp -d)"
pwd
```

This creates a random writable directory under `/tmp` and moves you into it.

This matters because the Bandit home directory is not writable. You need somewhere to save scan outputs and the returned SSH key.

The `pwd` command prints your temporary directory path. It will look similar to:

```text
/tmp/tmp.Yfk6hsyBEB
```

Your path will probably be different. Save or remember this path because you will need it later when downloading the key to your local WSL environment.

### Step 3

Scan the port range.

```bash
nmap -p 31000-32000 localhost
```

This scans ports `31000` through `32000` on the Bandit server.

You should see several open ports. In one example run, the open ports were:

```text
31046
31518
31691
31790
31960
```

Do not assume your result will always be identical. Use the ports shown by your own scan.

### Step 4

Get a cleaner list of open ports.

```bash
nmap -p 31000-32000 --open -oG - localhost | awk '/Ports:/{print $0}'
```

This gives you a more compact output showing only the open port information.

Example output:

```text
Host: 127.0.0.1 (localhost)     Ports: 31046/open/tcp/////, 31518/open/tcp/////, 31691/open/tcp/////, 31790/open/tcp/////, 31960/open/tcp/////  Ignored State: closed (996)
```

This is easier to read than a long scan report.

### Step 5

Store the open ports in a variable.

Use the ports from your own scan. For example:

```bash
ports="31046 31518 31691 31790 31960"
```

This variable lets you test only the open ports instead of looping through the entire range.

### Step 6

Test each open port with OpenSSL.

Run this loop:

```bash
for port in $ports; do
  echo "Testing port $port"
  cat /etc/bandit_pass/bandit16 | openssl s_client -connect localhost:$port -quiet > "raw-key-output-$port.txt" 2>/dev/null
done
```

This command does several things:

<table>
  <tr>
    <th width="35%">Command Part</th>
    <th width="65%">Meaning</th>
  </tr>
  <tr>
    <td><code>for port in $ports</code></td>
    <td>Repeats the command once for every port stored in the <code>ports</code> variable.<br><br></td>
  </tr>
  <tr>
    <td><code>cat /etc/bandit_pass/bandit16</code></td>
    <td>Reads the current level password.<br><br></td>
  </tr>
  <tr>
    <td><code>|</code></td>
    <td>Pipes the current password into the next command.<br><br></td>
  </tr>
  <tr>
    <td><code>openssl s_client -connect localhost:$port -quiet</code></td>
    <td>Connects to the current port using SSL/TLS and submits the password.<br><br></td>
  </tr>
  <tr>
    <td><code>&gt; "raw-key-output-$port.txt"</code></td>
    <td>Saves the response from that port into a separate file named for the port number.<br><br></td>
  </tr>
  <tr>
    <td><code>2&gt;/dev/null</code></td>
    <td>Suppresses noisy OpenSSL error or handshake output so the saved files are easier to inspect.<br><br></td>
  </tr>
</table>

The loop should print something like:

```text
Testing port 31046
Testing port 31518
Testing port 31691
Testing port 31790
Testing port 31960
```

### Step 7

List the output files.

```bash
ls -l
```

You should see several files named like:

```text
raw-key-output-31046.txt
raw-key-output-31518.txt
raw-key-output-31691.txt
raw-key-output-31790.txt
raw-key-output-31960.txt
```

Some files may be empty. That is normal. Empty files mean those ports did not return useful output through this test.

### Step 8

Find the file that contains the private key.

```bash
grep -l "BEGIN RSA PRIVATE KEY" raw-key-output-*.txt
```

This searches all of the output files and prints the name of the file that contains a private key.

Example result:

```text
raw-key-output-31790.txt
```

This tells you that port `31790` returned the key in this example.

### Step 9

Extract only the private key.

Use the filename returned by `grep`. For example:

```bash
sed -n '/BEGIN RSA PRIVATE KEY/,/END RSA PRIVATE KEY/p' raw-key-output-31790.txt > bandit17.key
```

This creates a clean key file named:

```text
bandit17.key
```

The `sed` command extracts only the private key block. That means it removes extra text such as:

```text
Correct!
```

and keeps only:

```text
-----BEGIN RSA PRIVATE KEY-----
[REDACTED PRIVATE KEY CONTENT]
-----END RSA PRIVATE KEY-----
```

### Step 10

Verify the key structure without displaying the full key.

```bash
head -n 1 bandit17.key
tail -n 1 bandit17.key
```

You should see:

```text
-----BEGIN RSA PRIVATE KEY-----
-----END RSA PRIVATE KEY-----
```

This verifies that the file starts and ends correctly.

Do not run `cat bandit17.key` for screenshots or public notes. The private key is credential material.

### Step 11

Protect the private key on the Bandit server.

```bash
chmod 600 bandit17.key
ls -l bandit17.key
pwd
```

The permissions should look like:

```text
-rw------- 1 bandit16 bandit16 1675 [date] bandit17.key
```

The `pwd` command prints the temporary directory path where the key is stored. You will need this path for `scp`.

Example:

```text
/tmp/tmp.Yfk6hsyBEB
```

### Step 12

Download the key to your local WSL environment.

Open a second WSL terminal or log out of the Bandit server. From your local WSL prompt, run:

```bash
scp -P 2220 bandit16@bandit.labs.overthewire.org:/tmp/YOUR-TEMP-DIR/bandit17.key ./bandit17.key
```

Replace `YOUR-TEMP-DIR` with the actual temporary directory name from `pwd`.

Example format:

```bash
scp -P 2220 bandit16@bandit.labs.overthewire.org:/tmp/tmp.Yfk6hsyBEB/bandit17.key ./bandit17.key
```

You will be prompted for the `bandit16` password. Enter the password from the previous level.

Important syntax details:

```text
scp uses uppercase -P for the port.
ssh uses lowercase -p for the port.
Use one colon between the host and remote path.
```

Correct:

```bash
scp -P 2220 bandit16@bandit.labs.overthewire.org:/tmp/tmp.Yfk6hsyBEB/bandit17.key ./bandit17.key
```

Incorrect:

```bash
scp -p 2220 bandit16@bandit.labs.overthewire.org:/tmp/tmp.Yfk6hsyBEB/bandit17.key ./bandit17.key
```

Incorrect:

```bash
scp -P 2220 bandit16@bandit.labs.overthewire.org::/tmp/tmp.Yfk6hsyBEB/bandit17.key ./bandit17.key
```

### Step 13

Protect the local copy of the key.

From your local WSL terminal:

```bash
chmod 600 bandit17.key
ls -l bandit17.key
```

SSH may refuse to use the key if the permissions are too open.

### Step 14

Log in as `bandit17`.

From your local WSL terminal:

```bash
ssh -i bandit17.key bandit17@bandit.labs.overthewire.org -p 2220
```

After logging in, confirm your user context:

```bash
whoami
```

You should see:

```text
bandit17
```

At this point, you have moved from `bandit16` to `bandit17`.

## 9. Command Output and Screenshots

Use this section to include terminal output or screenshots after redacting credentials and private key material.

### Relevant Command Output

```text
$ ssh bandit16@bandit.labs.overthewire.org -p 2220
bandit16@bandit.labs.overthewire.org's password:
[successful login output omitted]

$ cd "$(mktemp -d)"
$ pwd
/tmp/tmp.XXXXXXXXXX

$ nmap -p 31000-32000 localhost
PORT      STATE SERVICE
31046/tcp open  unknown
31518/tcp open  unknown
31691/tcp open  unknown
31790/tcp open  unknown
31960/tcp open  unknown

$ nmap -p 31000-32000 --open -oG - localhost | awk '/Ports:/{print $0}'
Host: 127.0.0.1 (localhost)     Ports: 31046/open/tcp/////, 31518/open/tcp/////, 31691/open/tcp/////, 31790/open/tcp/////, 31960/open/tcp/////  Ignored State: closed (996)

$ ports="31046 31518 31691 31790 31960"

$ for port in $ports; do
>   echo "Testing port $port"
>   cat /etc/bandit_pass/bandit16 | openssl s_client -connect localhost:$port -quiet > "raw-key-output-$port.txt" 2>/dev/null
> done
Testing port 31046
Testing port 31518
Testing port 31691
Testing port 31790
Testing port 31960

$ ls -l
raw-key-output-31046.txt
raw-key-output-31518.txt
raw-key-output-31691.txt
raw-key-output-31790.txt
raw-key-output-31960.txt

$ grep -l "BEGIN RSA PRIVATE KEY" raw-key-output-*.txt
raw-key-output-31790.txt

$ sed -n '/BEGIN RSA PRIVATE KEY/,/END RSA PRIVATE KEY/p' raw-key-output-31790.txt > bandit17.key

$ head -n 1 bandit17.key
-----BEGIN RSA PRIVATE KEY-----

$ tail -n 1 bandit17.key
-----END RSA PRIVATE KEY-----

$ chmod 600 bandit17.key
$ ls -l bandit17.key
-rw------- 1 bandit16 bandit16 1675 [date omitted] bandit17.key

$ pwd
/tmp/tmp.XXXXXXXXXX
```

From local WSL:

```text
$ scp -P 2220 bandit16@bandit.labs.overthewire.org:/tmp/tmp.XXXXXXXXXX/bandit17.key ./bandit17.key
bandit16@bandit.labs.overthewire.org's password:
bandit17.key                                      100% [transfer details omitted]

$ chmod 600 bandit17.key

$ ssh -i bandit17.key bandit17@bandit.labs.overthewire.org -p 2220
[successful login output omitted]

$ whoami
bandit17
```

### Screenshots

<img width="710" height="281" alt="image" src="https://github.com/user-attachments/assets/2e87edd8-cb92-4f7f-85ca-5b3d744fc5e6" />

<img width="792" height="590" alt="image" src="https://github.com/user-attachments/assets/15a74e1f-b39d-4d16-86da-f4885fd7ac69" />

<img width="792" height="590" alt="image" src="https://github.com/user-attachments/assets/29e3aaf3-fde5-45d1-857f-3f962a6c901b" />

<img width="867" height="590" alt="image" src="https://github.com/user-attachments/assets/711ad7d5-a02d-4031-b7d9-38f9e208400a" />

<img width="867" height="590" alt="image" src="https://github.com/user-attachments/assets/2efa161b-95f0-42c3-a314-25fc27b13634" />

## 10. What Is Really Happening

This level combines several important cybersecurity skills.

First, you are performing service discovery. The level gives you a range of ports, but it does not tell you which exact port matters. That means you have to scan:

```bash
nmap -p 31000-32000 localhost
```

Second, you narrow the problem. Instead of testing every port from `31000` to `32000`, you identify only the open ports and store them in a variable:

```bash
ports="31046 31518 31691 31790 31960"
```

Third, you automate testing. The loop submits the current password to each candidate port and saves each result separately:

```bash
for port in $ports; do
  echo "Testing port $port"
  cat /etc/bandit_pass/bandit16 | openssl s_client -connect localhost:$port -quiet > "raw-key-output-$port.txt" 2>/dev/null
done
```

Fourth, you search for the useful response:

```bash
grep -l "BEGIN RSA PRIVATE KEY" raw-key-output-*.txt
```

This tells you which service returned a private key.

Fifth, you extract only the sensitive credential material you need:

```bash
sed -n '/BEGIN RSA PRIVATE KEY/,/END RSA PRIVATE KEY/p' raw-key-output-31790.txt > bandit17.key
```

Finally, you handle the private key like a real credential. You restrict its permissions, download it securely to your local machine, and use it to authenticate.

This workflow is a major step up because it combines discovery, automation, parsing, credential handling, and local-versus-remote context.

## 11. Common Mistakes

<table>
  <tr>
    <th width="35%">Mistake</th>
    <th width="65%">Correction</th>
  </tr>
  <tr>
    <td>Trying to save files in the home directory.</td>
    <td>The Bandit home directories are not writable. Use <code>cd "$(mktemp -d)"</code> to create and enter a temporary workspace under <code>/tmp</code>.<br><br></td>
  </tr>
  <tr>
    <td>Typing <code>PORT</code> literally in the OpenSSL command.</td>
    <td><code>PORT</code> is a placeholder. Replace it with a real port number, or use a loop with <code>$port</code>.<br><br></td>
  </tr>
  <tr>
    <td>Testing every port manually.</td>
    <td>Use <code>nmap</code> to identify open ports, store them in a variable, and test them with a loop.<br><br></td>
  </tr>
  <tr>
    <td>Assuming every open port is useful.</td>
    <td>Some open ports may return nothing or echo the password back. The correct one returns a private key.<br><br></td>
  </tr>
  <tr>
    <td>Using <code>cat raw-key-output*</code> and exposing the private key in screenshots.</td>
    <td>Use <code>grep</code>, <code>head</code>, and <code>tail</code> to verify the result without displaying the full key publicly.<br><br></td>
  </tr>
  <tr>
    <td>Saving the <code>Correct!</code> line inside the key file.</td>
    <td>Use <code>sed</code> to extract only the lines from <code>BEGIN RSA PRIVATE KEY</code> through <code>END RSA PRIVATE KEY</code>.<br><br></td>
  </tr>
  <tr>
    <td>Forgetting <code>chmod 600</code>.</td>
    <td>SSH may reject private keys with overly open permissions. Run <code>chmod 600 bandit17.key</code> before using the key.<br><br></td>
  </tr>
  <tr>
    <td>Trying to use the key from the Bandit server when localhost login is blocked.</td>
    <td>Download the key to local WSL with <code>scp</code>, then connect to <code>bandit17@bandit.labs.overthewire.org</code> from your local terminal.<br><br></td>
  </tr>
  <tr>
    <td>Using lowercase <code>-p</code> with <code>scp</code>.</td>
    <td>For <code>scp</code>, the port option is uppercase <code>-P</code>. For <code>ssh</code>, the port option is lowercase <code>-p</code>.<br><br></td>
  </tr>
  <tr>
    <td>Typing two colons in the <code>scp</code> remote path.</td>
    <td>Use one colon between the host and the remote path, like <code>bandit16@bandit.labs.overthewire.org:/tmp/tmp.XXXXXXXXXX/bandit17.key</code>.<br><br></td>
  </tr>
  <tr>
    <td>Publishing the private key in GitHub.</td>
    <td>Private keys are credentials. Redact them from screenshots, notes, writeups, and commit history.<br><br></td>
  </tr>
</table>

## 12. Defensive or Administrative Takeaway

This level introduces a professional workflow that appears in real security work.

From a defensive perspective, open ports are exposed interfaces. Administrators should know which services are listening, which protocols they require, who can reach them, and what information they return.

The level also reinforces that private keys must be treated like passwords. A private key can grant access to an account. If it is copied, exposed, committed, logged, or screenshotted, the account may be compromised.

The use of a temporary directory is also important. In shared systems, working in a random temporary directory helps reduce accidental exposure to other users and keeps your work organized.

## 13. Real-World Connection

Security analysts use port scanning to verify exposed services, validate firewall rules, identify unexpected listeners, and confirm that services are using the expected protocol.

They also use automation to test multiple services efficiently. The loop in this level is a simple version of a real testing workflow: discover targets, test each target, save results, search for important patterns, and act on the findings.

System administrators and defenders also need to understand secure credential handling. Private keys, API tokens, certificates, and passwords should be protected, transferred carefully, and never stored in public repositories.

This level is valuable because it connects several skills into one workflow:

```text
Discovery
Enumeration
Protocol testing
Automation
Text extraction
Credential protection
Secure file transfer
Authentication
```

That is why this level feels like a jump. It is no longer just one command. It is a small investigation.

## 14. Reflection Questions

Use these questions to check your understanding before moving to the next level. A good answer should explain the reasoning, not just repeat the command.

<table>
  <tr>
    <th width="35%">Question</th>
    <th width="65%">Learner Response</th>
  </tr>
  <tr>
    <td>What was the main concept in this level?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>Why did you need to create a temporary directory?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>Why did you scan a port range instead of connecting to one known port?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What does <code>nmap -p 31000-32000 localhost</code> do?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>Why did you store the open ports in a variable?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What does the <code>for</code> loop accomplish?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>Why did you use <code>grep</code> after testing the ports?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>Why did you use <code>sed</code> to extract the private key?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>Why should private keys be protected with <code>chmod 600</code>?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>Why did you download the key to local WSL before logging in as <code>bandit17</code>?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>How does this level connect to service discovery and defensive security?</td>
    <td><br><br></td>
  </tr>
</table>

## 15. References

Use these references to deepen your understanding after you complete the level. The goal is to learn the command behavior, not just finish the exercise.

<table>
  <tr>
    <th width="35%">Reference</th>
    <th width="65%">Why It Is Useful</th>
  </tr>
  <tr>
    <td>OverTheWire Bandit Level 16 to Level 17</td>
    <td>Provides the official level goal, including the port range and service-discovery requirement.<br><br></td>
  </tr>
  <tr>
    <td><code>man nmap</code></td>
    <td>Explains port scanning, service discovery, and scan options such as <code>-p</code>, <code>--open</code>, and output formats.<br><br></td>
  </tr>
  <tr>
    <td><code>man openssl</code></td>
    <td>Explains the OpenSSL command-line toolkit and its TLS-related functions.<br><br></td>
  </tr>
  <tr>
    <td><code>man s_client</code></td>
    <td>Explains how <code>openssl s_client</code> connects to SSL/TLS services and provides connection options.<br><br></td>
  </tr>
  <tr>
    <td><code>man grep</code></td>
    <td>Explains how to search text files for matching patterns.<br><br></td>
  </tr>
  <tr>
    <td><code>man sed</code></td>
    <td>Explains stream editing and line-range extraction.<br><br></td>
  </tr>
  <tr>
    <td><code>man scp</code></td>
    <td>Explains secure file copy syntax, including remote paths and the uppercase <code>-P</code> port option.<br><br></td>
  </tr>
  <tr>
    <td><code>man ssh</code></td>
    <td>Explains SSH authentication, identity files, hostnames, and ports.<br><br></td>
  </tr>
  <tr>
    <td><code>man chmod</code></td>
    <td>Explains file permissions, which are important when protecting private keys.<br><br></td>
  </tr>
</table>
