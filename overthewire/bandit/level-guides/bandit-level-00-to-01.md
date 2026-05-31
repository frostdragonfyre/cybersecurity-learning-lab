# Bandit Level 0 to Level 1

In this level, you will learn how to connect to a remote Linux system with SSH, orient yourself inside a shell, list files in a directory, and read the contents of a simple text file.

The password for the next level is stored in a file called `readme` in the home directory. Your job is to find that file, read it, and use the password to move from `bandit0` to `bandit1`.

This guide does not publish active passwords. The goal is to help you understand the method, the commands, and the real-world lesson behind the exercise.

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
    <td>Bandit Level 0 to Level 1<br><br></td>
  </tr>
  <tr>
    <td>Category</td>
    <td>Linux fundamentals, SSH, file inspection, command-line navigation<br><br></td>
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
    <td>This guide explains how to find the password but does not include the password value.<br><br></td>
  </tr>
</table>

## 2. Learning Objective

By the end of this level, you should understand how to connect to a remote Linux system, verify where you are in the filesystem, list files, and read a file from the command line.

<table>
  <tr>
    <th width="30%">Learning Layer</th>
    <th width="70%">Objective</th>
  </tr>
  <tr>
    <td>Beginner</td>
    <td>You will learn how to use SSH from WSL to connect to a remote system and run basic Linux commands inside that remote shell.<br><br></td>
  </tr>
  <tr>
    <td>Practitioner</td>
    <td>You will practice verifying your current location, inspecting directory contents, reading a file, and using the result to authenticate to the next level.<br><br></td>
  </tr>
  <tr>
    <td>Advanced</td>
    <td>You will connect a simple exercise to deeper systems concepts: user accounts, home directories, remote shells, standard output, file access, and credential handling.<br><br></td>
  </tr>
</table>

## 3. Level Summary

The official level goal says the password for the next level is stored in a file called `readme` located in the home directory.

That means you do not need to search the entire system. Start by connecting to the Bandit server, confirm where you are, list the files in the current directory, and read the file named `readme`.

You will use these basic commands:

```bash
pwd
ls
cat readme
```

You will also use SSH to connect to the Bandit server:

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

Official level reference:

```text
https://overthewire.org/wargames/bandit/bandit1.html
```

## 4. Concepts Introduced

<table>
  <tr>
    <th width="30%">Concept</th>
    <th width="70%">Explanation</th>
  </tr>
  <tr>
    <td>SSH</td>
    <td>SSH, or Secure Shell, is how you connect securely to a remote system from your terminal. In Bandit, you use SSH to log in as a specific Bandit user for each level.<br><br></td>
  </tr>
  <tr>
    <td>WSL terminal context</td>
    <td>When you run <code>ssh</code> from WSL, the command starts on your local Windows machine inside a Linux-like terminal. After you successfully log in, your commands run on the remote OverTheWire server. This distinction matters because you should always know whether you are working locally or remotely.<br><br></td>
  </tr>
  <tr>
    <td>Home directory</td>
    <td>A home directory is the default working area for a user account on a Unix-like system. When you log in as a user, the shell commonly starts in that user’s home directory.<br><br></td>
  </tr>
  <tr>
    <td>Directory listing</td>
    <td>A directory listing shows the files and folders present in the current location. This is often the first step in command-line investigation because it tells you what objects are available to inspect.<br><br></td>
  </tr>
  <tr>
    <td>Reading file contents</td>
    <td>A text file can be displayed in the terminal using commands that send its contents to standard output. For this level, the relevant skill is reading a simple file without modifying it.<br><br></td>
  </tr>
  <tr>
    <td>Credential handling</td>
    <td>The password discovered in this level is a credential for the next account. It should be recorded privately and should not be committed to a public repository.<br><br></td>
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
    <td>The level goal names a specific file.</td>
    <td>This reduces the problem from searching the whole system to checking whether the named file exists in the expected location.<br><br></td>
  </tr>
  <tr>
    <td>The file is located in the home directory.</td>
    <td>After you log in, you are usually already in the Bandit user’s home directory, so the first check should be the current directory contents.<br><br></td>
  </tr>
  <tr>
    <td>The file is a normal text file.</td>
    <td>If the file is readable text, you can inspect it directly with a basic file display command.<br><br></td>
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
    <td>Start by connecting as the correct Bandit user for the level. Then ask yourself, “Where am I in the filesystem?”<br><br></td>
  </tr>
  <tr>
    <td>Hint 2</td>
    <td>Use a command that lists files in the current directory. Look for the file named in the level goal.<br><br></td>
  </tr>
  <tr>
    <td>Hint 3</td>
    <td>Once you find the file, use a command that prints a file’s contents to the terminal.<br><br></td>
  </tr>
</table>

## 7. Commands Introduced

These commands are not just things to memorize. Each one teaches you something about remote login, filesystem orientation, or file handling.

<table>
  <tr>
    <th width="30%">Command or Tool</th>
    <th width="70%">Explanation</th>
  </tr>
  <tr>
    <td><code>ssh bandit0@bandit.labs.overthewire.org -p 2220</code></td>
    <td>Connects from your local terminal to the remote OverTheWire Bandit server as user <code>bandit0</code> on port <code>2220</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>pwd</code></td>
    <td>Prints your current working directory. This helps you verify where you are after logging in.<br><br></td>
  </tr>
  <tr>
    <td><code>ls</code></td>
    <td>Lists files and directories in the current directory. In this level, it confirms that a file named <code>readme</code> exists.<br><br></td>
  </tr>
  <tr>
    <td><code>cat readme</code></td>
    <td>Prints the contents of the file named <code>readme</code> to the terminal. In this level, that file contains the password for the next level.<br><br></td>
  </tr>
  <tr>
    <td><code>ssh bandit1@bandit.labs.overthewire.org -p 2220</code></td>
    <td>Connects to the next Bandit account after you retrieve the password from the <code>readme</code> file.<br><br></td>
  </tr>
</table>

## 8. Walkthrough Without Credential Disclosure

This walkthrough assumes you are working from a local terminal, such as Windows Subsystem for Linux, macOS Terminal, or a Linux shell. The examples below use WSL because it gives Windows users a Linux-like command-line environment.

### Step 1

Open WSL and connect to the Bandit server as `bandit0`.

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
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
    <td><code>bandit0</code></td>
    <td>The username for this level. Each Bandit level has its own user account, such as <code>bandit0</code>, <code>bandit1</code>, and <code>bandit2</code>.<br><br></td>
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

When prompted for the password, enter the starting password provided by OverTheWire for Bandit Level 0. The terminal may not show any characters while you type the password. That is normal behavior for password prompts.

After you log in successfully, your commands are running inside a remote Linux shell on the Bandit server, not merely inside your local WSL environment.

### Step 2

Confirm your current working directory.

```bash
pwd
```

This command prints the directory your shell is currently operating in. This matters because many beginner mistakes come from assuming the current filesystem location without verifying it.

You should see that you are in the Bandit user’s home directory.

### Step 3

List the files in the current directory.

```bash
ls
```

You should see a file named:

```text
readme
```

This confirms that the level goal is pointing to a real file in the current directory.

### Step 4

Read the contents of the file.

```bash
cat readme
```

This command sends the contents of the `readme` file to the terminal.

The output is the password for the next Bandit level. Do not commit that password to GitHub. Save it in a private local note or password manager if you need to track your progress.

### Step 5

Use the discovered password to log in to the next level.

```bash
ssh bandit1@bandit.labs.overthewire.org -p 2220
```

When prompted, enter the password you found in the `readme` file. Again, the terminal may not show characters while the password is typed. That is normal behavior.

At this point, you have moved from `bandit0` to `bandit1`.

## 9. Command Output and Screenshots

Use this section to include terminal output or screenshots after redacting credentials.

### Relevant Command Output

```text
$ ssh bandit0@bandit.labs.overthewire.org -p 2220
bandit0@bandit.labs.overthewire.org's password:
[successful login output omitted]

$ pwd
/home/bandit0

$ ls
readme

$ cat readme
[REDACTED PASSWORD]
```

This output shows the reasoning path without exposing the active credential. It confirms the current directory, the presence of the target file, and the fact that the file contains the next password.

### Screenshots

<img width="867" height="281" alt="image" src="https://github.com/user-attachments/assets/85b19268-2d35-4748-9b27-5f8990e118f6" />

<img width="867" height="281" alt="image" src="https://github.com/user-attachments/assets/127c3bfd-204e-4088-9027-17055dacf965" />


## 10. What Is Really Happening

In this level, you are learning how a remote shell session gives you access to another Linux environment, and how basic filesystem commands help you understand where you are and what files are available.

When you run `ssh` from WSL, you start on your local machine. After authentication succeeds, SSH gives you an interactive shell on the remote OverTheWire server. Commands such as `pwd`, `ls`, and `cat` now run in that remote environment as the Bandit user.

When a user logs in to a Linux system, the shell usually starts in that user’s home directory. A directory is a container that maps names to filesystem objects. The `ls` command asks the operating system to show the names of objects in that directory. The `cat` command opens a file, reads its contents, and writes those contents to standard output, which is displayed in the terminal.

The password is not hidden through exploitation, encryption, or obfuscation. It is simply stored in a readable file. That is why the lesson is foundational: before advanced exploitation matters, you must understand how to inspect the environment carefully.

## 11. Common Mistakes

<table>
  <tr>
    <th width="35%">Mistake</th>
    <th width="65%">Correction</th>
  </tr>
  <tr>
    <td>Assuming the terminal will show password characters while typing.</td>
    <td>SSH password prompts often do not display characters, dots, or asterisks. Type the password carefully and press Enter.<br><br></td>
  </tr>
  <tr>
    <td>Confusing the local WSL shell with the remote Bandit shell.</td>
    <td>Before SSH, commands run on your local WSL environment. After a successful SSH login, commands run on the remote OverTheWire server as the Bandit user.<br><br></td>
  </tr>
  <tr>
    <td>Trying to search the entire system immediately.</td>
    <td>The level goal already says the file is in the home directory. Start with the simplest local observation before using broader search commands.<br><br></td>
  </tr>
  <tr>
    <td>Copying the password into a public repo or screenshot.</td>
    <td>Credentials should be handled as sensitive material. Redact them in screenshots and avoid committing them to public GitHub repositories.<br><br></td>
  </tr>
  <tr>
    <td>Forgetting the custom SSH port.</td>
    <td>Bandit uses port <code>2220</code> for SSH. If you omit the port, the connection may fail or go to the wrong service.<br><br></td>
  </tr>
</table>

## 12. Defensive or Administrative Takeaway

This level demonstrates a basic but important administrative lesson: sensitive information should not be stored in readable plaintext files unless the access model is intentional and controlled.

In real systems, credentials should be protected through appropriate permissions, secret management tools, auditing, rotation, and access controls. Even when a file is easy to read for a lab exercise, the real-world lesson is that defenders must know where secrets are stored and who can access them.

This level also reinforces a core operational habit: verify your environment before acting. A security analyst, administrator, or incident responder needs to know whether commands are running locally, remotely, in a container, in a cloud shell, or on a production host.

## 13. Real-World Connection

The same concepts appear constantly in real Linux administration and incident response. Analysts inspect directories, review files, verify paths, check user context, and look for exposed secrets. Cloud servers, CI/CD runners, developer workstations, and application directories may all contain configuration files, tokens, keys, or credentials if secret management practices are weak.

The beginner command `cat readme` is simple, but the underlying habit is professional: inspect the environment, verify assumptions, read only what is needed, and protect sensitive findings.

The WSL-to-SSH workflow also mirrors real administrative work. Security analysts, system administrators, and engineers often use a local terminal to connect to remote systems, inspect files, review logs, and troubleshoot issues. Knowing which system you are currently operating on is essential.

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
    <td>How can you tell whether you are working in your local WSL shell or the remote Bandit shell?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>Why was listing the directory useful before reading the file?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What does <code>cat</code> do in this context?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>Why should the discovered password not be committed to GitHub?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>How does this level connect to real-world secret management?</td>
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
    <td>OverTheWire Bandit Level 0 to Level 1</td>
    <td>Provides the official level goal and command suggestions for this exercise.</td>
  </tr>
  <tr>
    <td><code>man ssh</code></td>
    <td>Explains SSH syntax, remote login behavior, authentication, and the use of a non-default port with <code>-p</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>man pwd</code></td>
    <td>Explains how to print the current working directory.<br><br></td>
  </tr>
  <tr>
    <td><code>man ls</code></td>
    <td>Explains how to list directory contents and use options such as long format or hidden file display.<br><br></td>
  </tr>
  <tr>
    <td><code>man cat</code></td>
    <td>Explains how <code>cat</code> reads files and writes content to standard output.<br><br></td>
  </tr>
</table>
