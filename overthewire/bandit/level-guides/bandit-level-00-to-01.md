# Bandit Level 0 to Level 1

This guide explains Bandit Level 0 to Level 1 as a teaching exercise. It focuses on command-line fundamentals, remote Linux navigation, file inspection, and safe credential handling. The goal is to understand what is happening rather than simply copy a password.

Active passwords are intentionally not published in this guide.

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

<table>
  <tr>
    <th width="30%">Learning Layer</th>
    <th width="70%">Objective</th>
  </tr>
  <tr>
    <td>Beginner</td>
    <td>Learn how to inspect the contents of a home directory and read a simple text file from the Linux command line.<br><br></td>
  </tr>
  <tr>
    <td>Practitioner</td>
    <td>Practice using basic shell commands to verify assumptions, identify relevant files, and extract needed information without guessing.<br><br></td>
  </tr>
  <tr>
    <td>Advanced</td>
    <td>Understand how simple command-line operations reflect deeper operating system concepts, including directories, files, standard output, user context, and credential handling.<br><br></td>
  </tr>
</table>

## 3. Level Summary

The official level goal states that the password for the next level is stored in a file called `readme` located in the home directory. The learner must inspect the home directory, locate the file, read its contents, and then use that password to authenticate as the next Bandit user over SSH.

The important lesson is not that the file is named `readme`. The important lesson is learning how to orient yourself inside a remote Linux shell, inspect the current directory, and read file contents safely.

## 4. Concepts Introduced

<table>
  <tr>
    <th width="30%">Concept</th>
    <th width="70%">Explanation</th>
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

## 5. What the Learner Should Notice

<table>
  <tr>
    <th width="35%">Observation</th>
    <th width="65%">Why It Matters</th>
  </tr>
  <tr>
    <td>The level goal names a specific file.</td>
    <td>This reduces the problem from searching the whole system to checking whether the named file exists in the expected location.<br><br></td>
  </tr>
  <tr>
    <td>The file is located in the home directory.</td>
    <td>After logging in, the learner is usually already in the home directory, so the first check should be the current directory contents.<br><br></td>
  </tr>
  <tr>
    <td>The file is a normal text file.</td>
    <td>If the file is readable text, the learner can inspect it directly with a basic file display command.<br><br></td>
  </tr>
</table>

## 6. Guided Hints

<table>
  <tr>
    <th width="20%">Hint Level</th>
    <th width="80%">Hint</th>
  </tr>
  <tr>
    <td>Hint 1</td>
    <td>Start by asking, “Where am I in the filesystem, and what files are here?”<br><br></td>
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

<table>
  <tr>
    <th width="30%">Command or Tool</th>
    <th width="70%">Explanation</th>
  </tr>
  <tr>
    <td><code>pwd</code></td>
    <td>Prints the current working directory. This helps the learner confirm where they are in the filesystem before making assumptions.<br><br></td>
  </tr>
  <tr>
    <td><code>ls</code></td>
    <td>Lists files and directories in the current directory. This is used to confirm that the expected file is present.<br><br></td>
  </tr>
  <tr>
    <td><code>cat readme</code></td>
    <td>Prints the contents of the file named <code>readme</code> to the terminal. In this level, that file contains the password for the next level.<br><br></td>
  </tr>
  <tr>
    <td><code>ssh</code></td>
    <td>Connects to a remote system over Secure Shell. After finding the next password, the learner uses SSH to log in as the next Bandit user.<br><br></td>
  </tr>
</table>

## 8. Walkthrough Without Credential Disclosure

### Step 1

Confirm the current working directory.

```bash
pwd
```

This command prints the directory the shell is currently operating in. In a beginner-level exercise, this matters because many mistakes come from assuming you are in one location when you are actually somewhere else.

The learner should observe that they are in the Bandit user’s home directory.

### Step 2

List the files in the current directory.

```bash
ls
```

This command shows the visible files and directories in the current location.

The learner should see a file named `readme`. That confirms the level goal is pointing to a real file in the current directory.

### Step 3

Read the contents of the file.

```bash
cat readme
```

This command sends the contents of the `readme` file to the terminal.

The output is the password for the next Bandit level. Do not commit that password to GitHub. Save it in a private local note or password manager if you need to track your progress.

### Step 4

Use the discovered password to log in to the next level.

```bash
ssh bandit1@bandit.labs.overthewire.org -p 2220
```

The `-p 2220` option tells SSH to connect on port `2220`, which is the port specified by the Bandit instructions. The username changes to `bandit1` because the learner is moving from Level 0 to Level 1.

When prompted for the password, enter the password discovered from the `readme` file. The terminal may not show characters while you type the password. That is normal behavior.

## 9. Command Output and Screenshots

Use this section to include terminal output or screenshots after redacting credentials.

### Relevant Command Output

```text
$ pwd
/home/bandit0

$ ls
readme

$ cat readme
[REDACTED PASSWORD]
```

This output shows the reasoning path without exposing the active credential. It confirms the current directory, the presence of the target file, and the fact that the file contains the next password.

### Screenshot

<img width="867" height="281" alt="image" src="https://github.com/user-attachments/assets/d06cb637-c9db-4963-bf81-266d73dbec88" />



## 10. What Is Really Happening

This level introduces the relationship between a user account, a home directory, files, and terminal output.

When a user logs in to a Linux system, the shell usually starts in that user’s home directory. A directory is a container that maps names to filesystem objects. The `ls` command asks the operating system to show the names of objects in that directory. The `cat` command opens a file, reads its contents, and writes those contents to standard output, which is displayed in the terminal.

The password is not hidden through exploitation, encryption, or obfuscation. It is simply stored in a readable file. That is why the lesson is foundational: before advanced exploitation matters, a learner must understand how to inspect the environment carefully.

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
    <td>Trying to search the entire system immediately.</td>
    <td>The level goal already says the file is in the home directory. Start with the simplest evidence before using broader search commands.<br><br></td>
  </tr>
  <tr>
    <td>Copying the password into a public repo or screenshot.</td>
    <td>Credentials should be handled as sensitive material. Redact them in screenshots and avoid committing them to public GitHub repositories.<br><br></td>
  </tr>
  <tr>
    <td>Forgetting the custom SSH port.</td>
    <td>Bandit uses port 2220 for SSH. If the learner omits the port, the connection may fail or go to the wrong service.<br><br></td>
  </tr>
</table>

## 12. Defensive or Administrative Takeaway

This level demonstrates a basic but important administrative lesson: sensitive information should not be stored in readable plaintext files unless the access model is intentional and controlled.

In real systems, credentials should be protected through appropriate permissions, secret management tools, auditing, rotation, and access controls. Even when a file is easy to read for a lab exercise, the real-world lesson is that defenders must know where secrets are stored and who can access them.

## 13. Real-World Connection

The same concepts appear constantly in real Linux administration and incident response. Analysts inspect directories, review files, verify paths, check user context, and look for exposed secrets. Cloud servers, CI/CD runners, developer workstations, and application directories may all contain configuration files, tokens, keys, or credentials if secret management practices are weak.

The beginner command `cat readme` is simple, but the underlying habit is professional: inspect the environment, verify assumptions, read only what is needed, and protect sensitive findings.

## 14. Reflection Questions

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
    <td><code>man ls</code></td>
    <td>Explains how to list directory contents and use options such as long format or hidden file display.<br><br></td>
  </tr>
  <tr>
    <td><code>man cat</code></td>
    <td>Explains how <code>cat</code> reads files and writes content to standard output.<br><br></td>
  </tr>
  <tr>
    <td><code>man ssh</code></td>
    <td>Explains SSH syntax, including the use of a non-default port with <code>-p</code>.<br><br></td>
  </tr>
</table>
