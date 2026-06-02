# Bandit Level 12 to Level 13

In this level, you will learn how to work through a file that has been transformed several times.

The password for the next level is stored in `data.txt`, but the file is not directly readable. It is a hexdump of a file that has been repeatedly compressed and archived. Your job is to create a safe working directory, reverse the hexdump, identify each file type, decompress or extract each layer, and continue until the password is revealed.

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
    <td>Bandit Level 12 to Level 13<br><br></td>
  </tr>
  <tr>
    <td>Category</td>
    <td>Linux fundamentals, SSH, hexdump reversal, file identification, compression, archive extraction, temporary workspace management<br><br></td>
  </tr>
  <tr>
    <td>Difficulty</td>
    <td>Intermediate<br><br></td>
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

By the end of this level, you should understand how to reverse a hexdump, identify file types with `file`, and handle multiple layers of compression and archiving. You should also understand why creating a temporary working directory is safer than modifying files directly in the home directory.

<table>
  <tr>
    <th width="30%">Learning Layer</th>
    <th width="70%">Objective</th>
  </tr>
  <tr>
    <td>Beginner</td>
    <td>You will learn how to create a temporary workspace, copy a file, inspect file types, and use common decompression tools.<br><br></td>
  </tr>
  <tr>
    <td>Practitioner</td>
    <td>You will practice an iterative investigation workflow: identify the current file type, apply the correct extraction or decompression command, then inspect the next output file.<br><br></td>
  </tr>
  <tr>
    <td>Advanced</td>
    <td>You will connect this exercise to a broader security principle: real investigation often involves layered transformations, and analysts must verify each layer rather than assume what a file is based on its name.<br><br></td>
  </tr>
</table>

## 3. Level Summary

The official level goal says the password for the next level is stored in `data.txt`, which is a hexdump of a file that has been repeatedly compressed.

That gives you several useful facts:

```text
The file to inspect: data.txt
The first transformation to reverse: hexdump
The next task: repeatedly identify and unpack compressed or archived data
```

A typical workflow is:

```bash
cd "$(mktemp -d)"
cp ~/data.txt .
xxd -r data.txt > data
file data
```

From there, you use `file` to identify the current file type, then use the appropriate tool to decompress or extract it. Common tools in this level include:

```text
xxd
file
gzip
gunzip
bzip2
bunzip2
tar
cat
```

Official level reference:

```text
https://overthewire.org/wargames/bandit/bandit13.html
```

## 4. Concepts Introduced

<table>
  <tr>
    <th width="30%">Concept</th>
    <th width="70%">Explanation</th>
  </tr>
  <tr>
    <td>Temporary workspace</td>
    <td>A temporary workspace is a safe directory where you can copy files, rename them, decompress them, extract archives, and create intermediate outputs without cluttering the original home directory.<br><br></td>
  </tr>
  <tr>
    <td><code>mktemp -d</code></td>
    <td><code>mktemp -d</code> creates a uniquely named temporary directory. This is useful on shared systems because it avoids name collisions with other users.<br><br></td>
  </tr>
  <tr>
    <td>Command substitution</td>
    <td>Command substitution runs a command and substitutes its output into another command. In <code>cd "$(mktemp -d)"</code>, Bash creates a temporary directory first, then changes into that directory.<br><br></td>
  </tr>
  <tr>
    <td>Hexdump</td>
    <td>A hexdump represents file bytes as hexadecimal text. It is useful for viewing binary data, but it must be reversed before the original binary file can be processed normally.<br><br></td>
  </tr>
  <tr>
    <td><code>xxd -r</code></td>
    <td><code>xxd -r</code> reverses a hexdump back into the original binary data. In this level, it converts <code>data.txt</code> into a file that can be inspected with <code>file</code>.<br><br></td>
  </tr>
  <tr>
    <td>File type inspection</td>
    <td>The <code>file</code> command examines a file’s contents and reports what kind of data it appears to contain. This is more reliable than trusting the filename.<br><br></td>
  </tr>
  <tr>
    <td>Compression</td>
    <td>Compression reduces file size by representing data more efficiently. Common compression formats in this level include gzip and bzip2.<br><br></td>
  </tr>
  <tr>
    <td>Archive</td>
    <td>An archive stores one or more files together. A tar archive may not be compressed by itself, but it often appears together with compression formats.<br><br></td>
  </tr>
  <tr>
    <td>Iterative analysis</td>
    <td>Iterative analysis means repeating a cycle: inspect the file, identify what it is, apply the correct tool, and inspect the next result.<br><br></td>
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
    <td>The level recommends working under <code>/tmp</code>.</td>
    <td>You will create several intermediate files. A temporary directory keeps your work organized and avoids modifying the original file in your home directory.<br><br></td>
  </tr>
  <tr>
    <td>The original <code>data.txt</code> is a hexdump.</td>
    <td>You cannot simply decompress the hexdump text. You must first reverse it back into binary data with <code>xxd -r</code>.<br><br></td>
  </tr>
  <tr>
    <td>The output file type changes after each step.</td>
    <td>This is a layered problem. Each decompression or extraction reveals a new file that must be inspected again.<br><br></td>
  </tr>
  <tr>
    <td>File extensions may be missing or misleading.</td>
    <td>You should rely on <code>file</code> rather than guessing from filenames.<br><br></td>
  </tr>
  <tr>
    <td>Different file types require different tools.</td>
    <td>Gzip, bzip2, and tar each require different commands. The correct command depends on the current file type.<br><br></td>
  </tr>
  <tr>
    <td>Renaming a file does not change its contents.</td>
    <td>Renaming <code>data</code> to <code>data.gz</code>, <code>data.bz2</code>, or <code>data.tar</code> only changes the filename. The actual file type is determined by the file contents.<br><br></td>
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
    <td>Do not work directly in the home directory. Create a temporary directory under <code>/tmp</code> and copy <code>data.txt</code> there.<br><br></td>
  </tr>
  <tr>
    <td>Hint 2</td>
    <td>The first transformation is a hexdump. Reverse it before trying to decompress anything.<br><br></td>
  </tr>
  <tr>
    <td>Hint 3</td>
    <td>After each step, run <code>file</code> on the new output to decide what to do next.<br><br></td>
  </tr>
  <tr>
    <td>Hint 4</td>
    <td>If <code>file</code> reports gzip data, use gzip or gunzip. If it reports bzip2 data, use bzip2 or bunzip2. If it reports a tar archive, use tar.<br><br></td>
  </tr>
  <tr>
    <td>Hint 5</td>
    <td>Keep old layers organized by moving them into an <code>archive</code> folder once you no longer need them.<br><br></td>
  </tr>
</table>

## 7. Commands Introduced

These commands are not just things to memorize. Each one teaches you something about workspace management, file identification, or layered extraction.

<table>
  <tr>
    <th width="30%">Command or Tool</th>
    <th width="70%">Explanation</th>
  </tr>
  <tr>
    <td><code>ssh bandit12@bandit.labs.overthewire.org -p 2220</code></td>
    <td>Connects from your local terminal to the remote OverTheWire Bandit server as user <code>bandit12</code> on port <code>2220</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>cd "$(mktemp -d)"</code></td>
    <td>Creates a uniquely named temporary directory and changes into it. The <code>$(...)</code> syntax runs the command inside the parentheses first and substitutes its output.<br><br></td>
  </tr>
  <tr>
    <td><code>cp ~/data.txt .</code></td>
    <td>Copies the original file from the Bandit home directory into the current temporary workspace.<br><br></td>
  </tr>
  <tr>
    <td><code>xxd -r data.txt &gt; data</code></td>
    <td>Reverses the hexdump in <code>data.txt</code> and writes the binary output to a new file named <code>data</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>file data</code></td>
    <td>Identifies the apparent file type based on content, not just filename.<br><br></td>
  </tr>
  <tr>
    <td><code>mv data data.gz</code></td>
    <td>Renames a file so gzip tools recognize the expected extension. The rename does not change the file contents.<br><br></td>
  </tr>
  <tr>
    <td><code>gzip -d data.gz</code></td>
    <td>Decompresses a gzip-compressed file.<br><br></td>
  </tr>
  <tr>
    <td><code>gunzip data.gz</code></td>
    <td>Also decompresses a gzip-compressed file. It is the common shortcut command for gzip decompression.<br><br></td>
  </tr>
  <tr>
    <td><code>bzip2 -d data.bz2</code></td>
    <td>Decompresses a bzip2-compressed file.<br><br></td>
  </tr>
  <tr>
    <td><code>bunzip2 data.bz2</code></td>
    <td>Also decompresses a bzip2-compressed file. It is the bzip2 equivalent of <code>gunzip</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>tar -xf data.tar</code></td>
    <td>Extracts files from a tar archive.<br><br></td>
  </tr>
  <tr>
    <td><code>mkdir -p archive</code></td>
    <td>Creates an <code>archive</code> directory if it does not already exist. This is useful for moving old intermediate files out of the way.<br><br></td>
  </tr>
  <tr>
    <td><code>cat filename</code></td>
    <td>Displays the final readable file once the layered transformations have been reversed.<br><br></td>
  </tr>
</table>

## 8. Walkthrough Without Credential Disclosure

This walkthrough assumes you are working from a local terminal, such as Windows Subsystem for Linux, macOS Terminal, or a Linux shell. The examples below use WSL because it gives Windows users a Linux-like command-line environment.

### Step 1

Open WSL and connect to the Bandit server as `bandit12`.

```bash
ssh bandit12@bandit.labs.overthewire.org -p 2220
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
    <td><code>bandit12</code></td>
    <td>The username for this level. Each Bandit level has its own user account, such as <code>bandit11</code>, <code>bandit12</code>, and <code>bandit13</code>.<br><br></td>
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

Confirm your current working directory and locate the file.

```bash
pwd
ls
```

You should see that you are in `/home/bandit12` and that `data.txt` is present.

### Step 3

Create and enter a temporary working directory.

```bash
cd "$(mktemp -d)"
```

This command creates a unique temporary directory and immediately changes into it.

The syntax matters. The `$(mktemp -d)` portion runs `mktemp -d` first and substitutes the new temporary directory path into the `cd` command.

### Step 4

Copy the original file into your temporary workspace.

```bash
cp ~/data.txt .
ls
```

This copies `data.txt` from the Bandit home directory into your current temporary directory.

Working in `/tmp` is useful because this level creates several intermediate files. You do not want to clutter the home directory or accidentally overwrite the original file.

### Step 5

Look at the hexdump.

```bash
cat data.txt
```

You should see lines that look like hexadecimal byte offsets and hexadecimal values. This confirms that `data.txt` is a hexdump representation, not the original compressed file itself.

### Step 6

Reverse the hexdump into binary data.

```bash
xxd -r data.txt > data
file data
```

The `xxd -r` command reverses the hexdump and writes the reconstructed file to a new file named `data`.

Then `file data` identifies what kind of file you have recovered.

You should see that `data` is gzip-compressed data.

### Step 7

Rename and decompress the gzip layer.

```bash
mv data data.gz
gzip -d data.gz
ls
file data
```

The rename gives the file the `.gz` extension expected by gzip tools. The rename does not change the file contents; it only changes the filename.

After decompression, inspect the new `data` file with `file`.

You should see that the next layer is bzip2-compressed data.

### Step 8

Rename and decompress the bzip2 layer.

```bash
mv data data.bz2
bzip2 -d data.bz2
ls
file data
```

You could also use:

```bash
bunzip2 data.bz2
```

Both approaches decompress bzip2 data. In this step, `bzip2 -d` is used because it mirrors the earlier `gzip -d` pattern.

After decompression, inspect the new `data` file with `file`.

You should see that the next layer is gzip-compressed data.

### Step 9

Rename and decompress the next gzip layer.

```bash
mv data data.gz
gunzip data.gz
ls
file data
```

Here, `gunzip data.gz` is equivalent in purpose to `gzip -d data.gz`.

After decompression, inspect the new `data` file with `file`.

You should see that the next layer is a POSIX tar archive.

### Step 10

Rename and extract the tar archive.

```bash
mv data data.tar
tar -xf data.tar
ls
```

The `tar -xf` command extracts the contents of the tar archive.

You should see a new file, such as:

```text
data5.bin
```

### Step 11

Move old working files into an archive folder.

```bash
mkdir -p archive
mv data.t* archive/
ls
```

This step is not required to solve the level, but it is a good organizational habit. It moves the old `data.txt` and `data.tar` files out of the way so you can focus on the current file.

At this point, your active file should be:

```text
data5.bin
```

### Step 12

Inspect and extract the next tar archive.

```bash
file data5.bin
mv data5.bin data5.tar
tar -xf data5.tar
ls
```

You should see a new file, such as:

```text
data6.bin
```

Move the old tar file into the archive folder:

```bash
mv data5.tar archive/
```

### Step 13

Inspect and decompress the bzip2 layer.

```bash
file data6.bin
mv data6.bin data6.bz2
bunzip2 data6.bz2
ls
file data6
```

This time, `bunzip2` is used. It is the bzip2 equivalent of `gunzip`.

After decompression, inspect `data6` with `file`.

You should see that it is another POSIX tar archive.

### Step 14

Rename and extract the next tar archive.

```bash
mv data6 data6.tar
tar -xf data6.tar
ls
```

You should see a new file, such as:

```text
data8.bin
```

Move the old tar file into the archive folder:

```bash
mv data6.tar archive/
```

### Step 15

Inspect and decompress the final gzip layer.

```bash
file data8.bin
mv data8.bin data8.gz
gzip -d data8.gz
ls
file data8
```

You should see that `data8` is ASCII text.

That means the repeated decompression and extraction process is finished. The file is now readable text.

### Step 16

Rename and read the final text file.

```bash
mv data8 data8.txt
cat data8.txt
```

The output is the password for the next Bandit level. Do not commit that password to GitHub.

### Step 17

Use the discovered password to log in to the next level.

```bash
ssh bandit13@bandit.labs.overthewire.org -p 2220
```

When prompted, enter the password you found in the final text file. Again, the terminal may not show characters while the password is typed. That is normal behavior.

At this point, you have moved from `bandit12` to `bandit13`.

## 9. Command Output and Screenshots

Use this section to include terminal output or screenshots after redacting credentials.

### Relevant Command Output

```text
$ ssh bandit12@bandit.labs.overthewire.org -p 2220
bandit12@bandit.labs.overthewire.org's password:
[successful login output omitted]

$ pwd
/home/bandit12

$ ls
data.txt

$ cd "$(mktemp -d)"

$ cp ~/data.txt .
$ ls
data.txt

$ xxd -r data.txt > data
$ file data
data: gzip compressed data, was "data2.bin"

$ mv data data.gz
$ gzip -d data.gz
$ file data
data: bzip2 compressed data, block size = 900k

$ mv data data.bz2
$ bzip2 -d data.bz2
$ file data
data: gzip compressed data, was "data4.bin"

$ mv data data.gz
$ gunzip data.gz
$ file data
data: POSIX tar archive (GNU)

$ mv data data.tar
$ tar -xf data.tar
$ ls
data5.bin  data.tar  data.txt

$ mkdir -p archive
$ mv data.t* archive/
$ ls
archive  data5.bin

$ file data5.bin
data5.bin: POSIX tar archive (GNU)

$ mv data5.bin data5.tar
$ tar -xf data5.tar
$ ls
archive  data5.tar  data6.bin

$ mv data5.tar archive/

$ file data6.bin
data6.bin: bzip2 compressed data, block size = 900k

$ mv data6.bin data6.bz2
$ bunzip2 data6.bz2
$ file data6
data6: POSIX tar archive (GNU)

$ mv data6 data6.tar
$ tar -xf data6.tar
$ ls
archive  data6.tar  data8.bin

$ mv data6.tar archive/

$ file data8.bin
data8.bin: gzip compressed data, was "data9.bin"

$ mv data8.bin data8.gz
$ gzip -d data8.gz
$ file data8
data8: ASCII text

$ mv data8 data8.txt
$ cat data8.txt
The password is [REDACTED PASSWORD]
```

This output shows the central lesson. You reverse the hexdump first, then repeatedly identify the current file type, apply the correct decompression or extraction tool, and inspect the next layer.

### Screenshots

<img width="775" height="464" alt="image" src="https://github.com/user-attachments/assets/e92d7953-ddc5-4771-95b2-62980de92c25" />

<img width="775" height="464" alt="image" src="https://github.com/user-attachments/assets/446c789b-d3bc-42e8-a1f2-472f9444e8c5" />

<img width="775" height="716" alt="image" src="https://github.com/user-attachments/assets/fb00f64a-36d2-42d9-973e-c7fef0d7153a" />

<img width="775" height="357" alt="image" src="https://github.com/user-attachments/assets/360ccfaa-d266-46af-aff1-2a53f7b629f1" />

## 10. What Is Really Happening

In this level, you are working through several layers of data representation.

The original `data.txt` is not the compressed file itself. It is a hexdump of the compressed file. A hexdump is a text representation of bytes. Before decompression tools can work, you must reconstruct the original bytes with:

```bash
xxd -r data.txt > data
```

After that, the problem becomes an iterative file analysis task. The file may be gzip data, bzip2 data, a tar archive, or readable text. Each tool handles a different format.

The important habit is to avoid guessing. Run `file`, read the result, then apply the appropriate tool.

A good mental model is:

```text
Identify the current layer.
Apply the correct reverse operation.
Inspect the next layer.
Repeat until the file is readable text.
```

This is similar to real technical analysis. Files may be encoded, compressed, archived, packed, encrypted, or transformed more than once. Analysts must peel back each layer carefully.

## 11. Common Mistakes

<table>
  <tr>
    <th width="35%">Mistake</th>
    <th width="65%">Correction</th>
  </tr>
  <tr>
    <td>Typing <code>cd(mktemp -d)</code>, <code>cd (mktemp -d)</code>, or <code>cd{mktemp -d}</code>.</td>
    <td>Those are not valid Bash command substitution forms. Use <code>cd "$(mktemp -d)"</code> or use a two-step approach with <code>workdir="$(mktemp -d)"</code> followed by <code>cd "$workdir"</code>.<br><br></td>
  </tr>
  <tr>
    <td>Trying to decompress <code>data.txt</code> before reversing the hexdump.</td>
    <td>The file is a hexdump first. Use <code>xxd -r</code> to reconstruct the binary data before using decompression tools.<br><br></td>
  </tr>
  <tr>
    <td>Working directly in the home directory.</td>
    <td>This level creates several intermediate files. Use a temporary directory under <code>/tmp</code> to keep your work organized.<br><br></td>
  </tr>
  <tr>
    <td>Guessing the file type from the filename.</td>
    <td>Filenames may not include useful extensions. Use <code>file</code> to identify the content type.<br><br></td>
  </tr>
  <tr>
    <td>Using the wrong decompression tool.</td>
    <td>Use <code>gzip</code> or <code>gunzip</code> for gzip data, <code>bzip2</code> or <code>bunzip2</code> for bzip2 data, and <code>tar</code> for tar archives.<br><br></td>
  </tr>
  <tr>
    <td>Typing <code>bunzip</code> instead of <code>bunzip2</code>.</td>
    <td>The bzip2 decompression command is <code>bunzip2</code>. You can also use <code>bzip2 -d</code>.<br><br></td>
  </tr>
  <tr>
    <td>Losing track of intermediate files.</td>
    <td>Use clear names, run <code>ls</code> often, and check each file with <code>file</code> before continuing.<br><br></td>
  </tr>
  <tr>
    <td>Assuming renaming a file changes its type.</td>
    <td>Renaming a file only changes its name. The contents stay the same. Use <code>file</code> to verify what the file actually contains.<br><br></td>
  </tr>
  <tr>
    <td>Publishing the password in screenshots or notes.</td>
    <td>Credentials should be redacted from public writeups. The guide should teach the method without exposing active credential material.<br><br></td>
  </tr>
</table>

## 12. Defensive or Administrative Takeaway

This level shows why file identification and careful extraction matter in cybersecurity work.

During incident response, digital forensics, malware analysis, or system administration, files may be layered through encoding, compression, archiving, or obfuscation. A file may not be what its name suggests. A safe workflow is to inspect the file type, choose the appropriate tool, and avoid making assumptions.

The temporary workspace also matters. Analysts should avoid contaminating original evidence, overwriting important files, or losing track of intermediate artifacts. Even in a training lab, disciplined workspace management is a professional habit.

## 13. Real-World Connection

This concept appears in malware analysis, forensic triage, archive handling, log collection, and data recovery. Analysts often receive files that are compressed, archived, encoded, or transformed multiple times.

For example, a suspicious attachment might contain a compressed archive, which contains another archive, which contains a script, which contains encoded strings. Each layer must be identified and handled correctly.

The level is challenging because it requires patience, not because any single command is difficult. That is realistic. Many security investigations are solved by careful iteration.

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
    <td>Why do you reverse the hexdump before decompressing anything?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What does <code>file</code> tell you during this level?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>Why is a temporary working directory useful?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What is the difference between compression and archiving?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>Why does renaming a file not change its actual file type?</td>
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
    <td>OverTheWire Bandit Level 12 to Level 13</td>
    <td>Provides the official level goal and command suggestions for this exercise.</td>
  </tr>
  <tr>
    <td><code>man ssh</code></td>
    <td>Explains SSH syntax, remote login behavior, authentication, and the use of a non-default port with <code>-p</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>man mktemp</code></td>
    <td>Explains how to create temporary files and directories safely.<br><br></td>
  </tr>
  <tr>
    <td><code>man xxd</code></td>
    <td>Explains how <code>xxd</code> creates and reverses hexdumps.<br><br></td>
  </tr>
  <tr>
    <td><code>man file</code></td>
    <td>Explains how <code>file</code> identifies file types based on content.<br><br></td>
  </tr>
  <tr>
    <td><code>man gzip</code></td>
    <td>Explains how to decompress gzip-compressed files.<br><br></td>
  </tr>
  <tr>
    <td><code>man bzip2</code></td>
    <td>Explains how to decompress bzip2-compressed files.<br><br></td>
  </tr>
  <tr>
    <td><code>man tar</code></td>
    <td>Explains how to extract files from tar archives.<br><br></td>
  </tr>
  <tr>
    <td><code>man bash</code></td>
    <td>Provides background on command substitution, quoting, redirection, and shell behavior.<br><br></td>
  </tr>
</table>
