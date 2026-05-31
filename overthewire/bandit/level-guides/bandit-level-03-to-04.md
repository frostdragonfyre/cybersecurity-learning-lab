# Bandit Level 3 to Level 4

In this level, you will learn how Linux handles hidden files and why a file may exist even when a normal directory listing appears empty.

The password for the next level is stored in a hidden file inside the `inhere` directory. Your job is to enter that directory, recognize that the default `ls` output is incomplete, list hidden files, and read the correct file.

This guide does not publish active passwords. The goal is to help you understand the method, the command behavior, and the real-world lesson behind the exercise.

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
    <td>Bandit Level 3 to Level 4<br><br></td>
  </tr>
  <tr>
    <td>Category</td>
    <td>Linux fundamentals, SSH, directory navigation, hidden files, file inspection<br><br></td>
  </tr>
  <tr>
    <td>Difficulty</td>
    <td>Beginner<br><br></td>
  </tr>
  <tr>
    <td>Spoiler posture</td>
    <td>Teaching notes with guided walkthrough. The active password is not published.<br><br></td>
  </tr>
  <tr>
    <td>Password policy</td>
    <td>This guide explains how to retrieve the password but does not include the password value.<br><br></td>
  </tr>
</table>

## 2. Learning Objective

By the end of this level, you should understand that Linux hidden files are hidden by naming convention, not by encryption or access control. You should also understand how to use `ls -la` to reveal files that normal `ls` does not display.

<table>
  <tr>
    <th width="30%">Learning Layer</th>
    <th width="70%">Objective</th>
  </tr>
  <tr>
    <td>Beginner</td>
    <td>You will learn how to connect to the Bandit server from WSL, move into a directory, list hidden files, and read a hidden file.<br><br></td>
  </tr>
  <tr>
    <td>Practitioner</td>
    <td>You will practice verifying your location, using directory navigation commands, and choosing the correct listing option when default output does not show what you need.<br><br></td>
  </tr>
  <tr>
    <td>Advanced</td>
    <td>You will connect this beginner exercise to a broader systems principle: visibility is not the same thing as access control. A file can be hidden from default display while still being readable by users with the right permissions.<br><br></td>
  </tr>
</table>

## 3. Level Summary

The official level goal says the password for the next level is stored in a hidden file located inside the `inhere` directory.

At first, the directory may appear empty if you run a normal `ls`. That does not mean there are no files. It means the default listing does not show hidden files.

On Linux, files that begin with a dot are conventionally hidden from normal directory listings. To see them, you can use:

```bash
ls -la
```

Then you can read the hidden file with:

```bash
cat ...Hiding-From-You
```

Official level reference:

```text
https://overthewire.org/wargames/bandit/bandit4.html
```

## 4. Concepts Introduced

<table>
  <tr>
    <th width="30%">Concept</th>
    <th width="70%">Explanation</th>
  </tr>
  <tr>
    <td>SSH</td>
    <td>SSH, or Secure Shell, is how you connect securely to a remote system from your terminal. In Bandit, each level is a different user account, so moving to the next level means logging in as the next Bandit user.<br><br></td>
  </tr>
  <tr>
    <td>WSL terminal context</td>
    <td>When you run <code>ssh</code> from WSL, the command starts on your local Windows machine inside a Linux-like terminal. After you successfully log in, your commands run on the remote OverTheWire server. You should always know whether you are working locally or remotely.<br><br></td>
  </tr>
  <tr>
    <td>Directory navigation</td>
    <td>The <code>cd</code> command changes your current working directory. In this level, you use it to move from the Bandit home directory into the <code>inhere</code> directory.<br><br></td>
  </tr>
  <tr>
    <td>Hidden files</td>
    <td>In Unix-like systems, a hidden file is usually a file whose name begins with a dot. Hidden files are not shown by default with a normal <code>ls</code> command.<br><br></td>
  </tr>
  <tr>
    <td>Long listing</td>
    <td>The <code>-l</code> option for <code>ls</code> shows more detail, including permissions, owner, group, size, and modification time.<br><br></td>
  </tr>
  <tr>
    <td>Show all files</td>
    <td>The <code>-a</code> option for <code>ls</code> shows all directory entries, including hidden files and the special entries <code>.</code> and <code>..</code>.<br><br></td>
  </tr>
  <tr>
    <td>File permissions</td>
    <td>Permissions determine who can read, write, or execute a file. In this level, the hidden file is visible with <code>ls -la</code> and readable by the appropriate Bandit user context.<br><br></td>
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
    <td>The SSH command includes a username, hostname, and port.</td>
    <td>These parts determine which remote account you connect to, which server you contact, and which network service you use.<br><br></td>
  </tr>
  <tr>
    <td>The home directory contains a directory named <code>inhere</code>.</td>
    <td>The level goal tells you the password is inside that directory, so you need to move into it before looking for the file.<br><br></td>
  </tr>
  <tr>
    <td>A normal <code>ls</code> inside <code>inhere</code> shows no visible files.</td>
    <td>This is the central clue. The directory is not necessarily empty; the file may be hidden from default output.<br><br></td>
  </tr>
  <tr>
    <td><code>ls -la</code> reveals a hidden file.</td>
    <td>The <code>-a</code> option shows hidden files, and the <code>-l</code> option gives you useful details about the file.<br><br></td>
  </tr>
  <tr>
    <td>The hidden file begins with dots.</td>
    <td>Files beginning with dots are hidden by convention. They are not automatically protected from users who have permission to read them.<br><br></td>
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
    <td>If you see a directory named <code>inhere</code>, move into it and list its contents.<br><br></td>
  </tr>
  <tr>
    <td>Hint 3</td>
    <td>If a normal listing appears empty, ask whether the file might be hidden from default output.<br><br></td>
  </tr>
  <tr>
    <td>Hint 4</td>
    <td>Use an <code>ls</code> option that shows hidden files.<br><br></td>
  </tr>
</table>

## 7. Commands Introduced

These commands are not just things to memorize. Each one teaches you something about remote login, directory navigation, hidden files, or file inspection.

<table>
  <tr>
    <th width="30%">Command or Tool</th>
    <th width="70%">Explanation</th>
  </tr>
  <tr>
    <td><code>ssh bandit3@bandit.labs.overthewire.org -p 2220</code></td>
    <td>Connects from your local terminal to the remote OverTheWire Bandit server as user <code>bandit3</code> on port <code>2220</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>pwd</code></td>
    <td>Prints your current working directory. This helps you verify where you are after logging in.<br><br></td>
  </tr>
  <tr>
    <td><code>ls</code></td>
    <td>Lists visible files and directories in the current directory. In this level, it shows the <code>inhere</code> directory from the home directory.<br><br></td>
  </tr>
  <tr>
    <td><code>cd inhere</code></td>
    <td>Changes your current working directory to the <code>inhere</code> directory.<br><br></td>
  </tr>
  <tr>
    <td><code>ls -la</code></td>
    <td>Lists all files, including hidden files, in long format. This reveals files that normal <code>ls</code> does not show.<br><br></td>
  </tr>
  <tr>
    <td><code>cat ...Hiding-From-You</code></td>
    <td>Prints the contents of the hidden file to the terminal. In this level, that file contains the password for the next level.<br><br></td>
  </tr>
  <tr>
    <td><code>ssh bandit4@bandit.labs.overthewire.org -p 2220</code></td>
    <td>Connects to the next Bandit account after you retrieve the password from the hidden file.<br><br></td>
  </tr>
</table>

## 8. Walkthrough Without Credential Disclosure

This walkthrough assumes you are working from a local terminal, such as Windows Subsystem for Linux, macOS Terminal, or a Linux shell. The examples below use WSL because it gives Windows users a Linux-like command-line environment.

### Step 1

Open WSL and connect to the Bandit server as `bandit3`.

```bash
ssh bandit3@bandit.labs.overthewire.org -p 2220
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
    <td><code>bandit3</code></td>
    <td>The username for this level. Each Bandit level has its own user account, such as <code>bandit0</code>, <code>bandit1</code>, <code>bandit2</code>, and <code>bandit3</code>.<br><br></td>
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

You should see a directory named:

```text
inhere
```

This tells you where to look next.

### Step 4

Move into the `inhere` directory.

```bash
cd inhere
```

Your prompt may change to show that you are now inside `~/inhere`.

### Step 5

List the visible files.

```bash
ls
```

You may see no output. That does not necessarily mean the directory is empty. It means there are no non-hidden files displayed by normal `ls`.

### Step 6

List all files, including hidden files.

```bash
ls -la
```

You should see output that includes a hidden file named:

```text
...Hiding-From-You
```

The filename starts with dots, so it is hidden from the default `ls` output.

### Step 7

Read the hidden file.

```bash
cat ...Hiding-From-You
```

The output is the password for the next Bandit level. Do not commit that password to GitHub.

### Step 8

Use the discovered password to log in to the next level.

```bash
ssh bandit4@bandit.labs.overthewire.org -p 2220
```

When prompted, enter the password you found in the hidden file. Again, the terminal may not show characters while the password is typed. That is normal behavior.

At this point, you have moved from `bandit3` to `bandit4`.

## 9. Command Output and Screenshots

Use this section to include terminal output or screenshots after redacting credentials.

### Relevant Command Output

```text
$ ssh bandit3@bandit.labs.overthewire.org -p 2220
bandit3@bandit.labs.overthewire.org's password:
[successful login output omitted]

$ pwd
/home/bandit3

$ ls
inhere

$ cd inhere

$ ls

$ ls -la
total 12
drwxr-xr-x 2 root    root    4096 Apr  3 15:17 .
drwxr-xr-x 3 root    root    4096 Apr  3 15:17 ..
-rw-r----- 1 bandit4 bandit3   33 Apr  3 15:17 ...Hiding-From-You

$ cat ...Hiding-From-You
[REDACTED PASSWORD]
```

This output shows the central lesson. A normal `ls` does not show the hidden file, but `ls -la` reveals it.

### Screenshot

<img width="669" height="239" alt="image" src="https://github.com/user-attachments/assets/1633efaf-010b-4712-8760-ed8899b57c5e" />

<img width="669" height="310" alt="image" src="https://github.com/user-attachments/assets/d6400322-08ee-40a0-9c8d-e1c3a5e1f7b9" />


## 10. What Is Really Happening

In this level, you are learning that hidden files in Linux are hidden by convention.

A filename that begins with a dot is not normally displayed by `ls`. This behavior is a user interface convention, not a security boundary. The file still exists in the directory, and if you have permission to read it, you can read it.

When you run:

```bash
ls
```

the command shows visible directory entries.

When you run:

```bash
ls -la
```

you are combining two options. The `-l` option gives a long listing, and the `-a` option shows all entries, including hidden files.

The entries `.` and `..` are also shown. The single dot means the current directory. The double dot means the parent directory.

This level is simple, but it teaches an important habit: when the first command does not show what you expect, do not assume the object is absent. Ask whether your command is only showing part of the available information.

## 11. Common Mistakes

<table>
  <tr>
    <th width="35%">Mistake</th>
    <th width="65%">Correction</th>
  </tr>
  <tr>
    <td>Running <code>ls</code> inside <code>inhere</code> and assuming the directory is empty.</td>
    <td>Normal <code>ls</code> hides files that begin with a dot. Use <code>ls -la</code> to show hidden files.<br><br></td>
  </tr>
  <tr>
    <td>Thinking hidden files are protected files.</td>
    <td>Hidden files are not automatically protected. They are only omitted from default listings. Permissions determine whether you can read them.<br><br></td>
  </tr>
  <tr>
    <td>Using <code>ll</code> without understanding what it means.</td>
    <td><code>ll</code> is often an alias for <code>ls -la</code>, but it is not guaranteed to exist everywhere. Teach and understand <code>ls -la</code> because it is portable.<br><br></td>
  </tr>
  <tr>
    <td>Publishing the password in screenshots or notes.</td>
    <td>Credentials should be redacted from public writeups. The guide should teach the method without exposing active credential material.<br><br></td>
  </tr>
  <tr>
    <td>Confusing the local WSL shell with the remote Bandit shell.</td>
    <td>Before SSH, commands run on your local WSL environment. After a successful SSH login, commands run on the remote OverTheWire server as the Bandit user.<br><br></td>
  </tr>
</table>

## 12. Defensive or Administrative Takeaway

This level shows why visibility and access control are different concepts.

A hidden file is not necessarily secure. It is simply omitted from normal listings. In real systems, sensitive files should not rely on hidden naming conventions for protection. They should be protected with appropriate permissions, ownership, encryption where needed, secret management, and monitoring.

For administrators and defenders, this level also reinforces the habit of using the right level of inspection. During troubleshooting or incident response, default views may hide important evidence. Analysts often need to use options that reveal hidden files, metadata, ownership, and permissions.

## 13. Real-World Connection

Hidden files are common in Linux and Unix-like systems. Configuration files such as `.bashrc`, `.profile`, `.ssh`, `.gitconfig`, and many application settings are hidden by convention.

In security work, hidden files may contain configuration, credentials, shell history, SSH keys, persistence mechanisms, malware artifacts, or evidence of user activity. An analyst who only uses default directory listings may miss important information.

The beginner command `ls -la` is simple, but the underlying habit is professional: when investigating a system, make sure your tools are showing you the information you actually need.

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
    <td>Why did normal <code>ls</code> appear to show an empty directory?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What does the <code>-a</code> option do in <code>ls -la</code>?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What do <code>.</code> and <code>..</code> mean in a directory listing?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>Why are hidden files not the same thing as protected files?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>How does this level connect to incident response or system administration?</td>
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
    <td>OverTheWire Bandit Level 3 to Level 4</td>
    <td>Provides the official level goal and command suggestions for this exercise.</td>
  </tr>
  <tr>
    <td><code>man ssh</code></td>
    <td>Explains SSH syntax, remote login behavior, authentication, and the use of a non-default port with <code>-p</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>man ls</code></td>
    <td>Explains how to list directory contents and use options such as <code>-a</code> and <code>-l</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>man cd</code></td>
    <td><code>cd</code> is commonly documented as a shell built-in. Use shell documentation, such as <code>help cd</code> in Bash, to understand directory navigation.<br><br></td>
  </tr>
  <tr>
    <td><code>man cat</code></td>
    <td>Explains how <code>cat</code> reads files and writes content to standard output.<br><br></td>
  </tr>
</table>
