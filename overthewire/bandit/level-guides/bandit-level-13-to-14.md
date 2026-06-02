# Bandit Level 13 to Level 14

In this level, you will learn how SSH key-based authentication works and why private keys must be handled carefully.

The password for the next level is stored in `/etc/bandit_pass/bandit14`, but only the `bandit14` user can read it. Instead of giving you the password directly, this level gives you a private SSH key. The key can be downloaded to your local WSL environment and used to log in as `bandit14`.

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
    <td>Bandit Level 13 to Level 14<br><br></td>
  </tr>
  <tr>
    <td>Category</td>
    <td>Linux fundamentals, SSH, SCP, private keys, key-based authentication, file permissions, credential handling<br><br></td>
  </tr>
  <tr>
    <td>Difficulty</td>
    <td>Beginner to intermediate<br><br></td>
  </tr>
  <tr>
    <td>Spoiler posture</td>
    <td>Teaching notes with guided walkthrough. The active password and private key are not published.<br><br></td>
  </tr>
  <tr>
    <td>Password policy</td>
    <td>This guide explains how to retrieve the password but does not include the password value.<br><br></td>
  </tr>
</table>

## 2. Learning Objective

By the end of this level, you should understand how an SSH private key can authenticate a user without typing that user’s password. You should also understand how to use `scp` to copy a file from a remote server to your local WSL environment, how to protect a private key with file permissions, and why private keys should never be committed to GitHub.

<table>
  <tr>
    <th width="30%">Learning Layer</th>
    <th width="70%">Objective</th>
  </tr>
  <tr>
    <td>Beginner</td>
    <td>You will learn how to connect to the Bandit server, locate an SSH private key, read the level hint, copy the private key to your local WSL environment, and use it to log in as the next user.<br><br></td>
  </tr>
  <tr>
    <td>Practitioner</td>
    <td>You will practice using <code>scp</code> to download a file, <code>chmod 600</code> to restrict private key permissions, and <code>ssh -i</code> to authenticate with a specific key file.<br><br></td>
  </tr>
  <tr>
    <td>Advanced</td>
    <td>You will connect this exercise to a broader security principle: private keys are credentials. If a private key is exposed, copied carelessly, or committed to a repository, it can provide access to an account or system.<br><br></td>
  </tr>
</table>

## 3. Level Summary

The official level goal explains that the password for the next level is stored in:

```text
/etc/bandit_pass/bandit14
```

However, that file can only be read by the `bandit14` user.

In the `bandit13` home directory, you are given a private SSH key named:

```text
sshkey.private
```

The current OverTheWire environment may also include a file named:

```text
HINT
```

That file explains that logging in from one level to another through `localhost` is prevented in the current version of the game. Because of that, this guide uses a local WSL workflow: download the private key with `scp`, protect it with `chmod 600`, and then use the key from your local terminal to log in as `bandit14`.

A practical workflow is:

```bash
scp -P 2220 bandit13@bandit.labs.overthewire.org:/home/bandit13/sshkey.private ./bandit14.private
chmod 600 bandit14.private
ssh -i bandit14.private bandit14@bandit.labs.overthewire.org -p 2220
```

After logging in as `bandit14`, you can read the password file:

```bash
cat /etc/bandit_pass/bandit14
```

Do not commit the downloaded private key to GitHub. Even though this is a training environment, a private key is still credential material and should be handled like a password.

Official level reference:

```text
https://overthewire.org/wargames/bandit/bandit14.html
```

## 4. Concepts Introduced

<table>
  <tr>
    <th width="30%">Concept</th>
    <th width="70%">Explanation</th>
  </tr>
  <tr>
    <td>SSH key-based authentication</td>
    <td>SSH can authenticate users with a private key instead of a password. The private key proves identity when it matches a public key authorized for the target account.<br><br></td>
  </tr>
  <tr>
    <td>Private key</td>
    <td>A private key is a sensitive credential. Anyone who can use the private key may be able to authenticate as the associated account, depending on system configuration.<br><br></td>
  </tr>
  <tr>
    <td><code>scp</code></td>
    <td><code>scp</code>, or secure copy, copies files between a local system and a remote system over SSH. In this level, you use it to download the private key from the Bandit server to your local WSL environment.<br><br></td>
  </tr>
  <tr>
    <td><code>scp -P</code></td>
    <td>For <code>scp</code>, the uppercase <code>-P</code> option specifies the SSH port. This is different from <code>ssh</code>, which uses lowercase <code>-p</code> for the port.<br><br></td>
  </tr>
  <tr>
    <td>SCP remote path syntax</td>
    <td>An <code>scp</code> remote file path uses one colon between the hostname and the remote file path, such as <code>bandit13@bandit.labs.overthewire.org:/home/bandit13/sshkey.private</code>. A double colon is not correct for this workflow.<br><br></td>
  </tr>
  <tr>
    <td><code>ssh -i</code></td>
    <td>The <code>-i</code> option tells SSH which identity file, or private key, to use for authentication.<br><br></td>
  </tr>
  <tr>
    <td><code>chmod 600</code></td>
    <td><code>chmod 600</code> restricts a file so only the owner can read and write it. SSH commonly refuses to use private keys if their permissions are too open.<br><br></td>
  </tr>
  <tr>
    <td>Local versus remote context</td>
    <td>Some commands run on your local WSL system, while others run on the remote Bandit server. In this level, <code>scp</code>, <code>chmod</code>, and the final <code>ssh -i</code> command should be run from your local WSL terminal after you log out of Bandit.<br><br></td>
  </tr>
  <tr>
    <td>Level hint</td>
    <td>The <code>HINT</code> file explains that localhost login between levels is blocked in the current OverTheWire environment. Reading hints and error messages is part of the learning process.<br><br></td>
  </tr>
  <tr>
    <td>Account context</td>
    <td>The user account you are operating as determines what files you can read. As <code>bandit13</code>, you cannot read <code>/etc/bandit_pass/bandit14</code>. As <code>bandit14</code>, you can.<br><br></td>
  </tr>
  <tr>
    <td>Credential handling</td>
    <td>Private keys and passwords should not be committed to public repositories, pasted into screenshots, or shared in course materials.<br><br></td>
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
    <td>The home directory contains <code>sshkey.private</code>.</td>
    <td>This is the main clue. The level is not asking you to find the password directly as <code>bandit13</code>. It is giving you a different authentication method.<br><br></td>
  </tr>
  <tr>
    <td>The home directory may include a <code>HINT</code> file.</td>
    <td>The hint explains that localhost login between levels is blocked in the current OverTheWire environment. This is why the guide uses <code>scp</code> to download the private key and then logs in from local WSL.<br><br></td>
  </tr>
  <tr>
    <td>The password file belongs to the next user context.</td>
    <td>The file <code>/etc/bandit_pass/bandit14</code> can only be read after authenticating as <code>bandit14</code>.<br><br></td>
  </tr>
  <tr>
    <td>The key should be copied to your local WSL environment.</td>
    <td>Attempting to SSH from <code>bandit13</code> to <code>bandit14</code> through <code>localhost</code> may be blocked on the OverTheWire server. Downloading the key locally and connecting from WSL avoids that issue.<br><br></td>
  </tr>
  <tr>
    <td><code>scp</code> uses uppercase <code>-P</code> for the port.</td>
    <td>This is easy to confuse with SSH, which uses lowercase <code>-p</code>. For this copy command, use <code>scp -P 2220</code>.<br><br></td>
  </tr>
  <tr>
    <td>The remote path contains one colon.</td>
    <td>The correct syntax is <code>user@host:/remote/path</code>. If you type two colons, <code>scp</code> may look for a file path beginning with a colon and fail.<br><br></td>
  </tr>
  <tr>
    <td>The SSH command uses <code>-i bandit14.private</code>.</td>
    <td>This tells SSH to authenticate with the downloaded private key file instead of relying on a password prompt.<br><br></td>
  </tr>
  <tr>
    <td>The key permissions matter.</td>
    <td>Private keys should not be readable by other users. <code>chmod 600</code> restricts access to the local user who owns the file.<br><br></td>
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
    <td>Start by connecting as the correct Bandit user for the level. Then list the files in the home directory.<br><br></td>
  </tr>
  <tr>
    <td>Hint 2</td>
    <td>If you see a file named <code>HINT</code>, read it. It explains why the localhost method does not work in the current environment.<br><br></td>
  </tr>
  <tr>
    <td>Hint 3</td>
    <td>If you see a file named <code>sshkey.private</code>, think about how SSH can use a private key for authentication.<br><br></td>
  </tr>
  <tr>
    <td>Hint 4</td>
    <td>Download the key to your local WSL environment with <code>scp</code>. Remember that <code>scp</code> uses uppercase <code>-P</code> for the port.<br><br></td>
  </tr>
  <tr>
    <td>Hint 5</td>
    <td>Use one colon between the remote hostname and the remote path. The safest form is <code>bandit13@bandit.labs.overthewire.org:/home/bandit13/sshkey.private</code>.<br><br></td>
  </tr>
  <tr>
    <td>Hint 6</td>
    <td>Protect the key locally with <code>chmod 600</code> before using it with SSH.<br><br></td>
  </tr>
  <tr>
    <td>Hint 7</td>
    <td>Use the <code>-i</code> option with SSH to specify the downloaded private key file.<br><br></td>
  </tr>
  <tr>
    <td>Hint 8</td>
    <td>After you log in as <code>bandit14</code>, read the password file for that user.<br><br></td>
  </tr>
</table>

## 7. Commands Introduced

These commands are not just things to memorize. Each one teaches you something about remote login, secure copy, SSH keys, account context, or credential handling.

<table>
  <tr>
    <th width="30%">Command or Tool</th>
    <th width="70%">Explanation</th>
  </tr>
  <tr>
    <td><code>ssh bandit13@bandit.labs.overthewire.org -p 2220</code></td>
    <td>Connects from your local terminal to the remote OverTheWire Bandit server as user <code>bandit13</code> on port <code>2220</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>pwd</code></td>
    <td>Prints your current working directory. This helps you verify where you are after logging in.<br><br></td>
  </tr>
  <tr>
    <td><code>ls -l</code></td>
    <td>Lists files in long format, showing permissions, owner, group, size, and filename. This is useful when inspecting a private key file.<br><br></td>
  </tr>
  <tr>
    <td><code>cat HINT</code></td>
    <td>Displays the level hint provided by OverTheWire. In this level, it explains that logging in from one level to another through <code>localhost</code> is blocked and that learners should use the official level guidance.<br><br></td>
  </tr>
  <tr>
    <td><code>exit</code></td>
    <td>Closes the current shell session. In this level, use it to leave the Bandit server before running local WSL commands.<br><br></td>
  </tr>
  <tr>
    <td><code>scp -P 2220 bandit13@bandit.labs.overthewire.org:/home/bandit13/sshkey.private ./bandit14.private</code></td>
    <td>Copies <code>sshkey.private</code> from the remote <code>bandit13</code> account to your local WSL directory as <code>bandit14.private</code>. This full remote path form reduces confusion about where the file is located.<br><br></td>
  </tr>
  <tr>
    <td><code>chmod 600 bandit14.private</code></td>
    <td>Restricts the downloaded private key so only your local user can read and write it.<br><br></td>
  </tr>
  <tr>
    <td><code>ssh -i bandit14.private bandit14@bandit.labs.overthewire.org -p 2220</code></td>
    <td>Uses the downloaded private key file to authenticate as <code>bandit14</code> on the Bandit server.<br><br></td>
  </tr>
  <tr>
    <td><code>whoami</code></td>
    <td>Displays the current username. This is useful to confirm that you are now operating as <code>bandit14</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>cat /etc/bandit_pass/bandit14</code></td>
    <td>Reads the password file for <code>bandit14</code>. This works only after you are authenticated as <code>bandit14</code>.<br><br></td>
  </tr>
</table>

## 8. Walkthrough Without Credential Disclosure

This walkthrough assumes you are working from a local terminal, such as Windows Subsystem for Linux, macOS Terminal, or a Linux shell. The examples below use WSL because it gives Windows users a Linux-like command-line environment.

### Step 1

Open WSL and connect to the Bandit server as `bandit13`.

```bash
ssh bandit13@bandit.labs.overthewire.org -p 2220
```

This command has several parts.

<table>
  <tr>
    <th width="35%">Command Part</th>
    <th width="65%">Meaning</th>
  </tr>
  <tr>
    <td><code>ssh</code></td>
    <td>Starts the Secure Shell client, which is used to connect to a remote system securely from the command line.<br><br></td>
  </tr>
  <tr>
    <td><code>bandit13</code></td>
    <td>The username for this level. Each Bandit level has its own user account, such as <code>bandit12</code>, <code>bandit13</code>, and <code>bandit14</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>@</code></td>
    <td>Separates the username from the remote host address.<br><br></td>
  </tr>
  <tr>
    <td><code>bandit.labs.overthewire.org</code></td>
    <td>The hostname of the OverTheWire Bandit server.<br><br></td>
  </tr>
  <tr>
    <td><code>-p 2220</code></td>
    <td>Tells SSH to connect on port <code>2220</code> instead of the default SSH port, which is <code>22</code>.<br><br></td>
  </tr>
</table>

When prompted for the password, enter the password you obtained from the previous level. The terminal may not show any characters while you type the password. That is normal behavior for password prompts.

After you log in successfully, your commands are running inside a remote Linux shell on the Bandit server, not merely inside your local WSL environment.

### Step 2

Confirm your current working directory.

```bash
pwd
```

You should see that you are in the Bandit user’s home directory.

### Step 3

List the files in the home directory.

```bash
ls
```

You should see files similar to:

```text
HINT  sshkey.private
```

The private key is the credential material you will use to authenticate as `bandit14`.

The `HINT` file explains an important environment-specific detail.

### Step 4

Read the level hint.

```bash
cat HINT
```

The hint explains that the current OverTheWire environment prevents logging in from one level to another through `localhost`.

This matters because older writeups may show a command like:

```bash
ssh -i sshkey.private bandit14@localhost -p 2220
```

That approach may now fail. The current workflow is to log out, download the key to your local WSL environment, and then connect to the Bandit server as `bandit14` using the downloaded key.

### Step 5

Log out of the Bandit server.

```bash
exit
```

This returns you to your local WSL terminal.

This distinction matters. The next few commands should be run locally from WSL, not from inside the `bandit13` remote shell.

### Step 6

Download the private key to your local WSL environment.

```bash
scp -P 2220 bandit13@bandit.labs.overthewire.org:/home/bandit13/sshkey.private ./bandit14.private
```

This command copies the remote file `sshkey.private` from the `bandit13` account to your current local WSL directory.

The downloaded local file is named:

```text
bandit14.private
```

This local rename helps you remember what the key is used for.

You will be prompted for the `bandit13` password. Enter the password you used to log in to Level 13.

The remote path syntax matters. The correct format is:

```text
user@host:/remote/path
```

There should be exactly one colon between the host and the remote file path.

Correct:

```bash
scp -P 2220 bandit13@bandit.labs.overthewire.org:/home/bandit13/sshkey.private ./bandit14.private
```

Incorrect:

```bash
scp -P 2220 bandit13@bandit.labs.overthewire.org::sshkey.private ./bandit14.private
```

The incorrect version uses two colons and may cause `scp` to search for a path such as `:sshkey.private`, which does not exist.

### Step 7

Confirm the key downloaded.

```bash
ls -l bandit14.private
```

You should see the local private key file.

Do not open it, screenshot its contents, or commit it to GitHub.

### Step 8

Restrict the private key permissions.

```bash
chmod 600 bandit14.private
```

This makes the key readable and writable only by your local user.

SSH may refuse to use private keys that are accessible by other users. More importantly, private keys should be protected because they are credential material.

### Step 9

Use the private key to log in as `bandit14`.

```bash
ssh -i bandit14.private bandit14@bandit.labs.overthewire.org -p 2220
```

This command tells SSH to use `bandit14.private` as the identity file.

The target is:

```text
bandit14@bandit.labs.overthewire.org
```

That means you are connecting to the Bandit server as the `bandit14` user.

If SSH asks whether you want to continue connecting because the host authenticity cannot be established, type:

```text
yes
```

This is common the first time an SSH client connects to a host from a particular local environment.

### Step 10

Confirm that you are now operating as `bandit14`.

```bash
whoami
```

You should see:

```text
bandit14
```

This matters because the password file for `bandit14` is readable only from the correct user context.

### Step 11

Read the password file for `bandit14`.

```bash
cat /etc/bandit_pass/bandit14
```

The output is the password for Bandit Level 14. Do not commit that password to GitHub.

### Step 12

Return to your local WSL shell when finished.

```bash
exit
```

This exits the `bandit14` SSH session and returns you to your local WSL shell.

## 9. Command Output and Screenshots

Use this section to include terminal output or screenshots after redacting credentials and private key material.

### Relevant Command Output

```text
$ ssh bandit13@bandit.labs.overthewire.org -p 2220
bandit13@bandit.labs.overthewire.org's password:
[successful login output omitted]

$ pwd
/home/bandit13

$ ls
HINT  sshkey.private

$ cat HINT
If you have trouble with this level, note the following:

1) As for all other levels, this level has a website with information:
   https://overthewire.org/wargames/bandit/bandit14.html
2) No, the level is not broken. To verify, see:
   https://status.overthewire.org/
3) The current version of OverTheWire prevents logging in from one
   level to another via localhost. Log out, and see 1)
4) If you get errors, read the error message on your screen.
   We mean it!

$ exit
logout
Connection to bandit.labs.overthewire.org closed.

$ scp -P 2220 bandit13@bandit.labs.overthewire.org:/home/bandit13/sshkey.private ./bandit14.private
bandit13@bandit.labs.overthewire.org's password:
sshkey.private                                      100% 1679     [transfer details omitted]

$ ls -l bandit14.private
-r-------- 1 student student 1679 [date omitted] bandit14.private

$ chmod 600 bandit14.private

$ ssh -i bandit14.private bandit14@bandit.labs.overthewire.org -p 2220
[successful login output omitted]

$ whoami
bandit14

$ cat /etc/bandit_pass/bandit14
[REDACTED PASSWORD]
```

This output shows the central lesson. Instead of using `localhost` from inside the Bandit server, you follow the current OverTheWire guidance: read the hint, log out, download the private key to your local WSL environment, protect the key, authenticate as `bandit14`, and then read the password file from the correct user context.

### Screenshots

<img width="775" height="323" alt="image" src="https://github.com/user-attachments/assets/70fcfbe6-b3fb-4b49-adbc-fb636e6eb1c3" />

<img width="775" height="323" alt="image" src="https://github.com/user-attachments/assets/3acd0acd-8afa-4f15-af8d-610a1a9c0db1" />

<img width="775" height="221" alt="image" src="https://github.com/user-attachments/assets/92c7e21d-ecc6-4f43-8977-dd2f1299eff2" />

<img width="775" height="323" alt="image" src="https://github.com/user-attachments/assets/a4abd22a-a2cc-459f-b25d-12a07b2ce1cf" />

<img width="775" height="323" alt="image" src="https://github.com/user-attachments/assets/67446896-ab35-48f2-9480-dbaca3db6ad5" />


## 10. What Is Really Happening

In this level, you are learning the difference between password-based authentication and key-based authentication.

In earlier levels, you used a password to log in as the next Bandit user. In this level, you are given a private SSH key. The private key allows SSH to prove your identity to the server without typing the next user’s password.

The workflow has four major parts.

First, you inspect the remote `bandit13` home directory and find the key:

```text
sshkey.private
```

Second, you read the `HINT` file. The hint explains that localhost login from one level to another is blocked in the current OverTheWire environment.

Third, you copy the key to your local WSL environment with `scp`:

```bash
scp -P 2220 bandit13@bandit.labs.overthewire.org:/home/bandit13/sshkey.private ./bandit14.private
```

Fourth, you use that downloaded key to authenticate as `bandit14`:

```bash
ssh -i bandit14.private bandit14@bandit.labs.overthewire.org -p 2220
```

The `-i bandit14.private` portion tells SSH which private key to use. The `bandit14@bandit.labs.overthewire.org` portion tells SSH to log in as `bandit14` on the Bandit server. The `-p 2220` portion tells SSH to use the Bandit SSH port.

The `scp` command has its own syntax detail. The remote file is written as:

```text
user@host:/remote/path
```

There is one colon between the hostname and the remote path. If you accidentally type two colons, `scp` may interpret the path incorrectly and fail with a message such as:

```text
scp: :sshkey.private: No such file or directory
```

Once you are logged in as `bandit14`, your permissions change. You can now read:

```text
/etc/bandit_pass/bandit14
```

This level teaches an important access control principle: what you can read depends on who you are authenticated as. The same server and same file path may behave differently under a different user account.

## 11. Common Mistakes

<table>
  <tr>
    <th width="35%">Mistake</th>
    <th width="65%">Correction</th>
  </tr>
  <tr>
    <td>Ignoring the <code>HINT</code> file.</td>
    <td>The hint explains that localhost login between levels is blocked in the current OverTheWire environment. Reading the hint saves time and prevents confusion.<br><br></td>
  </tr>
  <tr>
    <td>Trying to read <code>/etc/bandit_pass/bandit14</code> as <code>bandit13</code>.</td>
    <td>The file is readable only by <code>bandit14</code>. Use the private key to authenticate as <code>bandit14</code> first.<br><br></td>
  </tr>
  <tr>
    <td>Trying to SSH from <code>bandit13</code> to <code>bandit14</code> using <code>localhost</code>.</td>
    <td>The OverTheWire server prevents localhost SSH connections from one level to another. Download the private key to your local WSL environment with <code>scp</code>, protect it with <code>chmod 600</code>, and then SSH from WSL to <code>bandit14</code> using the key.<br><br></td>
  </tr>
  <tr>
    <td>Running <code>scp</code> while still inside the remote Bandit shell.</td>
    <td>For this workflow, log out first and run <code>scp</code> from your local WSL terminal. That downloads the key to your local machine.<br><br></td>
  </tr>
  <tr>
    <td>Using lowercase <code>-p</code> with <code>scp</code>.</td>
    <td>For <code>scp</code>, the port option is uppercase <code>-P</code>. For <code>ssh</code>, the port option is lowercase <code>-p</code>.<br><br></td>
  </tr>
  <tr>
    <td>Typing two colons in the <code>scp</code> remote path.</td>
    <td>Use one colon between the hostname and remote file path. For example, use <code>bandit13@bandit.labs.overthewire.org:/home/bandit13/sshkey.private</code>, not <code>bandit13@bandit.labs.overthewire.org::sshkey.private</code>.<br><br></td>
  </tr>
  <tr>
    <td>Forgetting the <code>-i</code> option.</td>
    <td>The <code>-i</code> option tells SSH which private key to use. Without it, SSH may try password authentication or another default key.<br><br></td>
  </tr>
  <tr>
    <td>Forgetting to restrict the private key permissions.</td>
    <td>Use <code>chmod 600 bandit14.private</code>. SSH may reject private keys with overly open permissions, and private keys should be protected regardless.<br><br></td>
  </tr>
  <tr>
    <td>Publishing the private key.</td>
    <td>Private keys are credentials. Do not commit <code>sshkey.private</code> or <code>bandit14.private</code>, paste key contents into a public guide, or expose key material in screenshots.<br><br></td>
  </tr>
  <tr>
    <td>Publishing the password in screenshots or notes.</td>
    <td>Credentials should be redacted from public writeups. The guide should teach the method without exposing active credential material.<br><br></td>
  </tr>
  <tr>
    <td>Confusing local and remote shells.</td>
    <td>Use the prompt and <code>whoami</code> to keep track of where you are. Some commands run on the remote Bandit server, while <code>scp</code>, <code>chmod</code>, and the final key-based SSH command are run from your local WSL shell.<br><br></td>
  </tr>
</table>

## 12. Defensive or Administrative Takeaway

This level shows why SSH private keys must be protected.

A private key is not just a file. It is an authentication credential. If an attacker obtains a private key and the corresponding account accepts that key, the attacker may be able to log in without knowing the account password.

In real environments, private keys should be protected with appropriate file permissions, passphrases where appropriate, secure storage, rotation processes, and access reviews. Unused or exposed keys should be removed from authorized access.

This level also reinforces the importance of user context. Security work often depends on knowing which account you are using, what that account can access, and whether a command is being run locally, remotely, or inside a nested session.

## 13. Real-World Connection

SSH keys are widely used in system administration, cloud infrastructure, DevOps, Git platforms, automation, and incident response. They are convenient and powerful, but they must be managed carefully.

Exposed private keys are a common security risk. They may appear in public repositories, old backups, shared folders, screenshots, developer workstations, build systems, or misconfigured servers. Attackers often search for private keys because they can provide direct access to systems.

The level also reinforces the value of reading official hints and error messages. In real technical work, environments change. Documentation, error output, and system-provided hints often explain why an older method no longer works.

The lesson is simple but important: treat private keys like passwords, and pay attention when the system tells you why something failed.

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
    <td>What does the <code>HINT</code> file explain?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What does the <code>-i</code> option do in SSH?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>Why does this guide download the private key to local WSL instead of using <code>localhost</code> from the Bandit server?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What is the difference between <code>scp -P</code> and <code>ssh -p</code>?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>Why does the <code>scp</code> remote path use one colon between the hostname and file path?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>Why can <code>bandit14</code> read <code>/etc/bandit_pass/bandit14</code> but <code>bandit13</code> cannot?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>Why should private keys be treated like passwords?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>How can you confirm which user you are currently operating as?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>How does this level connect to cloud security, DevOps, or system administration?</td>
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
    <td>OverTheWire Bandit Level 13 to Level 14</td>
    <td>Provides the official level goal and command suggestions for this exercise.</td>
  </tr>
  <tr>
    <td>OverTheWire Status Page</td>
    <td>Useful for verifying whether the game environment is operational when a level behaves unexpectedly.</td>
  </tr>
  <tr>
    <td><code>man ssh</code></td>
    <td>Explains SSH syntax, key-based authentication, identity files, hostnames, and the use of a non-default port with <code>-p</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>man scp</code></td>
    <td>Explains secure file copy syntax, including remote file paths and the uppercase <code>-P</code> port option.<br><br></td>
  </tr>
  <tr>
    <td><code>man ssh_config</code></td>
    <td>Provides background on SSH client configuration, identity files, and authentication behavior.<br><br></td>
  </tr>
  <tr>
    <td><code>man chmod</code></td>
    <td>Provides background on file permissions, which are important when protecting private keys.<br><br></td>
  </tr>
  <tr>
    <td><code>man whoami</code></td>
    <td>Explains how to confirm the current user context.<br><br></td>
  </tr>
</table>
