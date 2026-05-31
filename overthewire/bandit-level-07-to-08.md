# Bandit Level 7 to Level 8

In this level, you will learn how to search inside a text file for a specific word.

The password for the next level is stored in the file `data.txt` next to the word `millionth`. Your job is to inspect the file efficiently by searching for the target word instead of reading through the entire file manually.

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
    <td>Bandit Level 7 to Level 8<br><br></td>
  </tr>
  <tr>
    <td>Category</td>
    <td>Linux fundamentals, SSH, text search, pattern matching, command-line investigation<br><br></td>
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

By the end of this level, you should understand how to search a text file for a known word using `grep`. You should also understand why targeted searching is better than manually scanning large files.

<table>
  <tr>
    <th width="30%">Learning Layer</th>
    <th width="70%">Objective</th>
  </tr>
  <tr>
    <td>Beginner</td>
    <td>You will learn how to connect to the Bandit server from WSL, locate a text file, and search inside it for a specific word.<br><br></td>
  </tr>
  <tr>
    <td>Practitioner</td>
    <td>You will practice using <code>grep</code> to find relevant lines in a file instead of reading all file contents manually.<br><br></td>
  </tr>
  <tr>
    <td>Advanced</td>
    <td>You will connect this exercise to a broader security and systems principle: effective investigation depends on filtering large amounts of text to find relevant evidence quickly and repeatably.<br><br></td>
  </tr>
</table>

## 3. Level Summary

The official level goal says the password for the next level is stored in the file `data.txt` next to the word `millionth`.

That means you already know two important facts:

```text
The file to inspect: data.txt
The keyword to search for: millionth
```

You do not need to read the whole file by hand. You can use `grep` to search for the line containing the target word:

```bash
grep millionth data.txt
```

The output should show the word `millionth` and the password next to it.

Official level reference:

```text
https://overthewire.org/wargames/bandit/bandit8.html
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
    <td>Text file</td>
    <td>A text file contains characters that can be displayed and searched meaningfully in a terminal. In this level, <code>data.txt</code> contains many lines of text.<br><br></td>
  </tr>
  <tr>
    <td>Pattern matching</td>
    <td>Pattern matching means searching for text that matches a specific word, phrase, or expression. In this level, the pattern is the word <code>millionth</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>grep</code></td>
    <td><code>grep</code> searches input for lines that match a pattern. It is one of the most useful tools for finding relevant text in files, logs, command output, and investigation data.<br><br></td>
  </tr>
  <tr>
    <td>Targeted search</td>
    <td>Targeted search means using known clues to narrow your work. Instead of reading the whole file, you search for the line that contains the known keyword.<br><br></td>
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
    <td>The password is next to a known word.</td>
    <td>The keyword <code>millionth</code> is the clue that lets you search directly for the relevant line.<br><br></td>
  </tr>
  <tr>
    <td>The file may contain many lines.</td>
    <td>Manual reading is inefficient. A search command is faster and less error-prone.<br><br></td>
  </tr>
  <tr>
    <td>The relevant line contains both the keyword and the password.</td>
    <td>Once <code>grep</code> finds the line, you can read the value next to the keyword and use it for the next level.<br><br></td>
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
    <td>The level tells you the filename and the word to search for. Use both clues.<br><br></td>
  </tr>
  <tr>
    <td>Hint 3</td>
    <td>Use a command that searches for matching lines inside a text file.<br><br></td>
  </tr>
  <tr>
    <td>Hint 4</td>
    <td>Search <code>data.txt</code> for the word <code>millionth</code>.<br><br></td>
  </tr>
</table>

## 7. Commands Introduced

These commands are not just things to memorize. Each one teaches you something about remote login, file inspection, or text searching.

<table>
  <tr>
    <th width="30%">Command or Tool</th>
    <th width="70%">Explanation</th>
  </tr>
  <tr>
    <td><code>ssh bandit7@bandit.labs.overthewire.org -p 2220</code></td>
    <td>Connects from your local terminal to the remote OverTheWire Bandit server as user <code>bandit7</code> on port <code>2220</code>.<br><br></td>
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
    <td><code>grep millionth data.txt</code></td>
    <td>Searches <code>data.txt</code> for lines containing the word <code>millionth</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>cat data.txt</code></td>
    <td>Prints the entire file. This works, but it is less efficient than searching directly for the known keyword.<br><br></td>
  </tr>
  <tr>
    <td><code>ssh bandit8@bandit.labs.overthewire.org -p 2220</code></td>
    <td>Connects to the next Bandit account after you retrieve the password from the matching line.<br><br></td>
  </tr>
</table>

## 8. Walkthrough Without Credential Disclosure

This walkthrough assumes you are working from a local terminal, such as Windows Subsystem for Linux, macOS Terminal, or a Linux shell. The examples below use WSL because it gives Windows users a Linux-like command-line environment.

### Step 1

Open WSL and connect to the Bandit server as `bandit7`.

```bash
ssh bandit7@bandit.labs.overthewire.org -p 2220
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
    <td><code>bandit7</code></td>
    <td>The username for this level. Each Bandit level has its own user account, such as <code>bandit6</code>, <code>bandit7</code>, and <code>bandit8</code>.<br><br></td>
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

Search for the keyword.

```bash
grep millionth data.txt
```

This command searches `data.txt` for any line containing the word `millionth`.

The output should include the keyword and the password for the next Bandit level. Do not commit that password to GitHub.

### Step 5

Use the discovered password to log in to the next level.

```bash
ssh bandit8@bandit.labs.overthewire.org -p 2220
```

When prompted, enter the password you found next to `millionth`. Again, the terminal may not show characters while the password is typed. That is normal behavior.

At this point, you have moved from `bandit7` to `bandit8`.

## 9. Command Output and Screenshots

Use this section to include terminal output or screenshots after redacting credentials.

### Relevant Command Output

```text
$ ssh bandit7@bandit.labs.overthewire.org -p 2220
bandit7@bandit.labs.overthewire.org's password:
[successful login output omitted]

$ pwd
/home/bandit7

$ ls
data.txt

$ grep millionth data.txt
millionth    [REDACTED PASSWORD]
```

This output shows the central lesson. Instead of reading the entire file manually, you use `grep` to find the line containing the known keyword.

### Screenshots

<img width="863" height="345" alt="image" src="https://github.com/user-attachments/assets/b34769a4-4606-443b-b92a-ab216a5b9a0f" />

<img width="867" height="212" alt="image" src="https://github.com/user-attachments/assets/f5cb3995-4d8c-4f8e-a5eb-bb6d4b0edbb9" />

## 10. What Is Really Happening

In this level, you are learning how to filter text.

A file can contain many lines, and only one of them may matter. If you print the whole file with `cat`, you may have to visually scan a large amount of output. That is inefficient and easy to get wrong.

When you run:

```bash
grep millionth data.txt
```

you are asking the system:

```text
Show me the lines in data.txt that contain the text millionth.
```

The command does not need to understand that the line contains a password. It only needs to match the word you gave it. This is the power of text search: you use a known clue to reduce a large amount of text to a small, relevant result.

This level teaches a professional habit: when you know what you are looking for, search for it directly.

## 11. Common Mistakes

<table>
  <tr>
    <th width="35%">Mistake</th>
    <th width="65%">Correction</th>
  </tr>
  <tr>
    <td>Using <code>cat data.txt</code> and manually scanning the whole file.</td>
    <td>This can work, but it is inefficient. Use <code>grep</code> when you know the word you are looking for.<br><br></td>
  </tr>
  <tr>
    <td>Misspelling the search term.</td>
    <td><code>grep</code> searches for the exact pattern you provide. If you misspell <code>millionth</code>, you may get no result.<br><br></td>
  </tr>
  <tr>
    <td>Searching the wrong file.</td>
    <td>The level identifies <code>data.txt</code>. Make sure you are searching the correct file in the correct remote shell.<br><br></td>
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

This level shows why text search is foundational for cybersecurity work.

Security analysts, system administrators, and incident responders constantly search logs, configuration files, command histories, alerts, scripts, and evidence files. The ability to quickly find a relevant line in a large file is a basic but powerful skill.

A simple command such as `grep` can help identify usernames, IP addresses, errors, suspicious strings, authentication events, process names, file paths, and indicators of compromise.

## 13. Real-World Connection

This concept appears in nearly every technical security workflow. Analysts may use `grep` to search web server logs for an IP address, authentication logs for a username, configuration files for a setting, or forensic artifacts for a suspicious string.

The level is simple, but the habit is professional: use known clues to filter large data sources and focus on relevant evidence.

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
    <td>Why is <code>grep</code> better than manually reading the entire file?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What does <code>grep millionth data.txt</code> do?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What could cause <code>grep</code> to return no results?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>How can you tell whether you are working in your local WSL shell or the remote Bandit shell?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>How does this level connect to log analysis or incident response?</td>
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
    <td>OverTheWire Bandit Level 7 to Level 8</td>
    <td>Provides the official level goal and command suggestions for this exercise.</td>
  </tr>
  <tr>
    <td><code>man ssh</code></td>
    <td>Explains SSH syntax, remote login behavior, authentication, and the use of a non-default port with <code>-p</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>man grep</code></td>
    <td>Explains how <code>grep</code> searches files for matching lines and supports pattern matching options.<br><br></td>
  </tr>
  <tr>
    <td><code>man cat</code></td>
    <td>Explains how <code>cat</code> reads files and writes content to standard output.<br><br></td>
  </tr>
</table>
