# Bandit Level 8 to Level 9

In this level, you will learn how to find the only unique line in a file that contains many repeated lines.

The password for the next level is stored in `data.txt`. The correct line is the only line that occurs exactly once. Your job is to sort the file, identify the unique line, and avoid manually scanning through a large amount of text.

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
    <td>Bandit Level 8 to Level 9<br><br></td>
  </tr>
  <tr>
    <td>Category</td>
    <td>Linux fundamentals, SSH, text processing, sorting, uniqueness, pipelines<br><br></td>
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

By the end of this level, you should understand how to combine simple Linux commands with a pipeline to solve a text-processing problem. You should also understand why sorting is important before using `uniq`.

<table>
  <tr>
    <th width="30%">Learning Layer</th>
    <th width="70%">Objective</th>
  </tr>
  <tr>
    <td>Beginner</td>
    <td>You will learn how to connect to the Bandit server from WSL and find the only unique line in a text file.<br><br></td>
  </tr>
  <tr>
    <td>Practitioner</td>
    <td>You will practice using <code>sort</code>, <code>uniq</code>, and a pipeline to transform file content into useful evidence.<br><br></td>
  </tr>
  <tr>
    <td>Advanced</td>
    <td>You will connect this exercise to a broader data analysis and security principle: useful signals are often hidden inside noisy data, and command-line tools can reduce that noise efficiently.<br><br></td>
  </tr>
</table>

## 3. Level Summary

The official level goal says the password for the next level is stored in `data.txt` and is the only line of text that occurs once.

That gives you two useful facts:

```text
The file to inspect: data.txt
The property to find: the only line that appears once
```

A useful command is:

```bash
sort data.txt | uniq -u
```

This command sorts the file first, then shows only lines that are unique.

Official level reference:

```text
https://overthewire.org/wargames/bandit/bandit9.html
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
    <td>Sorting</td>
    <td><code>sort</code> rearranges lines of text into order. Sorting matters because <code>uniq</code> works by comparing adjacent lines.<br><br></td>
  </tr>
  <tr>
    <td>Uniqueness</td>
    <td>A unique line is a line that appears only once. In this level, the password is the only line in the file that is not repeated.<br><br></td>
  </tr>
  <tr>
    <td><code>uniq</code></td>
    <td><code>uniq</code> filters adjacent matching lines. With the <code>-u</code> option, it prints only lines that are unique.<br><br></td>
  </tr>
  <tr>
    <td>Pipeline</td>
    <td>A pipeline uses <code>|</code> to send the output of one command into another command. In this level, the output of <code>sort</code> becomes the input to <code>uniq -u</code>.<br><br></td>
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
    <td>The password is the only line that occurs once.</td>
    <td>This is not a keyword search problem. It is a frequency problem. You need to identify which line is unique.<br><br></td>
  </tr>
  <tr>
    <td><code>uniq</code> compares adjacent lines.</td>
    <td>This is why sorting comes first. If duplicate lines are not next to each other, <code>uniq</code> may not identify them correctly.<br><br></td>
  </tr>
  <tr>
    <td>The pipe connects the two steps.</td>
    <td>The sorted output is passed directly into <code>uniq -u</code>, so you do not need to create a temporary file.<br><br></td>
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
    <td>The level is asking for a line that occurs once. Think about commands that help with repeated lines.<br><br></td>
  </tr>
  <tr>
    <td>Hint 3</td>
    <td>Before using <code>uniq</code>, think about whether duplicate lines need to be next to each other.<br><br></td>
  </tr>
  <tr>
    <td>Hint 4</td>
    <td>Sort the file first, then show only unique lines.<br><br></td>
  </tr>
</table>

## 7. Commands Introduced

These commands are not just things to memorize. Each one teaches you something about remote login, text processing, or command composition.

<table>
  <tr>
    <th width="30%">Command or Tool</th>
    <th width="70%">Explanation</th>
  </tr>
  <tr>
    <td><code>ssh bandit8@bandit.labs.overthewire.org -p 2220</code></td>
    <td>Connects from your local terminal to the remote OverTheWire Bandit server as user <code>bandit8</code> on port <code>2220</code>.<br><br></td>
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
    <td><code>sort data.txt</code></td>
    <td>Sorts the lines in <code>data.txt</code> so repeated lines appear next to each other.<br><br></td>
  </tr>
  <tr>
    <td><code>uniq -u</code></td>
    <td>Prints only lines that are unique among adjacent lines. This is why sorted input matters.<br><br></td>
  </tr>
  <tr>
    <td><code>sort data.txt | uniq -u</code></td>
    <td>Sorts the file and then prints only the line that occurs once.<br><br></td>
  </tr>
  <tr>
    <td><code>ssh bandit9@bandit.labs.overthewire.org -p 2220</code></td>
    <td>Connects to the next Bandit account after you retrieve the password from the unique line.<br><br></td>
  </tr>
</table>

## 8. Walkthrough Without Credential Disclosure

This walkthrough assumes you are working from a local terminal, such as Windows Subsystem for Linux, macOS Terminal, or a Linux shell. The examples below use WSL because it gives Windows users a Linux-like command-line environment.

### Step 1

Open WSL and connect to the Bandit server as `bandit8`.

```bash
ssh bandit8@bandit.labs.overthewire.org -p 2220
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
    <td><code>bandit8</code></td>
    <td>The username for this level. Each Bandit level has its own user account, such as <code>bandit7</code>, <code>bandit8</code>, and <code>bandit9</code>.<br><br></td>
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

Sort the file and return only the unique line.

```bash
sort data.txt | uniq -u
```

This command has two parts. First, `sort data.txt` orders the lines so duplicates are grouped together. Then `uniq -u` prints only the line that appears once.

The output is the password for the next Bandit level. Do not commit that password to GitHub.

### Step 5

Use the discovered password to log in to the next level.

```bash
ssh bandit9@bandit.labs.overthewire.org -p 2220
```

When prompted, enter the password you found from the unique line. Again, the terminal may not show characters while the password is typed. That is normal behavior.

At this point, you have moved from `bandit8` to `bandit9`.

## 9. Command Output and Screenshots

Use this section to include terminal output or screenshots after redacting credentials.

### Relevant Command Output

```text
$ ssh bandit8@bandit.labs.overthewire.org -p 2220
bandit8@bandit.labs.overthewire.org's password:
[successful login output omitted]

$ pwd
/home/bandit8

$ ls
data.txt

$ sort data.txt | uniq -u
[REDACTED PASSWORD]
```

This output shows the central lesson. Sorting groups repeated lines together, and `uniq -u` prints only the line that occurs once.

### Screenshots

<img width="867" height="323" alt="image" src="https://github.com/user-attachments/assets/5f5ba908-cd05-4fef-9e90-5fcf20d4825c" />

<img width="816" height="323" alt="image" src="https://github.com/user-attachments/assets/74cb6fbe-aea6-4a10-8d79-3b272fa4143c" />

## 10. What Is Really Happening

In this level, you are learning how to combine commands to solve a text-processing problem.

The file contains many repeated lines and one line that appears only once. If you try to inspect the file manually, you may waste time and miss the important line. Instead, you can transform the data so the unique line becomes easy to see.

The `sort` command groups identical lines together by ordering the file. This matters because `uniq` only compares neighboring lines. If duplicate lines are scattered throughout the file, `uniq` may not treat them as duplicates unless the file is sorted first.

The pipe symbol `|` sends the output of one command into the next command. In this case, the sorted lines become the input to `uniq -u`.

When you run:

```bash
sort data.txt | uniq -u
```

you are asking the system:

```text
Sort the lines in data.txt, then show me only the line that occurs once.
```

This level teaches a professional habit: combine small tools to answer a precise question.

## 11. Common Mistakes

<table>
  <tr>
    <th width="35%">Mistake</th>
    <th width="65%">Correction</th>
  </tr>
  <tr>
    <td>Running <code>uniq -u data.txt</code> without sorting first.</td>
    <td><code>uniq</code> only compares adjacent lines. Sort the file first so repeated lines are grouped together.<br><br></td>
  </tr>
  <tr>
    <td>Trying to manually read the entire file.</td>
    <td>Manual reading is inefficient and error-prone. Use text-processing tools when the file is large or repetitive.<br><br></td>
  </tr>
  <tr>
    <td>Not understanding the pipe.</td>
    <td>The pipe sends the output of <code>sort data.txt</code> into <code>uniq -u</code>. The second command works on the output of the first command.<br><br></td>
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

This level shows why command-line text processing matters in cybersecurity and system administration.

Security work often involves large files with repeated information: logs, alerts, process lists, network events, authentication records, and file inventories. The important signal may be the unusual entry, the rare value, or the line that does not appear like the others.

Tools such as `sort` and `uniq` help analysts reduce noise and identify what stands out.

## 13. Real-World Connection

This concept appears in log analysis, incident response, threat hunting, and data cleanup. Analysts often need to find rare events, unique indicators, uncommon usernames, unusual IP addresses, or one-off errors inside large datasets.

For example, you might sort and count log entries to identify repeated failures, rare source IPs, unique user agents, or uncommon command executions.

The level is simple, but the habit is professional: use pipelines to turn raw text into meaningful evidence.

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
    <td>Why does the file need to be sorted before using <code>uniq -u</code>?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What does the pipe symbol <code>|</code> do?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What does <code>uniq -u</code> print?</td>
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
    <td>OverTheWire Bandit Level 8 to Level 9</td>
    <td>Provides the official level goal and command suggestions for this exercise.</td>
  </tr>
  <tr>
    <td><code>man ssh</code></td>
    <td>Explains SSH syntax, remote login behavior, authentication, and the use of a non-default port with <code>-p</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>man sort</code></td>
    <td>Explains how <code>sort</code> orders lines of text and supports different sorting options.<br><br></td>
  </tr>
  <tr>
    <td><code>man uniq</code></td>
    <td>Explains how <code>uniq</code> filters adjacent matching lines and how <code>-u</code> prints unique lines.<br><br></td>
  </tr>
  <tr>
    <td><code>man bash</code></td>
    <td>Provides background on pipelines, standard input, and standard output.<br><br></td>
  </tr>
</table>
