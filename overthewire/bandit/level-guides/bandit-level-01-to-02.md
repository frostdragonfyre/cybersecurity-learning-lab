# Bandit Level 1 to Level 2

In this level, you will learn how Linux command-line tools can interpret the same character in different ways depending on context.

The password for the next level is stored in a file with an unusual name: `-`. Your job is to read that file without accidentally telling the command to read from standard input.

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
    <td>Bandit Level 1 to Level 2<br><br></td>
  </tr>
  <tr>
    <td>Category</td>
    <td>Linux fundamentals, SSH, special filenames, standard input, command-line interpretation<br><br></td>
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

By the end of this level, you should understand that a filename and a command argument are not always interpreted the same way. You should also be able to explain why `cat -` behaves differently from `cat ./-`.

<table>
  <tr>
    <th width="30%">Learning Layer</th>
    <th width="70%">Objective</th>
  </tr>
  <tr>
    <td>Beginner</td>
    <td>You will learn how to connect to a remote Linux system with SSH from WSL and read a file whose name has special meaning to command-line tools.<br><br></td>
  </tr>
  <tr>
    <td>Practitioner</td>
    <td>You will practice recognizing when a command interprets an argument as an option or stream indicator rather than as a literal filename.<br><br></td>
  </tr>
  <tr>
    <td>Advanced</td>
    <td>You will connect this small example to a larger systems principle: programs interpret inputs according to syntax, conventions, and context. That matters in shell usage, scripting, automation, and security engineering.<br><br></td>
  </tr>
</table>

## 3. Level Summary

The official level goal says the password for the next level is stored in a file called `-` located in the home directory.

That sounds simple, but there is a catch. The dash character has special meaning in many command-line tools. In this level, the challenge is not finding the file. The challenge is telling the command that `-` is the name of a file, not a special instruction to read from standard input.

You will solve this by using an explicit relative path:

```bash
cat ./-
```

The `./` means “look in the current directory.” By writing `./-`, you are telling `cat` that you mean the file named `-`.

Official level reference:

```text
https://overthewire.org/wargames/bandit/bandit2.html
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
    <td>When you run <code>ssh</code> from WSL, the command starts on your local Windows machine inside a Linux-like terminal. After you successfully log in, your commands run on the remote OverTheWire server. This distinction matters because you should always know whether you are working locally or remotely.<br><br></td>
  </tr>
  <tr>
    <td>Special filename</td>
    <td>A file can have a name that is valid but awkward to use. A single dash is a valid filename, but many command-line tools treat it as special syntax rather than an ordinary filename.<br><br></td>
  </tr>
  <tr>
    <td>Standard input</td>
    <td>Standard input, often called <code>stdin</code>, is the input stream a program reads from. In a terminal, standard input usually comes from your keyboard unless it is redirected from a file or another command.<br><br></td>
  </tr>
  <tr>
    <td>Explicit relative path</td>
    <td>A path such as <code>./-</code> tells the command to look for a file named <code>-</code> in the current directory. The <code>./</code> prefix removes ambiguity because the argument now looks like a file path, not a special standalone dash.<br><br></td>
  </tr>
  <tr>
    <td>Argument interpretation</td>
    <td>Commands do not treat every argument as a filename. Some arguments are options, some represent streams, and some are interpreted according to conventions built into the command.<br><br></td>
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
    <td>The file is named only <code>-</code>.</td>
    <td>This is the central clue. You are not solving a search problem. You are solving an argument interpretation problem.<br><br></td>
  </tr>
  <tr>
    <td><code>cat -</code> does not behave like <code>cat readme</code>.</td>
    <td>When <code>cat</code> receives a single dash, it commonly reads from standard input instead of opening a file named <code>-</code>.<br><br></td>
  </tr>
  <tr>
    <td>The file is in the current directory.</td>
    <td>Because the file is in your current directory, you can reference it with the explicit relative path <code>./-</code>.<br><br></td>
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
    <td>Start by connecting as the correct Bandit user for the level. Then list the files in the home directory and pay close attention to the exact filename.<br><br></td>
  </tr>
  <tr>
    <td>Hint 2</td>
    <td>Ask yourself why a command might treat <code>-</code> differently from a normal filename such as <code>readme</code>.<br><br></td>
  </tr>
  <tr>
    <td>Hint 3</td>
    <td>Try referring to the file by its path in the current directory rather than by the bare filename alone.<br><br></td>
  </tr>
</table>

## 7. Commands Introduced

These commands are not just things to memorize. Each one teaches you something about how the shell, remote login, or file handling works.

<table>
  <tr>
    <th width="30%">Command or Tool</th>
    <th width="70%">Explanation</th>
  </tr>
  <tr>
    <td><code>ssh bandit1@bandit.labs.overthewire.org -p 2220</code></td>
    <td>Connects from your local terminal to the remote OverTheWire Bandit server as user <code>bandit1</code> on port <code>2220</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>pwd</code></td>
    <td>Prints your current working directory. This helps you verify where you are after logging in.<br><br></td>
  </tr>
  <tr>
    <td><code>ls</code></td>
    <td>Lists files and directories in the current directory. In this level, it confirms that a file named <code>-</code> exists.<br><br></td>
  </tr>
  <tr>
    <td><code>cat -</code></td>
    <td>Often tells <code>cat</code> to read from standard input. This is useful as a teaching example, but it is not the correct way to read the file named <code>-</code> in this level.<br><br></td>
  </tr>
  <tr>
    <td><code>cat ./-</code></td>
    <td>Reads the file named <code>-</code> from the current directory. The <code>./</code> prefix makes the argument an explicit relative path.<br><br></td>
  </tr>
  <tr>
    <td><code>Ctrl+C</code></td>
    <td>Interrupts a command that is waiting for input or not behaving as expected. If <code>cat -</code> appears to hang, it may be waiting for keyboard input.<br><br></td>
  </tr>
</table>

## 8. Walkthrough Without Credential Disclosure

This walkthrough assumes you are working from a local terminal, such as Windows Subsystem for Linux, macOS Terminal, or a Linux shell. The examples below use WSL because it gives Windows users a Linux-like command-line environment.

### Step 1

Open WSL and connect to the Bandit server as `bandit1`.

```bash
ssh bandit1@bandit.labs.overthewire.org -p 2220
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
    <td><code>bandit1</code></td>
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

When prompted for the password, enter the password you obtained from the previous level. The terminal may not show any characters while you type the password. That is normal behavior for password prompts.

After you log in successfully, your commands are running inside a remote Linux shell on the Bandit server, not merely inside your local WSL environment.

### Step 2

Confirm your current working directory.

```bash
pwd
```

This command prints the directory your shell is currently operating in. This matters because many beginner mistakes come from assuming the current filesystem location without verifying it.

You should see that you are in the Bandit user’s home directory.

### Step 3

List the files in the home directory.

```bash
ls
```

You should see a file named:

```text
-
```

This is the key detail. The file exists, but its name conflicts with a common Unix command-line convention.

### Step 4

Try the intuitive command and observe what happens.

```bash
cat -
```

This command is useful as a teaching moment. In many contexts, `cat -` tells `cat` to read from standard input. That means it may wait for you to type input from the keyboard instead of printing the contents of the file named `-`.

If the terminal appears to wait for input, interrupt it with:

```text
Ctrl+C
```

This is not a failure. It is the lesson. The command interpreted `-` as a special argument, not as the file you meant to read.

### Step 5

Read the file using an explicit relative path.

```bash
cat ./-
```

The `./` prefix means “look in the current directory.” By writing `./-`, you are telling `cat` to open the file named `-` located in the current directory rather than interpreting the dash as a special argument.

The output is the password for the next Bandit level. Do not commit that password to GitHub.

### Step 6

Use the discovered password to log in to the next level.

```bash
ssh bandit2@bandit.labs.overthewire.org -p 2220
```

When prompted, enter the password you found in the file. Again, the terminal may not show characters while the password is typed. That is normal behavior.

At this point, you have moved from `bandit1` to `bandit2`.

## 9. Command Output and Screenshots

Use this section to include terminal output or screenshots after redacting credentials.

### Relevant Command Output

```text
$ ssh bandit1@bandit.labs.overthewire.org -p 2220
bandit1@bandit.labs.overthewire.org's password:
[successful login output omitted]

$ pwd
/home/bandit1

$ ls
-

$ cat -
[command waits for standard input]

$ cat ./-
[REDACTED PASSWORD]
```

This output shows the central lesson. A bare dash is ambiguous to the command, while `./-` explicitly identifies a file in the current directory.

### Screenshot

<img width="867" height="276" alt="image" src="https://github.com/user-attachments/assets/ec683759-3ea8-42a7-a004-ff347c47ba82" />

<img width="867" height="281" alt="image" src="https://github.com/user-attachments/assets/d2fee5c2-c7a7-4ce7-9def-981775c20dd3" />

## 10. What Is Really Happening

In this level, you are learning that a filename and a command argument are not always interpreted the same way.

The shell passes arguments to programs. The command then decides how to interpret those arguments. A file named `-` is valid, but many Unix-style programs use the single dash as a convention for standard input or standard output. This means the problem is not that the file cannot be read. The problem is that the command needs an unambiguous way to identify the file.

The expression `./-` solves that problem. The dot represents the current directory, and the slash separates the directory from the filename. Once the argument is written as a path, the command treats it as a file path rather than as a special standalone dash.

This is a small example of a larger security and systems principle: syntax matters. The same character can have different meaning depending on context. In security work, misunderstandings about parsing, quoting, escaping, paths, and argument handling often lead to bugs, misconfigurations, and vulnerabilities.

## 11. Common Mistakes

<table>
  <tr>
    <th width="35%">Mistake</th>
    <th width="65%">Correction</th>
  </tr>
  <tr>
    <td>Running <code>cat -</code> and thinking the terminal is broken.</td>
    <td>The command may be waiting for standard input. Use <code>Ctrl+C</code> to interrupt it, then reference the file as <code>./-</code>.<br><br></td>
  </tr>
  <tr>
    <td>Assuming a dash cannot be a filename.</td>
    <td>Linux permits many unusual filenames. The challenge is not whether the file exists; the challenge is how to refer to it unambiguously.<br><br></td>
  </tr>
  <tr>
    <td>Trying unrelated search commands too early.</td>
    <td>The level goal already says the file is in the home directory. Start with the simplest local observation first.<br><br></td>
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

This level shows why command-line precision matters in administration and security work. Special characters, ambiguous filenames, and argument parsing can affect how tools behave. A command that appears obvious may do something different if the input has special meaning.

From a defensive perspective, this connects to safe scripting, secure automation, and operational reliability. Scripts that process filenames should account for unusual characters, spaces, leading dashes, and other edge cases. Administrators should avoid assuming that filenames are always simple, human-friendly strings.

## 13. Real-World Connection

The concept appears in real systems whenever automation processes untrusted or unusual filenames. Backup scripts, log processing jobs, malware analysis workflows, file upload systems, and incident response tools may all encounter filenames that begin with dashes or contain special characters.

A poorly written script might misinterpret a filename as an option. In the worst case, this can cause data loss, incorrect analysis, or unintended command behavior. Defensive engineering often requires treating filenames and user-controlled strings as data that must be quoted, escaped, validated, and handled deliberately.

The WSL-to-SSH workflow also mirrors real administrative work. Security analysts, system administrators, and engineers often use a local terminal to connect to remote systems, inspect files, review logs, and troubleshoot issues. Knowing which system you are currently operating on is essential.

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
    <td>Why does <code>cat -</code> behave differently from <code>cat ./-</code>?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What does <code>./</code> mean in a Linux path?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>How can you tell whether you are working in your local WSL shell or the remote Bandit shell?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>Why can unusual filenames create problems for scripts or command-line tools?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>How does this level connect to secure automation or defensive operations?</td>
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
    <td>OverTheWire Bandit Level 1 to Level 2</td>
    <td>Provides the official level goal, command suggestions, and helpful reading material.</td>
  </tr>
  <tr>
    <td><code>man ssh</code></td>
    <td>Explains SSH syntax, remote login behavior, and the use of a non-default port with <code>-p</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>man cat</code></td>
    <td>Explains how <code>cat</code> reads files and handles input streams.<br><br></td>
  </tr>
  <tr>
    <td><code>man bash</code></td>
    <td>Provides background on shell syntax, arguments, quoting, and command execution.<br><br></td>
  </tr>
  <tr>
    <td>Advanced Bash-Scripting Guide, Special Characters</td>
    <td>Useful for understanding why certain characters have special meaning in shell contexts.<br><br></td>
  </tr>
</table>
