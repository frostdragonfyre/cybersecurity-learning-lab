# Bandit Level 11 to Level 12

In this level, you will learn how to decode text that has been transformed with ROT13.

The password for the next level is stored in `data.txt`, but the letters have been rotated by 13 positions. Your job is to recognize the transformation and reverse it using a command-line tool.

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
    <td>Bandit Level 11 to Level 12<br><br></td>
  </tr>
  <tr>
    <td>Category</td>
    <td>Linux fundamentals, SSH, text transformation, ROT13, substitution ciphers, command-line decoding<br><br></td>
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

By the end of this level, you should understand how ROT13 transforms text, why ROT13 is not encryption in a meaningful security sense, and how to use `tr` to translate one set of characters into another.

<table>
  <tr>
    <th width="30%">Learning Layer</th>
    <th width="70%">Objective</th>
  </tr>
  <tr>
    <td>Beginner</td>
    <td>You will learn how to connect to the Bandit server from WSL, inspect a text file, and reverse a ROT13 transformation.<br><br></td>
  </tr>
  <tr>
    <td>Practitioner</td>
    <td>You will practice using <code>tr</code> to translate characters from one alphabet range to another and recover readable text from transformed input.<br><br></td>
  </tr>
  <tr>
    <td>Advanced</td>
    <td>You will connect this exercise to a broader security principle: simple transformations may obscure data, but they do not provide meaningful confidentiality. Analysts must distinguish encoding, transformation, obfuscation, and encryption.<br><br></td>
  </tr>
</table>

## 3. Level Summary

The official level goal says the password for the next level is stored in `data.txt`, where all lowercase and uppercase letters have been rotated by 13 positions.

That gives you two useful facts:

```text
The file to inspect: data.txt
The transformation needed: ROT13 character rotation
```

A useful command is:

```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

This command reads the file and translates each letter to the letter 13 positions away in the alphabet.

Official level reference:

```text
https://overthewire.org/wargames/bandit/bandit12.html
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
    <td>ROT13</td>
    <td>ROT13 is a simple letter substitution method where each letter is replaced by the letter 13 positions later in the alphabet. Because the English alphabet has 26 letters, applying ROT13 twice returns the original text.<br><br></td>
  </tr>
  <tr>
    <td>Character translation</td>
    <td>Character translation replaces characters from one set with corresponding characters from another set. In this level, <code>tr</code> maps original letters to their ROT13 equivalents.<br><br></td>
  </tr>
  <tr>
    <td><code>tr</code></td>
    <td><code>tr</code> reads input and translates, deletes, or squeezes characters. It is useful for simple text transformations.<br><br></td>
  </tr>
  <tr>
    <td>Transformation vs. encryption</td>
    <td>ROT13 transforms text, but it does not protect it. Anyone who knows the transformation can reverse it without a secret key.<br><br></td>
  </tr>
  <tr>
    <td>Pipeline</td>
    <td>A pipeline uses <code>|</code> to send the output of one command into another command. In this level, the output of <code>cat data.txt</code> becomes the input to <code>tr</code>.<br><br></td>
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
    <td>The text is readable but not meaningful at first.</td>
    <td>This suggests the data may be transformed rather than binary, compressed, or encrypted.<br><br></td>
  </tr>
  <tr>
    <td>The level says letters were rotated by 13 positions.</td>
    <td>This is the clue for ROT13. You need to rotate the letters back to recover the original text.<br><br></td>
  </tr>
  <tr>
    <td>ROT13 handles uppercase and lowercase letters separately.</td>
    <td>Your translation command should include both <code>A-Z</code> and <code>a-z</code> so it transforms all letters correctly.<br><br></td>
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
    <td>The file contains text, but the letters have been shifted. Think about how to translate one alphabet range into another.<br><br></td>
  </tr>
  <tr>
    <td>Hint 3</td>
    <td>ROT13 shifts letters by 13 positions. Because the alphabet has 26 letters, applying ROT13 again reverses the transformation.<br><br></td>
  </tr>
  <tr>
    <td>Hint 4</td>
    <td>Use <code>tr</code> to translate <code>A-Za-z</code> into the ROT13 alphabet order.<br><br></td>
  </tr>
</table>

## 7. Commands Introduced

These commands are not just things to memorize. Each one teaches you something about remote login, file inspection, text transformation, or command composition.

<table>
  <tr>
    <th width="30%">Command or Tool</th>
    <th width="70%">Explanation</th>
  </tr>
  <tr>
    <td><code>ssh bandit11@bandit.labs.overthewire.org -p 2220</code></td>
    <td>Connects from your local terminal to the remote OverTheWire Bandit server as user <code>bandit11</code> on port <code>2220</code>.<br><br></td>
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
    <td>Displays the transformed contents of the file. The output should look like text, but the letters are rotated.<br><br></td>
  </tr>
  <tr>
    <td><code>tr 'A-Za-z' 'N-ZA-Mn-za-m'</code></td>
    <td>Translates uppercase and lowercase letters into their ROT13 equivalents.<br><br></td>
  </tr>
  <tr>
    <td><code>cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'</code></td>
    <td>Reads the transformed file and pipes it into <code>tr</code> to recover the original readable text.<br><br></td>
  </tr>
  <tr>
    <td><code>ssh bandit12@bandit.labs.overthewire.org -p 2220</code></td>
    <td>Connects to the next Bandit account after you retrieve the decoded password.<br><br></td>
  </tr>
</table>

## 8. Walkthrough Without Credential Disclosure

This walkthrough assumes you are working from a local terminal, such as Windows Subsystem for Linux, macOS Terminal, or a Linux shell. The examples below use WSL because it gives Windows users a Linux-like command-line environment.

### Step 1

Open WSL and connect to the Bandit server as `bandit11`.

```bash
ssh bandit11@bandit.labs.overthewire.org -p 2220
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
    <td><code>bandit11</code></td>
    <td>The username for this level. Each Bandit level has its own user account, such as <code>bandit10</code>, <code>bandit11</code>, and <code>bandit12</code>.<br><br></td>
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

Look at the transformed file content.

```bash
cat data.txt
```

The output should look like readable text, but the words may not make sense because the letters have been rotated.

### Step 5

Apply the ROT13 translation.

```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

The `cat` command sends the file content into the pipeline. The `tr` command translates each uppercase and lowercase letter by 13 positions.

The output is the password for the next Bandit level. Do not commit that password to GitHub.

### Step 6

Use the discovered password to log in to the next level.

```bash
ssh bandit12@bandit.labs.overthewire.org -p 2220
```

When prompted, enter the decoded password. Again, the terminal may not show characters while the password is typed. That is normal behavior.

At this point, you have moved from `bandit11` to `bandit12`.

## 9. Command Output and Screenshots

Use this section to include terminal output or screenshots after redacting credentials.

### Relevant Command Output

```text
$ ssh bandit11@bandit.labs.overthewire.org -p 2220
bandit11@bandit.labs.overthewire.org's password:
[successful login output omitted]

$ pwd
/home/bandit11

$ ls
data.txt

$ cat data.txt
[ROT13-TRANSFORMED TEXT REDACTED OR TRUNCATED]

$ cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
[REDACTED PASSWORD]
```

This output shows the central lesson. The file contains text transformed with ROT13, and `tr` translates the letters back into readable form.

### Screenshots

<img width="867" height="212" alt="image" src="https://github.com/user-attachments/assets/6edfe69e-cd04-4614-a5eb-91a4214c2dc6" />

<img width="867" height="212" alt="image" src="https://github.com/user-attachments/assets/315864d0-ff04-4e83-8360-6ee24183c07f" />


## 10. What Is Really Happening

In this level, you are learning how a simple substitution transformation changes text.

ROT13 replaces each letter with the letter 13 positions later in the alphabet. For example, `A` becomes `N`, `B` becomes `O`, and so on. Because the alphabet has 26 letters, applying the same ROT13 transformation again reverses the result.

The `tr` command performs character translation. It reads input and replaces characters from the first set with the corresponding characters from the second set.

When you run:

```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

you are asking the system:

```text
Read data.txt, then translate uppercase and lowercase letters through the ROT13 mapping.
```

The uppercase mapping is:

```text
A-Z becomes N-ZA-M
```

The lowercase mapping is:

```text
a-z becomes n-za-m
```

This level teaches an important distinction: ROT13 is a transformation, not meaningful protection. It hides text from casual reading, but it does not secure the text.

## 11. Common Mistakes

<table>
  <tr>
    <th width="35%">Mistake</th>
    <th width="65%">Correction</th>
  </tr>
  <tr>
    <td>Assuming ROT13 is encryption.</td>
    <td>ROT13 is a simple substitution transformation. It does not require a secret key and should not be used to protect sensitive data.<br><br></td>
  </tr>
  <tr>
    <td>Only translating lowercase letters.</td>
    <td>The level says lowercase and uppercase letters are rotated. Include both <code>A-Z</code> and <code>a-z</code> in the translation.<br><br></td>
  </tr>
  <tr>
    <td>Forgetting the pipe.</td>
    <td>The pipe sends the output of <code>cat data.txt</code> into <code>tr</code>. Without input, <code>tr</code> may wait for you to type text manually.<br><br></td>
  </tr>
  <tr>
    <td>Mixing up the translation ranges.</td>
    <td>The target range should represent the alphabet shifted by 13 positions: <code>N-ZA-Mn-za-m</code>.<br><br></td>
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

This level shows why obfuscation should not be mistaken for security.

Simple transformations can make data less readable, but they do not provide meaningful confidentiality. In real systems, sensitive data should not be protected with reversible transformations that require no secret key.

For defenders, this is also a useful analysis lesson. Suspicious scripts, logs, malware, or configuration files may contain transformed strings. Analysts need to recognize when text has been encoded, transformed, compressed, or encrypted and choose the right method to interpret it.

## 13. Real-World Connection

ROT13 itself is simple, but the broader concept appears often in cybersecurity. Attackers and malware authors may use simple transformations or encodings to hide strings from casual inspection. Developers may accidentally treat encoded or transformed values as if they were protected secrets.

Security analysts often need to reverse simple transformations during malware analysis, incident response, log review, and forensic triage. The important skill is recognizing that the data has been transformed and selecting the right tool to reverse it.

The level is simple, but the habit is professional: identify how data has been transformed before deciding what it means.

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
    <td>What does ROT13 do to letters?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>Why does applying ROT13 again recover the original text?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What does <code>tr 'A-Za-z' 'N-ZA-Mn-za-m'</code> do?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>Why is ROT13 not meaningful encryption?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>How does this level connect to malware analysis or incident response?</td>
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
    <td>OverTheWire Bandit Level 11 to Level 12</td>
    <td>Provides the official level goal and command suggestions for this exercise.</td>
  </tr>
  <tr>
    <td><code>man ssh</code></td>
    <td>Explains SSH syntax, remote login behavior, authentication, and the use of a non-default port with <code>-p</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>man tr</code></td>
    <td>Explains how <code>tr</code> translates, deletes, or squeezes characters from input.<br><br></td>
  </tr>
  <tr>
    <td><code>man cat</code></td>
    <td>Explains how <code>cat</code> reads files and writes content to standard output.<br><br></td>
  </tr>
  <tr>
    <td><code>man bash</code></td>
    <td>Provides background on pipelines, standard input, and standard output.<br><br></td>
  </tr>
</table>
