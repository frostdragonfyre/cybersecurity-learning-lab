# Bandit Level 6 to Level 7

In this level, you will learn how to search the entire filesystem for a file based on ownership, group ownership, and file size.

The password for the next level is stored somewhere on the server. The correct file has three important properties: it is owned by user `bandit7`, it is owned by group `bandit6`, and it is 33 bytes in size. Your job is to translate those clues into a precise search command.

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
    <td>Bandit Level 6 to Level 7<br><br></td>
  </tr>
  <tr>
    <td>Category</td>
    <td>Linux fundamentals, SSH, filesystem search, ownership, group ownership, file size, permission errors<br><br></td>
  </tr>
  <tr>
    <td>Difficulty</td>
    <td>Beginner to intermediate<br><br></td>
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

By the end of this level, you should understand how to use `find` to search across the filesystem using ownership, group ownership, and size filters. You should also understand why permission errors appear during broad searches and how to redirect error output when it is not useful.

<table>
  <tr>
    <th width="30%">Learning Layer</th>
    <th width="70%">Objective</th>
  </tr>
  <tr>
    <td>Beginner</td>
    <td>You will learn how to connect to the Bandit server from WSL and search for a file using specific clues about owner, group, and size.<br><br></td>
  </tr>
  <tr>
    <td>Practitioner</td>
    <td>You will practice turning a plain-language requirement into a precise <code>find</code> command and filtering out distracting permission errors.<br><br></td>
  </tr>
  <tr>
    <td>Advanced</td>
    <td>You will connect this exercise to a broader security principle: ownership, group membership, and permissions are core parts of Unix-like access control and are essential during system administration, incident response, and forensic triage.<br><br></td>
  </tr>
</table>

## 3. Level Summary

The official level goal says the password for the next level is stored somewhere on the server and has these properties:

```text
owned by user bandit7
owned by group bandit6
33 bytes in size
```

Unlike the previous level, the file is not limited to the current directory. You need to search more broadly across the filesystem.

A useful command is:

```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

This command searches from the filesystem root, filters by owner, group, and size, and suppresses permission-denied errors.

Official level reference:

```text
https://overthewire.org/wargames/bandit/bandit7.html
```

## 4. Concepts Introduced

<table>
  <tr>
    <th width="30%">Concept</th>
    <th width="70%">Explanation</th>
  </tr>
  <tr>
    <td>Filesystem root</td>
    <td>The path <code>/</code> represents the root of the filesystem. Searching from <code>/</code> means searching broadly across the server rather than only inside the current directory.<br><br></td>
  </tr>
  <tr>
    <td>File owner</td>
    <td>Every file has an owning user. In this level, the correct file is owned by user <code>bandit7</code>.<br><br></td>
  </tr>
  <tr>
    <td>Group owner</td>
    <td>Every file also has an owning group. In this level, the correct file belongs to group <code>bandit6</code>.<br><br></td>
  </tr>
  <tr>
    <td>File size</td>
    <td>The correct file is exactly 33 bytes. The <code>-size 33c</code> filter searches for files that are exactly 33 bytes, where <code>c</code> means bytes.<br><br></td>
  </tr>
  <tr>
    <td>Permission errors</td>
    <td>When searching the whole filesystem, you may enter directories that your user cannot read. The resulting permission errors are expected and do not necessarily mean the command failed.<br><br></td>
  </tr>
  <tr>
    <td>Standard error</td>
    <td>Error messages are usually written to standard error, also called <code>stderr</code>. Redirecting <code>stderr</code> can make command output easier to read.<br><br></td>
  </tr>
  <tr>
    <td><code>/dev/null</code></td>
    <td><code>/dev/null</code> is a special location that discards anything written to it. Redirecting errors to <code>/dev/null</code> hides irrelevant permission-denied messages.<br><br></td>
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
    <td>The password file is somewhere on the server.</td>
    <td>This means the search is broader than the current directory. Starting from <code>/</code> searches the filesystem from the root.<br><br></td>
  </tr>
  <tr>
    <td>The level gives ownership and group clues.</td>
    <td>These are not random facts. They can be translated into <code>find</code> filters: <code>-user bandit7</code> and <code>-group bandit6</code>.<br><br></td>
  </tr>
  <tr>
    <td>The file size is exactly 33 bytes.</td>
    <td>This can be searched directly with <code>-size 33c</code>. The <code>c</code> means bytes.<br><br></td>
  </tr>
  <tr>
    <td>You may see many permission-denied errors.</td>
    <td>This is normal when searching the whole filesystem as a limited user. Redirecting errors helps you focus on useful results.<br><br></td>
  </tr>
  <tr>
    <td>The final result should be a file path.</td>
    <td>Once <code>find</code> returns the matching path, you can read that file with <code>cat</code>.<br><br></td>
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
    <td>The file is not necessarily in your home directory. Think about where to start a full filesystem search.<br><br></td>
  </tr>
  <tr>
    <td>Hint 2</td>
    <td>The clues about user, group, and size can be translated into <code>find</code> options.<br><br></td>
  </tr>
  <tr>
    <td>Hint 3</td>
    <td>If the screen fills with permission errors, the useful result may be hidden among error messages. Think about redirecting standard error.<br><br></td>
  </tr>
  <tr>
    <td>Hint 4</td>
    <td>Use <code>2&gt;/dev/null</code> to hide permission errors and focus on successful matches.<br><br></td>
  </tr>
</table>

## 7. Commands Introduced

These commands are not just things to memorize. Each one teaches you something about remote login, filesystem search, file ownership, or error handling.

<table>
  <tr>
    <th width="30%">Command or Tool</th>
    <th width="70%">Explanation</th>
  </tr>
  <tr>
    <td><code>ssh bandit6@bandit.labs.overthewire.org -p 2220</code></td>
    <td>Connects from your local terminal to the remote OverTheWire Bandit server as user <code>bandit6</code> on port <code>2220</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>find /</code></td>
    <td>Starts a search from the root of the filesystem.<br><br></td>
  </tr>
  <tr>
    <td><code>-user bandit7</code></td>
    <td>Filters results to files owned by user <code>bandit7</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>-group bandit6</code></td>
    <td>Filters results to files owned by group <code>bandit6</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>-size 33c</code></td>
    <td>Filters results to files that are exactly 33 bytes. The <code>c</code> means bytes.<br><br></td>
  </tr>
  <tr>
    <td><code>2&gt;/dev/null</code></td>
    <td>Redirects standard error to <code>/dev/null</code>, which hides permission-denied messages and other errors.<br><br></td>
  </tr>
  <tr>
    <td><code>cat /path/to/file</code></td>
    <td>Reads the matching file after <code>find</code> identifies the path.<br><br></td>
  </tr>
  <tr>
    <td><code>ssh bandit7@bandit.labs.overthewire.org -p 2220</code></td>
    <td>Connects to the next Bandit account after you retrieve the password from the matching file.<br><br></td>
  </tr>
</table>

## 8. Walkthrough Without Credential Disclosure

This walkthrough assumes you are working from a local terminal, such as Windows Subsystem for Linux, macOS Terminal, or a Linux shell. The examples below use WSL because it gives Windows users a Linux-like command-line environment.

### Step 1

Open WSL and connect to the Bandit server as `bandit6`.

```bash
ssh bandit6@bandit.labs.overthewire.org -p 2220
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
    <td><code>bandit6</code></td>
    <td>The username for this level. Each Bandit level has its own user account, such as <code>bandit5</code>, <code>bandit6</code>, and <code>bandit7</code>.<br><br></td>
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

Start with the level clues.

The level tells you the file is:

```text
owned by user bandit7
owned by group bandit6
33 bytes in size
```

These are search criteria. Your task is to turn them into a command.

### Step 3

Run a broad filesystem search.

```bash
find / -user bandit7 -group bandit6 -size 33c
```

You may see many `Permission denied` messages. That is expected. You are searching from `/`, and your user does not have permission to read every directory on the system.

### Step 4

Run the same search while hiding irrelevant error messages.

```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

This command keeps the useful output but hides errors written to standard error.

You should get one matching file path.

### Step 5

Read the matching file.

```bash
cat /path/to/matching/file
```

Replace `/path/to/matching/file` with the path returned by `find`.

The output is the password for the next Bandit level. Do not commit that password to GitHub.

### Step 6

Use the discovered password to log in to the next level.

```bash
ssh bandit7@bandit.labs.overthewire.org -p 2220
```

When prompted, enter the password you found in the matching file. Again, the terminal may not show characters while the password is typed. That is normal behavior.

At this point, you have moved from `bandit6` to `bandit7`.

## 9. Command Output and Screenshots

Use this section to include terminal output or screenshots after redacting credentials.

### Relevant Command Output

```text
$ ssh bandit6@bandit.labs.overthewire.org -p 2220
bandit6@bandit.labs.overthewire.org's password:
[successful login output omitted]

$ find / -user bandit7 -group bandit6 -size 33c
find: '/root': Permission denied
find: '/etc/ssl/private': Permission denied
[additional permission errors omitted]

$ find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
/path/to/matching/file

$ cat /path/to/matching/file
[REDACTED PASSWORD]
```

This output shows the central lesson. A broad filesystem search may produce permission errors, but redirecting standard error allows you to focus on the matching result.

### Screenshots

<img width="867" height="407" alt="image" src="https://github.com/user-attachments/assets/5e0e2d10-6ba0-4def-9f1e-6f139cf21cd6" />

<img width="867" height="604" alt="image" src="https://github.com/user-attachments/assets/378e4472-881e-4491-8cb6-32f7e34aaaf5" />

<img width="867" height="604" alt="image" src="https://github.com/user-attachments/assets/a6f47ce8-164d-480e-b973-bd5ac1571b5c" />

## 10. What Is Really Happening

In this level, you are learning how to search for files based on metadata.

Metadata is information about a file, such as its owner, group, permissions, size, path, and timestamps. The level gives you metadata clues rather than a filename. That means your job is not to browse manually. Your job is to search by properties.

When you run:

```bash
find / -user bandit7 -group bandit6 -size 33c
```

you are asking the system:

```text
Starting at the filesystem root, show me files owned by user bandit7, owned by group bandit6, and exactly 33 bytes in size.
```

The reason permission errors appear is that the Bandit user does not have permission to read every directory on the server. This is normal in Unix-like systems. Access control limits which users can inspect which parts of the filesystem.

When you add:

```bash
2>/dev/null
```

you redirect standard error to `/dev/null`. The number `2` represents standard error. The destination `/dev/null` discards whatever is written to it. This makes the output easier to read because the permission errors are hidden.

This level teaches a professional habit: turn clues into precise search filters, and separate useful results from noisy errors.

## 11. Common Mistakes

<table>
  <tr>
    <th width="35%">Mistake</th>
    <th width="65%">Correction</th>
  </tr>
  <tr>
    <td>Searching only the current directory.</td>
    <td>The level says the file is somewhere on the server, so the search should start from <code>/</code> unless you have a narrower known location.<br><br></td>
  </tr>
  <tr>
    <td>Thinking permission errors mean the command failed.</td>
    <td>Permission errors are expected during broad searches as a limited user. The useful result may still appear among the output.<br><br></td>
  </tr>
  <tr>
    <td>Forgetting the byte unit in <code>-size 33c</code>.</td>
    <td>The <code>c</code> means bytes. Without the right unit, the search may not match the intended file.<br><br></td>
  </tr>
  <tr>
    <td>Using only one clue instead of all three.</td>
    <td>The owner, group, and size together make the search precise. Using only one clue may produce too many results.<br><br></td>
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

This level shows why file ownership and permissions matter in security and administration.

In real systems, ownership and group membership help determine who can access a file. During incident response or system administration, analysts often search for files owned by a specific user, group, service account, or process. That can reveal configuration files, logs, suspicious artifacts, misplaced secrets, or files created by an attacker.

The level also introduces error handling. Permission errors are not always failures. Sometimes they are expected signals from the access control model. Good analysts know how to distinguish useful output from expected noise.

## 13. Real-World Connection

This concept appears in real Linux administration, cloud operations, incident response, and forensic triage. Analysts may search for files by owner, group, permission, size, modification time, or location.

Examples include finding files owned by a compromised account, locating world-readable secrets, identifying unusual files created by a service account, or searching for small credential files hidden outside normal directories.

The command-line skill is simple, but the professional habit is important: translate investigative clues into precise, repeatable searches.

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
    <td>Why does the search start from <code>/</code>?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What does <code>-user bandit7</code> do?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What does <code>-group bandit6</code> do?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What does <code>2&gt;/dev/null</code> do?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>Why are permission errors expected during this search?</td>
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
    <td>OverTheWire Bandit Level 6 to Level 7</td>
    <td>Provides the official level goal and command suggestions for this exercise.</td>
  </tr>
  <tr>
    <td><code>man ssh</code></td>
    <td>Explains SSH syntax, remote login behavior, authentication, and the use of a non-default port with <code>-p</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>man find</code></td>
    <td>Explains recursive file searching and filters such as <code>-user</code>, <code>-group</code>, and <code>-size</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>man bash</code></td>
    <td>Provides background on redirection, standard output, and standard error.<br><br></td>
  </tr>
  <tr>
    <td><code>man chmod</code></td>
    <td>Provides background on permissions, which are closely related to ownership and access control.<br><br></td>
  </tr>
  <tr>
    <td><code>man chown</code></td>
    <td>Provides background on file ownership and group ownership.<br><br></td>
  </tr>
</table>
