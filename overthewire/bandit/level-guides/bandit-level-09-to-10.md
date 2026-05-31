# Bandit Level 9 to Level 10

In this level, you will learn how to extract readable text from a file that contains mostly non-readable data.

The password for the next level is stored in `data.txt`. The file contains human-readable strings, and the password is located near several `=` characters. Your job is to filter the file so the readable text becomes visible, then search for the useful pattern.

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
    <td>Bandit Level 9 to Level 10<br><br></td>
  </tr>
  <tr>
    <td>Category</td>
    <td>Linux fundamentals, SSH, readable strings, binary data, filtering, pattern search<br><br></td>
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

By the end of this level, you should understand how to use `strings` to extract human-readable text from a file that contains mostly non-readable data. You should also understand how to combine `strings` with `grep` to search for a useful pattern.

<table>
  <tr>
    <th width="30%">Learning Layer</th>
    <th width="70%">Objective</th>
  </tr>
  <tr>
    <td>Beginner</td>
    <td>You will learn how to connect to the Bandit server from WSL and identify readable text inside a file that is not useful to inspect with normal <code>cat</code> output.<br><br></td>
  </tr>
  <tr>
    <td>Practitioner</td>
    <td>You will practice using <code>strings</code>, <code>grep</code>, and a pipeline to extract and filter relevant evidence from noisy file content.<br><br></td>
  </tr>
  <tr>
    <td>Advanced</td>
    <td>You will connect this exercise to a broader security principle: analysts often need to extract useful human-readable indicators from binary files, memory artifacts, malware samples, logs, or mixed-content data.<br><br></td>
  </tr>
</table>

## 3. Level Summary

The official level goal says the password for the next level is stored in `data.txt`, in one of the few human-readable strings, preceded by several `=` characters.

That gives you three useful clues:

```text
The file to inspect: data.txt
The data of interest: human-readable strings
The pattern to look for: several = characters
```

A useful command is:

```bash
strings data.txt | grep =
```

A more focused version is:

```bash
strings data.txt | grep ===
```

The `strings` command extracts readable text from the file. The pipe sends that readable output into `grep`, which searches for lines containing the pattern.

Official level reference:

```text
https://overthewire.org/wargames/bandit/bandit10.html
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
    <td>Human-readable strings</td>
    <td>Human-readable strings are sequences of characters that can be meaningfully displayed as text. A file may contain mostly binary or non-readable content while still containing a few readable strings.<br><br></td>
  </tr>
  <tr>
    <td><code>strings</code></td>
    <td><code>strings</code> scans a file and prints sequences of printable characters. It is useful when normal file output is unreadable or noisy.<br><br></td>
  </tr>
  <tr>
    <td><code>grep</code></td>
    <td><code>grep</code> searches input for lines matching a pattern. In this level, it helps you search the readable strings for lines containing <code>=</code> characters.<br><br></td>
  </tr>
  <tr>
    <td>Pipeline</td>
    <td>A pipeline uses <code>|</code> to send the output of one command into another command. Here, the output of <code>strings data.txt</code> becomes the input to <code>grep</code>.<br><br></td>
  </tr>
  <tr>
    <td>Signal in noisy data</td>
    <td>Noisy data contains a lot of irrelevant or unreadable content. Your goal is to extract the meaningful signal from that noise.<br><br></td>
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
    <td>The file is named <code>data.txt</code>.</td>
    <td>The level tells you exactly which file to inspect, so you do not need a broad filesystem search.<br><br></td>
  </tr>
  <tr>
    <td>The file contains mostly non-readable data.</td>
    <td>A normal <code>cat data.txt</code> may produce unreadable or messy output. You need a tool that extracts printable text.<br><br></td>
  </tr>
  <tr>
    <td>The password is near several <code>=</code> characters.</td>
    <td>This gives you a searchable pattern after extracting readable strings.<br><br></td>
  </tr>
  <tr>
    <td>The pipeline connects extraction and filtering.</td>
    <td><code>strings</code> extracts readable text, and <code>grep</code> filters that text for the pattern you care about.<br><br></td>
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
    <td>The level says the password is in one of the few human-readable strings. Think about a command that extracts readable strings from a file.<br><br></td>
  </tr>
  <tr>
    <td>Hint 3</td>
    <td>After extracting readable strings, search for lines containing <code>=</code> characters.<br><br></td>
  </tr>
  <tr>
    <td>Hint 4</td>
    <td>Use a pipeline so the output of <code>strings</code> becomes the input to <code>grep</code>.<br><br></td>
  </tr>
</table>

## 7. Commands Introduced

These commands are not just things to memorize. Each one teaches you something about remote login, file inspection, text extraction, filtering, or command composition.

<table>
  <tr>
    <th width="30%">Command or Tool</th>
    <th width="70%">Explanation</th>
  </tr>
  <tr>
    <td><code>ssh bandit9@bandit.labs.overthewire.org -p 2220</code></td>
    <td>Connects from your local terminal to the remote OverTheWire Bandit server as user <code>bandit9</code> on port <code>2220</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>pwd</code></td>
    <td>Prints your current working directory. This helps you verify where you are after logging in.<br><br></td>
  </tr>
  <tr>
    <td><code>ls</code></td>
    <td>Lists visible files and directories in the current directory. In this level, it should show <code>data.txt</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>cat data.txt</code></td>
    <td>Prints the file directly. This may produce messy or unreadable output in this level, which helps explain why <code>strings</code> is useful.<br><br></td>
  </tr>
  <tr>
    <td><code>strings data.txt</code></td>
    <td>Extracts printable character sequences from <code>data.txt</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>grep =</code></td>
    <td>Searches input for lines containing an equals sign.<br><br></td>
  </tr>
  <tr>
    <td><code>strings data.txt | grep =</code></td>
    <td>Extracts readable strings from the file and filters the results for lines containing <code>=</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>ssh bandit10@bandit.labs.overthewire.org -p 2220</code></td>
    <td>Connects to the next Bandit account after you retrieve the password from the matching string.<br><br></td>
  </tr>
</table>

## 8. Walkthrough Without Credential Disclosure

This walkthrough assumes you are working from a local terminal, such as Windows Subsystem for Linux, macOS Terminal, or a Linux shell. The examples below use WSL because it gives Windows users a Linux-like command-line environment.

### Step 1

Open WSL and connect to the Bandit server as `bandit9`.

```bash
ssh bandit9@bandit.labs.overthewire.org -p 2220
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
    <td><code>bandit9</code></td>
    <td>The username for this level. Each Bandit level has its own user account, such as <code>bandit8</code>, <code>bandit9</code>, and <code>bandit10</code>.<br><br></td>
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

You should see a file named:

```text
data.txt
```

This tells you which file to inspect.

### Step 4

Avoid relying on normal file output.

```bash
cat data.txt
```

This may produce unreadable or messy output. That is useful to notice. It tells you that normal text display is not the best tool for this file.

### Step 5

Extract human-readable strings.

```bash
strings data.txt
```

This command prints readable character sequences from the file. You may still see several lines, so the next step is to filter for the pattern described in the level.

### Step 6

Search the readable strings for the equals-sign pattern.

```bash
strings data.txt | grep =
```

You can also search more narrowly for multiple equals signs:

```bash
strings data.txt | grep ===
```

The output should show the line containing the password for the next Bandit level. Do not commit that password to GitHub.

### Step 7

Use the discovered password to log in to the next level.

```bash
ssh bandit10@bandit.labs.overthewire.org -p 2220
```

When prompted, enter the password you found from the matching string. Again, the terminal may not show characters while the password is typed. That is normal behavior.

At this point, you have moved from `bandit9` to `bandit10`.

## 9. Command Output and Screenshots

Use this section to include terminal output or screenshots after redacting credentials.

### Relevant Command Output

```text
$ ssh bandit9@bandit.labs.overthewire.org -p 2220
bandit9@bandit.labs.overthewire.org's password:
[successful login output omitted]

$ pwd
/home/bandit9

$ ls
data.txt

$ strings data.txt | grep =
========== [REDACTED PASSWORD]
```

This output shows the central lesson. `strings` extracts readable text from noisy file content, and `grep` filters that output for the pattern described in the level.

### Screenshots

<img width="817" height="323" alt="image" src="https://github.com/user-attachments/assets/df8cd617-9eaf-4ffb-86fa-aa306e1b2da8" />

<img width="867" height="323" alt="image" src="https://github.com/user-attachments/assets/9fdb26b7-e486-4ebe-a846-0e49c4dddd4a" />

## 10. What Is Really Happening

In this level, you are learning that files are not always clean text files.

A file can contain binary or non-readable data while still containing readable character sequences. If you use `cat`, your terminal may display messy output because it is trying to print data that was not meant to be read directly as text.

The `strings` command scans the file and extracts sequences of printable characters. This does not fully decode or analyze the file, but it gives you a useful first look at readable content embedded inside it.

When you run:

```bash
strings data.txt | grep =
```

you are asking the system:

```text
Extract readable strings from data.txt, then show me only the lines that contain an equals sign.
```

The pipe symbol `|` connects the two operations. First, `strings` reduces the file to readable text. Then `grep` reduces that text to the lines matching the clue.

This level teaches a professional habit: when direct viewing produces noise, use tools that extract the kind of signal you need.

## 11. Common Mistakes

<table>
  <tr>
    <th width="35%">Mistake</th>
    <th width="65%">Correction</th>
  </tr>
  <tr>
    <td>Trying to read the file only with <code>cat</code>.</td>
    <td><code>cat</code> prints the file directly, but this file contains mostly non-readable data. Use <code>strings</code> to extract readable text.<br><br></td>
  </tr>
  <tr>
    <td>Using <code>grep</code> directly on noisy output without understanding the input.</td>
    <td><code>grep</code> is useful, but the key first step is extracting readable strings from the file.<br><br></td>
  </tr>
  <tr>
    <td>Forgetting the pipe.</td>
    <td>The pipe sends the output of <code>strings data.txt</code> into <code>grep</code>. This lets you combine extraction and filtering in one command.<br><br></td>
  </tr>
  <tr>
    <td>Searching for the wrong pattern.</td>
    <td>The level says the password is preceded by several <code>=</code> characters. Search for <code>=</code> or multiple equals signs.<br><br></td>
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

This level shows why extracting readable strings is useful in cybersecurity work.

Security analysts often inspect files that are not plain text: binaries, memory dumps, malware samples, packet captures, compressed data, or mixed-content artifacts. These files may still contain readable clues such as URLs, file paths, commands, usernames, error messages, configuration fragments, or embedded strings.

The `strings` command is not a complete analysis tool, but it is a fast first-pass technique for finding readable indicators inside noisy files.

## 13. Real-World Connection

This concept appears in malware analysis, digital forensics, incident response, reverse engineering, and system administration.

For example, an analyst might run `strings` against a suspicious binary to look for domains, IP addresses, hardcoded paths, suspicious commands, registry keys, or embedded configuration values. The analyst might then pipe that output into `grep` to search for specific patterns.

The level is simple, but the habit is professional: extract readable signal from noisy data, then filter for the clue that matters.

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
    <td>Why might <code>cat data.txt</code> be unhelpful in this level?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What does <code>strings data.txt</code> do?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What does <code>grep =</code> filter for?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What does the pipe symbol <code>|</code> do in this command?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>How does this level connect to malware analysis or digital forensics?</td>
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
    <td>OverTheWire Bandit Level 9 to Level 10</td>
    <td>Provides the official level goal and command suggestions for this exercise.</td>
  </tr>
  <tr>
    <td><code>man ssh</code></td>
    <td>Explains SSH syntax, remote login behavior, authentication, and the use of a non-default port with <code>-p</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>man strings</code></td>
    <td>Explains how <code>strings</code> prints printable character sequences from files.<br><br></td>
  </tr>
  <tr>
    <td><code>man grep</code></td>
    <td>Explains how <code>grep</code> searches input for matching patterns.<br><br></td>
  </tr>
  <tr>
    <td><code>man bash</code></td>
    <td>Provides background on pipelines, standard input, and standard output.<br><br></td>
  </tr>
</table>
