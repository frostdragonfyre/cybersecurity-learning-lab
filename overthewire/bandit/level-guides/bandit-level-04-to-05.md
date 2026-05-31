# Bandit Level 4 to Level 5

In this level, you will learn how to identify the correct file when several files have similar names and most of them are not human-readable.

The password for the next level is stored in the only human-readable file inside the `inhere` directory. Your job is to inspect the files safely, determine which one contains readable text, and then read that file.

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
    <td>Bandit Level 4 to Level 5<br><br></td>
  </tr>
  <tr>
    <td>Category</td>
    <td>Linux fundamentals, SSH, file type inspection, option-like filenames, human-readable files, command-line investigation<br><br></td>
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

By the end of this level, you should understand how to inspect file types before reading files blindly. You should also understand why filenames beginning with `-` need to be handled carefully.

<table>
  <tr>
    <th width="30%">Learning Layer</th>
    <th width="70%">Objective</th>
  </tr>
  <tr>
    <td>Beginner</td>
    <td>You will learn how to connect to the Bandit server from WSL, move into a directory, list files, identify a human-readable file, and read it safely.<br><br></td>
  </tr>
  <tr>
    <td>Practitioner</td>
    <td>You will practice using file inspection instead of guessing, and you will learn why explicit paths are useful when filenames begin with dash characters.<br><br></td>
  </tr>
  <tr>
    <td>Advanced</td>
    <td>You will connect this beginner exercise to a broader security principle: analysts should identify file type and content characteristics before assuming a file is safe, relevant, or readable.<br><br></td>
  </tr>
</table>

## 3. Level Summary

The official level goal says the password for the next level is stored in the only human-readable file inside the `inhere` directory.

When you enter the directory, you will see several files with similar names:

```text
-file00
-file01
-file02
-file03
-file04
-file05
-file06
-file07
-file08
-file09
```

There are two important details.

First, you do not know which file contains the password. Instead of opening every file randomly, you should inspect the file types.

Second, the filenames begin with `-`. Many Unix-style commands interpret values that begin with `-` as options. To avoid that problem, refer to the files with an explicit relative path, such as:

```bash
file ./-file00
```

or inspect all of them with:

```bash
file ./-file*
```

Official level reference:

```text
https://overthewire.org/wargames/bandit/bandit5.html
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
    <td>Option-like filenames</td>
    <td>A filename beginning with <code>-</code> can be mistaken for a command option. Using <code>./</code> before the filename makes the argument look like a file path instead of an option.<br><br></td>
  </tr>
  <tr>
    <td>File type inspection</td>
    <td>The <code>file</code> command examines a file and reports what kind of content it appears to contain. This helps you avoid guessing which file is readable.<br><br></td>
  </tr>
  <tr>
    <td>Human-readable text</td>
    <td>A human-readable file contains text that can be meaningfully displayed in the terminal. In this level, the password is stored in the file identified as readable text.<br><br></td>
  </tr>
  <tr>
    <td>Globbing</td>
    <td>The shell can expand patterns such as <code>./-file*</code> into matching filenames. This allows you to inspect several similarly named files with one command.<br><br></td>
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
    <td>The files have similar names.</td>
    <td>You need a method for identifying the right file. Guessing is inefficient and teaches the wrong habit.<br><br></td>
  </tr>
  <tr>
    <td>The filenames begin with <code>-</code>.</td>
    <td>Commands may interpret these names as options unless you use an explicit path such as <code>./-file00</code>.<br><br></td>
  </tr>
  <tr>
    <td>The password is in the only human-readable file.</td>
    <td>This tells you to inspect file types before reading file contents.<br><br></td>
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
    <td>The file names begin with <code>-</code>, so think about how to refer to them as paths instead of options.<br><br></td>
  </tr>
  <tr>
    <td>Hint 4</td>
    <td>Use a command that identifies file types. Look for the file that is human-readable text.<br><br></td>
  </tr>
</table>

## 7. Commands Introduced

These commands are not just things to memorize. Each one teaches you something about remote login, directory navigation, file type inspection, option-like filenames, or file handling.

<table>
  <tr>
    <th width="30%">Command or Tool</th>
    <th width="70%">Explanation</th>
  </tr>
  <tr>
    <td><code>ssh bandit4@bandit.labs.overthewire.org -p 2220</code></td>
    <td>Connects from your local terminal to the remote OverTheWire Bandit server as user <code>bandit4</code> on port <code>2220</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>pwd</code></td>
    <td>Prints your current working directory. This helps you verify where you are after logging in.<br><br></td>
  </tr>
  <tr>
    <td><code>ls</code></td>
    <td>Lists visible files and directories in the current directory. In this level, it shows the <code>inhere</code> directory and then the candidate files inside it.<br><br></td>
  </tr>
  <tr>
    <td><code>cd inhere</code></td>
    <td>Changes your current working directory to the <code>inhere</code> directory.<br><br></td>
  </tr>
  <tr>
    <td><code>file ./-file*</code></td>
    <td>Inspects all matching files whose names begin with <code>-file</code>. The <code>./</code> prefix prevents the filenames from being interpreted as command options.<br><br></td>
  </tr>
  <tr>
    <td><code>cat ./-file07</code></td>
    <td>Reads a selected file by using an explicit relative path. Replace <code>-file07</code> with whichever file is identified as human-readable in your output.<br><br></td>
  </tr>
  <tr>
    <td><code>ssh bandit5@bandit.labs.overthewire.org -p 2220</code></td>
    <td>Connects to the next Bandit account after you retrieve the password from the human-readable file.<br><br></td>
  </tr>
</table>

## 8. Walkthrough Without Credential Disclosure

This walkthrough assumes you are working from a local terminal, such as Windows Subsystem for Linux, macOS Terminal, or a Linux shell. The examples below use WSL because it gives Windows users a Linux-like command-line environment.

### Step 1

Open WSL and connect to the Bandit server as `bandit4`.

```bash
ssh bandit4@bandit.labs.overthewire.org -p 2220
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
    <td><code>bandit4</code></td>
    <td>The username for this level. Each Bandit level has its own user account, such as <code>bandit3</code>, <code>bandit4</code>, and <code>bandit5</code>.<br><br></td>
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

List the candidate files.

```bash
ls
```

You should see files similar to:

```text
-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09
```

At this point, you know there are several possible files. The level goal says the password is in the only human-readable file, so the next step is to inspect file types.

### Step 6

Use `file` to identify the human-readable file.

```bash
file ./-file*
```

The `./` prefix matters. It makes each filename look like a path in the current directory instead of an option. The `*` expands to all matching files.

You should see one file identified as text or readable content, while the others are likely data files.

### Step 7

Read the human-readable file.

```bash
cat ./-file07
```

Replace `./-file07` with the file that your `file` output identifies as readable text.

The output is the password for the next Bandit level. Do not commit that password to GitHub.

### Step 8

Use the discovered password to log in to the next level.

```bash
ssh bandit5@bandit.labs.overthewire.org -p 2220
```

When prompted, enter the password you found in the readable file. Again, the terminal may not show characters while the password is typed. That is normal behavior.

At this point, you have moved from `bandit4` to `bandit5`.

## 9. Command Output and Screenshots

Use this section to include terminal output or screenshots after redacting credentials.

### Relevant Command Output

```text
$ ssh bandit4@bandit.labs.overthewire.org -p 2220
bandit4@bandit.labs.overthewire.org's password:
[successful login output omitted]

$ pwd
/home/bandit4

$ ls
inhere

$ cd inhere

$ ls
-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09

$ file ./-file*
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data

$ cat ./-file07
[REDACTED PASSWORD]
```

This output shows the central lesson. Instead of guessing, you use `file` to identify which file is human-readable, then you read that file with `cat`.

### Screenshot

<img width="669" height="310" alt="image" src="https://github.com/user-attachments/assets/2c5ae143-b3c3-4d1d-9151-b916b4927865" />

<img width="669" height="407" alt="image" src="https://github.com/user-attachments/assets/12bb4aea-c5d6-4dfd-b1d1-dd6c2d1d62a0" />


## 10. What Is Really Happening

In this level, you are learning how to inspect file content types before opening files blindly.

A normal `ls` shows filenames, but it does not tell you what kind of content each file contains. The level gives you a clue: the password is in the only human-readable file. That means your task is not merely to list files. Your task is to classify them.

The `file` command examines file contents and reports what kind of data it appears to be. This is useful because file extensions and names are not reliable indicators of content. A file can have no extension, a misleading name, or binary content that will not display cleanly in the terminal.

The filenames also begin with `-`, which creates another command-line issue. If you run a command such as:

```bash
cat -file07
```

the command may interpret `-file07` as an option. By using:

```bash
cat ./-file07
```

you make the argument an explicit path. The command then treats it as a file in the current directory.

This level combines two important habits: identify file type before reading, and handle unusual filenames safely.

## 11. Common Mistakes

<table>
  <tr>
    <th width="35%">Mistake</th>
    <th width="65%">Correction</th>
  </tr>
  <tr>
    <td>Trying to <code>cat</code> every file randomly.</td>
    <td>You can, but it is not the best method. Use <code>file</code> to identify the human-readable file first.<br><br></td>
  </tr>
  <tr>
    <td>Running <code>cat -file07</code> without <code>./</code>.</td>
    <td>A filename that begins with <code>-</code> may be interpreted as an option. Use <code>./-file07</code> to make it an explicit path.<br><br></td>
  </tr>
  <tr>
    <td>Assuming filenames reveal file content.</td>
    <td>Filenames are not reliable evidence of content type. Use tools such as <code>file</code> to inspect content characteristics.<br><br></td>
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

This level shows why file identification matters in security work.

During incident response, malware analysis, forensic triage, or system administration, you should not rely only on filenames. A file named like a text file may contain binary data, and a file without an obvious extension may still contain readable text. File names are metadata. They are useful, but they are not proof of content.

The level also reinforces safe handling of unusual filenames. In real scripts and investigations, files may begin with dashes, contain spaces, or include other characters that affect command-line parsing. Good analysts and administrators handle those cases deliberately.

## 13. Real-World Connection

This concept appears in real systems whenever analysts inspect unknown files. Malware samples, logs, uploaded files, archives, configuration files, and recovered artifacts may not have useful extensions or trustworthy names.

The `file` command is often one of the first tools used during triage because it helps identify whether a file appears to be text, executable, compressed data, image data, or something else. That classification helps determine the next safe step.

The lesson also applies to automation. Scripts that process files should handle unusual filenames correctly and should not assume that names accurately describe content.

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
    <td>Why is <code>file</code> useful before reading unknown files?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>Why do the filenames need to be referenced with <code>./</code>?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>Why are filenames not reliable proof of file content?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>How can you tell whether you are working in your local WSL shell or the remote Bandit shell?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>How does this level connect to incident response or forensic triage?</td>
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
    <td>OverTheWire Bandit Level 4 to Level 5</td>
    <td>Provides the official level goal and command suggestions for this exercise.</td>
  </tr>
  <tr>
    <td><code>man ssh</code></td>
    <td>Explains SSH syntax, remote login behavior, authentication, and the use of a non-default port with <code>-p</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>man file</code></td>
    <td>Explains how the <code>file</code> command determines file type based on file contents.<br><br></td>
  </tr>
  <tr>
    <td><code>man ls</code></td>
    <td>Explains how to list directory contents and interpret file listings.<br><br></td>
  </tr>
  <tr>
    <td><code>man cat</code></td>
    <td>Explains how <code>cat</code> reads files and writes content to standard output.<br><br></td>
  </tr>
</table>
