# Bandit Level 5 to Level 6

In this level, you will learn how to search through many directories and locate a file based on multiple file properties.

The password for the next level is stored somewhere inside the `inhere` directory. The correct file has three important characteristics: it is human-readable, it is 1033 bytes in size, and it is not executable. Your job is to search systematically instead of opening files one by one.

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
    <td>Bandit Level 5 to Level 6<br><br></td>
  </tr>
  <tr>
    <td>Category</td>
    <td>Linux fundamentals, SSH, recursive search, file size, file permissions, file type inspection<br><br></td>
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

By the end of this level, you should understand how to use file properties to search efficiently. You should also understand why `find` is more appropriate than manually checking every directory.

<table>
  <tr>
    <th width="30%">Learning Layer</th>
    <th width="70%">Objective</th>
  </tr>
  <tr>
    <td>Beginner</td>
    <td>You will learn how to connect to the Bandit server from WSL, move into a directory, and search through multiple subdirectories for a file matching specific criteria.<br><br></td>
  </tr>
  <tr>
    <td>Practitioner</td>
    <td>You will practice using <code>find</code> to filter files by type, size, and executable permissions instead of manually inspecting each candidate file.<br><br></td>
  </tr>
  <tr>
    <td>Advanced</td>
    <td>You will connect this exercise to a broader systems and security principle: effective investigation depends on narrowing a search space with reliable metadata and testable criteria.<br><br></td>
  </tr>
</table>

## 3. Level Summary

The official level goal says the password for the next level is stored in a file somewhere under the `inhere` directory.

The correct file has these properties:

```text
human-readable
1033 bytes in size
not executable
```

When you enter `inhere`, you will see many subdirectories named like this:

```text
maybehere00
maybehere01
maybehere02
...
maybehere19
```

This is a sign that manual inspection would be inefficient. Instead of opening directories one by one, use `find` to search recursively for files that match the known properties.

A useful command is:

```bash
find . -type f -size 1033c ! -executable
```

Then read the matching file with `cat`.

Official level reference:

```text
https://overthewire.org/wargames/bandit/bandit6.html
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
    <td>Recursive search</td>
    <td>A recursive search examines a directory and its subdirectories. In this level, the file is somewhere under <code>inhere</code>, so recursive search is more efficient than checking each folder manually.<br><br></td>
  </tr>
  <tr>
    <td>File type filter</td>
    <td>The <code>-type f</code> option tells <code>find</code> to return regular files, not directories or other filesystem objects.<br><br></td>
  </tr>
  <tr>
    <td>File size filter</td>
    <td>The <code>-size 1033c</code> option tells <code>find</code> to look for files that are exactly 1033 bytes. The <code>c</code> means bytes.<br><br></td>
  </tr>
  <tr>
    <td>Executable permission filter</td>
    <td>The <code>! -executable</code> condition tells <code>find</code> to exclude files that are executable by the current user.<br><br></td>
  </tr>
  <tr>
    <td>Human-readable file</td>
    <td>A human-readable file contains text that can be meaningfully displayed in the terminal. The <code>file</code> command can help confirm whether a candidate file appears to contain text.<br><br></td>
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
    <td>The level goal tells you the password is somewhere under that directory, so you need to search inside it.<br><br></td>
  </tr>
  <tr>
    <td>The <code>inhere</code> directory contains many subdirectories.</td>
    <td>This tells you that manual inspection would be slow and error-prone. You need a search strategy.<br><br></td>
  </tr>
  <tr>
    <td>The level gives exact file properties.</td>
    <td>The properties are clues that can be translated into <code>find</code> filters.<br><br></td>
  </tr>
  <tr>
    <td>The size is specified as 1033 bytes.</td>
    <td>This can be searched directly with <code>-size 1033c</code>. The <code>c</code> means bytes.<br><br></td>
  </tr>
  <tr>
    <td>The file is not executable.</td>
    <td>This can be represented with <code>! -executable</code>, which excludes files that the current user can execute.<br><br></td>
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
    <td>Do not open every file manually. Translate the level’s clues into search conditions.<br><br></td>
  </tr>
  <tr>
    <td>Hint 4</td>
    <td>Use <code>find</code> to search for regular files that are exactly 1033 bytes and not executable.<br><br></td>
  </tr>
</table>

## 7. Commands Introduced

These commands are not just things to memorize. Each one teaches you something about remote login, directory navigation, recursive search, or file metadata.

<table>
  <tr>
    <th width="30%">Command or Tool</th>
    <th width="70%">Explanation</th>
  </tr>
  <tr>
    <td><code>ssh bandit5@bandit.labs.overthewire.org -p 2220</code></td>
    <td>Connects from your local terminal to the remote OverTheWire Bandit server as user <code>bandit5</code> on port <code>2220</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>pwd</code></td>
    <td>Prints your current working directory. This helps you verify where you are after logging in.<br><br></td>
  </tr>
  <tr>
    <td><code>ls</code></td>
    <td>Lists visible files and directories in the current directory. In this level, it shows the <code>inhere</code> directory and then the many subdirectories inside it.<br><br></td>
  </tr>
  <tr>
    <td><code>cd inhere</code></td>
    <td>Changes your current working directory to the <code>inhere</code> directory.<br><br></td>
  </tr>
  <tr>
    <td><code>find . -type f -size 1033c ! -executable</code></td>
    <td>Searches from the current directory for regular files that are exactly 1033 bytes and not executable by the current user.<br><br></td>
  </tr>
  <tr>
    <td><code>file ./path/to/candidate</code></td>
    <td>Checks whether a candidate file appears to contain human-readable text or another type of data.<br><br></td>
  </tr>
  <tr>
    <td><code>cat ./path/to/candidate</code></td>
    <td>Reads the candidate file once you have identified it as the likely password file.<br><br></td>
  </tr>
  <tr>
    <td><code>ssh bandit6@bandit.labs.overthewire.org -p 2220</code></td>
    <td>Connects to the next Bandit account after you retrieve the password from the matching file.<br><br></td>
  </tr>
</table>

## 8. Walkthrough Without Credential Disclosure

This walkthrough assumes you are working from a local terminal, such as Windows Subsystem for Linux, macOS Terminal, or a Linux shell. The examples below use WSL because it gives Windows users a Linux-like command-line environment.

### Step 1

Open WSL and connect to the Bandit server as `bandit5`.

```bash
ssh bandit5@bandit.labs.overthewire.org -p 2220
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
    <td><code>bandit5</code></td>
    <td>The username for this level. Each Bandit level has its own user account, such as <code>bandit4</code>, <code>bandit5</code>, and <code>bandit6</code>.<br><br></td>
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

This tells you where to search next.

### Step 4

Move into the `inhere` directory.

```bash
cd inhere
```

Your prompt may change to show that you are now inside `~/inhere`.

### Step 5

List the contents of `inhere`.

```bash
ls
```

You should see many subdirectories named something like:

```text
maybehere00  maybehere01  maybehere02  maybehere03  maybehere04
maybehere05  maybehere06  maybehere07  maybehere08  maybehere09
maybehere10  maybehere11  maybehere12  maybehere13  maybehere14
maybehere15  maybehere16  maybehere17  maybehere18  maybehere19
```

This is your signal to stop thinking manually. You do not want to inspect every directory and every file by hand if the level gives you searchable properties.

### Step 6

Use `find` to search for the matching file.

```bash
find . -type f -size 1033c ! -executable
```

This command searches from the current directory, represented by `.`, and applies three conditions.

<table>
  <tr>
    <th width="35%">Command Part</th>
    <th width="65%">Meaning</th>
  </tr>
  <tr>
    <td><code>find .</code></td>
    <td>Start searching from the current directory and continue through its subdirectories.<br><br></td>
  </tr>
  <tr>
    <td><code>-type f</code></td>
    <td>Return regular files, not directories.<br><br></td>
  </tr>
  <tr>
    <td><code>-size 1033c</code></td>
    <td>Return files that are exactly 1033 bytes. The <code>c</code> means bytes.<br><br></td>
  </tr>
  <tr>
    <td><code>! -executable</code></td>
    <td>Return files that are not executable by the current user.<br><br></td>
  </tr>
</table>

You should get one matching path. That path is the candidate password file.

### Step 7

Optionally confirm that the candidate is human-readable.

```bash
file ./path/to/candidate
```

Replace `./path/to/candidate` with the path returned by `find`.

If the file appears to be text or ASCII text, it matches the human-readable clue.

### Step 8

Read the candidate file.

```bash
cat ./path/to/candidate
```

Replace `./path/to/candidate` with the path returned by `find`.

The output is the password for the next Bandit level. Do not commit that password to GitHub.

### Step 9

Use the discovered password to log in to the next level.

```bash
ssh bandit6@bandit.labs.overthewire.org -p 2220
```

When prompted, enter the password you found in the matching file. Again, the terminal may not show characters while the password is typed. That is normal behavior.

At this point, you have moved from `bandit5` to `bandit6`.

## 9. Command Output and Screenshots

Use this section to include terminal output or screenshots after redacting credentials.

### Relevant Command Output

```text
$ ssh bandit5@bandit.labs.overthewire.org -p 2220
bandit5@bandit.labs.overthewire.org's password:
[successful login output omitted]

$ pwd
/home/bandit5

$ ls
inhere

$ cd inhere

$ ls
maybehere00  maybehere03  maybehere06  maybehere09  maybehere12  maybehere15  maybehere18
maybehere01  maybehere04  maybehere07  maybehere10  maybehere13  maybehere16  maybehere19
maybehere02  maybehere05  maybehere08  maybehere11  maybehere14  maybehere17

$ find . -type f -size 1033c ! -executable
./maybehereXX/.fileX

$ file ./maybehereXX/.fileX
./maybehereXX/.fileX: ASCII text

$ cat ./maybehereXX/.fileX
[REDACTED PASSWORD]
```

This output shows the central lesson. Instead of checking every directory manually, you use `find` to narrow the search based on the exact properties provided by the level.

### Screenshot

<img width="734" height="407" alt="image" src="https://github.com/user-attachments/assets/7ee72bfe-2c66-4737-b5e4-f60b4def33d6" />


<img width="734" height="407" alt="image" src="https://github.com/user-attachments/assets/d284f504-11c1-4e6a-b439-59393b17c18f" />

## 10. What Is Really Happening

In this level, you are learning how to search by file metadata and properties.

A normal `ls` shows you names, but names alone are not enough. The level gives you structured criteria: the file is human-readable, exactly 1033 bytes, and not executable. Those criteria can be translated into a command.

The `find` command is useful because it can search recursively and filter results. Instead of looking inside every `maybehere` directory by hand, you ask the system to return only regular files matching the size and permission properties.

When you run:

```bash
find . -type f -size 1033c ! -executable
```

you are asking a precise question:

```text
Starting here, show me regular files that are exactly 1033 bytes and not executable.
```

The dot means the current directory. The `-type f` condition restricts the result to files. The `-size 1033c` condition restricts the result by byte size. The `! -executable` condition excludes executable files.

This level teaches a professional habit: use known facts to reduce the search space.

## 11. Common Mistakes

<table>
  <tr>
    <th width="35%">Mistake</th>
    <th width="65%">Correction</th>
  </tr>
  <tr>
    <td>Opening every file manually.</td>
    <td>You could do that, but it is slow and error-prone. The level gives you criteria that can be turned into a search command.<br><br></td>
  </tr>
  <tr>
    <td>Forgetting to search recursively.</td>
    <td>The file is somewhere under <code>inhere</code>, inside one of many subdirectories. Use <code>find</code> so the search includes subdirectories.<br><br></td>
  </tr>
  <tr>
    <td>Using the wrong size unit.</td>
    <td>Use <code>1033c</code> for 1033 bytes. Without understanding the unit, your search may not match the intended file.<br><br></td>
  </tr>
  <tr>
    <td>Ignoring the not executable condition.</td>
    <td>The level gives multiple properties for a reason. Using all of them reduces false matches.<br><br></td>
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

This level shows why structured searching matters in security work.

During incident response, system administration, or forensic triage, you often need to find files based on properties such as size, owner, permissions, modification time, filename pattern, or content type. Searching manually is inefficient and easy to get wrong.

The level also teaches that good investigations use constraints. If you know a suspicious file is a certain size, not executable, recently modified, owned by a certain user, or located under a specific directory, those facts should shape your search.

## 13. Real-World Connection

This concept appears in real systems whenever analysts need to find relevant files among many candidates. Examples include locating suspicious scripts, identifying unusual binaries, finding world-writable files, searching for large log files, locating recently modified files, or triaging unknown artifacts.

The `find` command is a foundational tool for Linux administration and security operations. It allows you to search with precision instead of relying on guesswork.

This level also reinforces the importance of translating a plain-language requirement into a technical query. The level says the file is human-readable, 1033 bytes, and not executable. A practitioner turns that into a repeatable command.

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
    <td>Why is <code>find</code> better than manually opening every file?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What does <code>-type f</code> do?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What does <code>-size 1033c</code> mean?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What does <code>! -executable</code> mean?</td>
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
    <td>OverTheWire Bandit Level 5 to Level 6</td>
    <td>Provides the official level goal and command suggestions for this exercise.</td>
  </tr>
  <tr>
    <td><code>man ssh</code></td>
    <td>Explains SSH syntax, remote login behavior, authentication, and the use of a non-default port with <code>-p</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>man find</code></td>
    <td>Explains recursive file searching, filters such as <code>-type</code> and <code>-size</code>, and expressions such as <code>!</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>man file</code></td>
    <td>Explains how the <code>file</code> command determines file type based on file contents.<br><br></td>
  </tr>
  <tr>
    <td><code>man cat</code></td>
    <td>Explains how <code>cat</code> reads files and writes content to standard output.<br><br></td>
  </tr>
</table>
