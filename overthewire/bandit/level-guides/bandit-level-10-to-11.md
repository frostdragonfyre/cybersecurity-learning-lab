# Bandit Level 10 to Level 11

In this level, you will learn how to decode Base64-encoded data.

The password for the next level is stored in `data.txt`, but it is not written as plain text. It has been Base64 encoded. Your job is to recognize that the file contains encoded text, decode it, and retrieve the password.

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
    <td>Bandit Level 10 to Level 11<br><br></td>
  </tr>
  <tr>
    <td>Category</td>
    <td>Linux fundamentals, SSH, encoding, Base64, command-line decoding, data representation<br><br></td>
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

By the end of this level, you should understand what Base64 encoding is, why encoded text is not the same thing as encryption, and how to decode Base64 data from the Linux command line.

<table>
  <tr>
    <th width="30%">Learning Layer</th>
    <th width="70%">Objective</th>
  </tr>
  <tr>
    <td>Beginner</td>
    <td>You will learn how to connect to the Bandit server from WSL, inspect a file, and decode Base64-encoded text.<br><br></td>
  </tr>
  <tr>
    <td>Practitioner</td>
    <td>You will practice recognizing encoded data and using <code>base64 -d</code> to convert it back into readable text.<br><br></td>
  </tr>
  <tr>
    <td>Advanced</td>
    <td>You will connect this exercise to a broader security principle: encoding changes representation, but it does not provide confidentiality. Encoded data should not be treated as protected data.<br><br></td>
  </tr>
</table>

## 3. Level Summary

The official level goal says the password for the next level is stored in `data.txt`, which contains Base64-encoded data.

That gives you two useful facts:

```text
The file to inspect: data.txt
The transformation needed: Base64 decoding
```

A useful command is:

```bash
base64 -d data.txt
```

The `-d` option tells `base64` to decode the input.

Official level reference:

```text
https://overthewire.org/wargames/bandit/bandit11.html
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
    <td>Encoding</td>
    <td>Encoding changes how data is represented. It is used to make data easier to store, transmit, or handle in systems that expect certain character formats.<br><br></td>
  </tr>
  <tr>
    <td>Base64</td>
    <td>Base64 is an encoding scheme that represents binary or text data using printable characters. Base64 output often contains letters, numbers, plus signs, slashes, and equals signs used as padding.<br><br></td>
  </tr>
  <tr>
    <td>Decoding</td>
    <td>Decoding reverses an encoding process. In this level, decoding Base64 converts the encoded content back into readable text.<br><br></td>
  </tr>
  <tr>
    <td>Encoding vs. encryption</td>
    <td>Encoding is not encryption. Encoded data can be decoded by anyone who knows the encoding scheme. Encryption is intended to protect confidentiality and requires a key to reverse.<br><br></td>
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
    <td>The content is Base64 encoded.</td>
    <td>The file may look like readable characters, but the meaning is hidden by representation. You need to decode it.<br><br></td>
  </tr>
  <tr>
    <td>Base64 output often has a recognizable character pattern.</td>
    <td>Base64 commonly uses letters, numbers, plus signs, slashes, and sometimes equals signs for padding.<br><br></td>
  </tr>
  <tr>
    <td>Decoding reveals the original readable content.</td>
    <td>Once the content is decoded, the password becomes readable in the terminal.<br><br></td>
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
    <td>The level tells you the file is Base64 encoded. Think about a command that can decode Base64 data.<br><br></td>
  </tr>
  <tr>
    <td>Hint 3</td>
    <td>Use the decode option for the <code>base64</code> command.<br><br></td>
  </tr>
  <tr>
    <td>Hint 4</td>
    <td>Decode <code>data.txt</code> directly from the command line.<br><br></td>
  </tr>
</table>

## 7. Commands Introduced

These commands are not just things to memorize. Each one teaches you something about remote login, file inspection, data representation, or decoding.

<table>
  <tr>
    <th width="30%">Command or Tool</th>
    <th width="70%">Explanation</th>
  </tr>
  <tr>
    <td><code>ssh bandit10@bandit.labs.overthewire.org -p 2220</code></td>
    <td>Connects from your local terminal to the remote OverTheWire Bandit server as user <code>bandit10</code> on port <code>2220</code>.<br><br></td>
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
    <td>Displays the encoded contents of the file. This helps you observe that the file contains encoded text rather than the final password directly.<br><br></td>
  </tr>
  <tr>
    <td><code>base64 -d data.txt</code></td>
    <td>Decodes the Base64-encoded content in <code>data.txt</code> and prints the decoded result to the terminal.<br><br></td>
  </tr>
  <tr>
    <td><code>ssh bandit11@bandit.labs.overthewire.org -p 2220</code></td>
    <td>Connects to the next Bandit account after you retrieve the decoded password.<br><br></td>
  </tr>
</table>

## 8. Walkthrough Without Credential Disclosure

This walkthrough assumes you are working from a local terminal, such as Windows Subsystem for Linux, macOS Terminal, or a Linux shell. The examples below use WSL because it gives Windows users a Linux-like command-line environment.

### Step 1

Open WSL and connect to the Bandit server as `bandit10`.

```bash
ssh bandit10@bandit.labs.overthewire.org -p 2220
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
    <td><code>bandit10</code></td>
    <td>The username for this level. Each Bandit level has its own user account, such as <code>bandit9</code>, <code>bandit10</code>, and <code>bandit11</code>.<br><br></td>
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

Look at the encoded file content.

```bash
cat data.txt
```

You should see text that looks encoded. It may contain letters, numbers, and possibly equals signs. This is not the final password yet. It is the encoded representation of the data.

### Step 5

Decode the Base64 content.

```bash
base64 -d data.txt
```

The `-d` option tells `base64` to decode the file instead of encoding it.

The output is the password for the next Bandit level. Do not commit that password to GitHub.

### Step 6

Use the discovered password to log in to the next level.

```bash
ssh bandit11@bandit.labs.overthewire.org -p 2220
```

When prompted, enter the decoded password. Again, the terminal may not show characters while the password is typed. That is normal behavior.

At this point, you have moved from `bandit10` to `bandit11`.

## 9. Command Output and Screenshots

Use this section to include terminal output or screenshots after redacting credentials.

### Relevant Command Output

```text
$ ssh bandit10@bandit.labs.overthewire.org -p 2220
bandit10@bandit.labs.overthewire.org's password:
[successful login output omitted]

$ pwd
/home/bandit10

$ ls
data.txt

$ cat data.txt
[BASE64-ENCODED DATA REDACTED OR TRUNCATED]

$ base64 -d data.txt
[REDACTED PASSWORD]
```

This output shows the central lesson. The file contains encoded data, and `base64 -d` decodes it into the readable password.

### Screenshots

<img width="865" height="321" alt="image" src="https://github.com/user-attachments/assets/e0579f95-5170-41b3-8b78-6006e29125a4" />

<img width="867" height="212" alt="image" src="https://github.com/user-attachments/assets/f595b596-57a2-498d-8be1-c5b961db9ae9" />

## 10. What Is Really Happening

In this level, you are learning that encoded data is not the same thing as encrypted data.

Base64 changes how data is represented. It is commonly used when data needs to be stored or transmitted using printable characters. For example, binary data or structured data may be encoded so it can safely pass through systems that expect text.

When you run:

```bash
base64 -d data.txt
```

you are asking the system:

```text
Decode the Base64 content in data.txt and print the decoded result.
```

The important lesson is that Base64 does not protect secrets. Anyone who recognizes Base64 can decode it. It is a representation format, not a security control.

This level teaches a professional habit: when data looks unreadable or transformed, ask whether it is encoded, compressed, encrypted, or otherwise represented differently.

## 11. Common Mistakes

<table>
  <tr>
    <th width="35%">Mistake</th>
    <th width="65%">Correction</th>
  </tr>
  <tr>
    <td>Assuming Base64 is encryption.</td>
    <td>Base64 is encoding, not encryption. It can be reversed without a key using a decoder.<br><br></td>
  </tr>
  <tr>
    <td>Using <code>cat data.txt</code> and expecting the final password immediately.</td>
    <td><code>cat</code> shows the encoded data. You still need to decode it with <code>base64 -d</code>.<br><br></td>
  </tr>
  <tr>
    <td>Forgetting the decode option.</td>
    <td>Use <code>-d</code> to decode. Without the decode option, <code>base64</code> may encode input instead of decoding it.<br><br></td>
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

This level shows why encoding should not be mistaken for security.

In real systems, sensitive values are sometimes Base64 encoded in configuration files, tokens, logs, HTTP headers, scripts, or environment variables. Encoding may make the value look less obvious, but it does not protect the value from someone who can access it.

Defenders should treat encoded secrets as exposed secrets if they are stored or transmitted without proper protection. Proper protection requires access control, encryption where appropriate, secret management, rotation, and monitoring.

## 13. Real-World Connection

Base64 appears frequently in cybersecurity and system administration. It is commonly seen in web tokens, API data, email attachments, certificates, malware payloads, command-and-control traffic, encoded scripts, and configuration files.

Security analysts often decode Base64 during incident response, malware analysis, log review, and forensic triage. The important question is not only “Can I decode this?” but also “Why was this data encoded, where did it come from, and does it expose anything sensitive?”

The level is simple, but the habit is professional: identify the transformation applied to data, reverse it when appropriate, and understand the security implications.

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
    <td>What does Base64 encoding do?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>Why is Base64 not the same thing as encryption?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What does <code>base64 -d data.txt</code> do?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>Where might Base64 appear in real cybersecurity work?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>How should defenders treat encoded secrets?</td>
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
    <td>OverTheWire Bandit Level 10 to Level 11</td>
    <td>Provides the official level goal and command suggestions for this exercise.</td>
  </tr>
  <tr>
    <td><code>man ssh</code></td>
    <td>Explains SSH syntax, remote login behavior, authentication, and the use of a non-default port with <code>-p</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>man base64</code></td>
    <td>Explains how the <code>base64</code> command encodes and decodes Base64 data.<br><br></td>
  </tr>
  <tr>
    <td><code>man cat</code></td>
    <td>Explains how <code>cat</code> reads files and writes content to standard output.<br><br></td>
  </tr>
</table>
