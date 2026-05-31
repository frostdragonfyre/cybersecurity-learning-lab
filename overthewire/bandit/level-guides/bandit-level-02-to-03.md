# Bandit Level 2 to Level 3

In this level, you will learn how the Linux shell and command-line programs handle filenames that contain spaces and begin with dash characters.

The password for the next level is stored in a file named `--spaces in this filename--`. Your job is to read that file without accidentally causing the shell to split the filename into separate arguments or causing `cat` to interpret the filename as an option.

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
    <td>Bandit Level 2 to Level 3<br><br></td>
  </tr>
  <tr>
    <td>Category</td>
    <td>Linux fundamentals, SSH, filenames with spaces, option-like filenames, shell parsing, quoting, escaping<br><br></td>
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

By the end of this level, you should understand two separate command-line issues: spaces can split a filename into multiple arguments, and filenames beginning with `-` or `--` may be interpreted as command options.

<table>
  <tr>
    <th width="30%">Learning Layer</th>
    <th width="70%">Objective</th>
  </tr>
  <tr>
    <td>Beginner</td>
    <td>You will learn how to connect to the Bandit server from WSL and read a file whose name contains spaces and begins with dash characters.<br><br></td>
  </tr>
  <tr>
    <td>Practitioner</td>
    <td>You will practice recognizing when the shell splits text into separate arguments and when a command interprets a filename as an option. You will learn two safe approaches: using an explicit path and using the option terminator <code>--</code>.<br><br></td>
  </tr>
  <tr>
    <td>Advanced</td>
    <td>You will connect this beginner exercise to a larger systems and security principle: parsing rules matter. Misunderstanding quoting, escaping, option parsing, and argument boundaries can break scripts, automation, forensic workflows, and security tooling.<br><br></td>
  </tr>
</table>

## 3. Level Summary

The official level goal says the password for the next level is stored in a file called `--spaces in this filename--` located in the home directory.

There are two traps in this filename.

First, the filename contains spaces. If you type the filename without quotes or escaping, the shell treats the words as separate arguments.

Second, the filename begins with `--`. Many command-line programs interpret arguments beginning with `-` or `--` as options. That means even if you quote the filename, `cat "--spaces in this filename--"` may still fail because `cat` interprets the quoted text as an option-like argument.

The safest beginner-friendly solution is to use an explicit relative path:

```bash
cat ./--spaces\ in\ this\ filename--
```

You can also use the `--` option terminator:

```bash
cat -- "--spaces in this filename--"
```

The first method teaches path disambiguation. The second method teaches option parsing.

Official level reference:

```text
https://overthewire.org/wargames/bandit/bandit3.html
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
    <td>Shell parsing</td>
    <td>The shell reads the line you type and separates it into a command and arguments. Spaces usually mark the boundary between arguments unless they are quoted or escaped.<br><br></td>
  </tr>
  <tr>
    <td>Filename with spaces</td>
    <td>A filename can contain spaces, but the shell will not automatically know that multiple words belong to one filename. You must quote or escape the spaces to preserve the filename as one argument.<br><br></td>
  </tr>
  <tr>
    <td>Quoting</td>
    <td>Quoting keeps text together as one argument. For example, <code>"--spaces in this filename--"</code> tells the shell to preserve the spaces, but it does not stop <code>cat</code> from treating the argument as an option-like value.<br><br></td>
  </tr>
  <tr>
    <td>Escaping</td>
    <td>Escaping changes how the shell treats the next character. In <code>./--spaces\ in\ this\ filename--</code>, each backslash tells the shell to treat the following space as part of the filename instead of an argument separator.<br><br></td>
  </tr>
  <tr>
    <td>Option-like filename</td>
    <td>A filename that begins with <code>-</code> or <code>--</code> can be mistaken for a command option. This is why quoting alone may not be enough.<br><br></td>
  </tr>
  <tr>
    <td>Explicit relative path</td>
    <td>A path such as <code>./--spaces\ in\ this\ filename--</code> tells the command to look for the file in the current directory. Because the argument starts with <code>./</code> instead of <code>--</code>, <code>cat</code> treats it as a path rather than as an option.<br><br></td>
  </tr>
  <tr>
    <td>Option terminator</td>
    <td>The standalone <code>--</code> tells many Unix-style commands to stop parsing options. Anything after it is treated as a positional argument rather than as an option.<br><br></td>
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
    <td>The filename contains spaces.</td>
    <td>This means the shell may split the filename into multiple arguments unless you quote or escape the spaces.<br><br></td>
  </tr>
  <tr>
    <td>The filename begins with <code>--</code>.</td>
    <td>This means <code>cat</code> may interpret the filename as an option, even when the filename is quoted.<br><br></td>
  </tr>
  <tr>
    <td>Quoting solves only part of the problem.</td>
    <td>Quotes preserve the spaces, but they do not change the fact that the argument begins with <code>--</code>.<br><br></td>
  </tr>
  <tr>
    <td>An explicit path changes how the argument begins.</td>
    <td>Using <code>./</code> makes the argument start with a path prefix instead of an option-like dash sequence.<br><br></td>
  </tr>
  <tr>
    <td>The option terminator <code>--</code> is another valid solution.</td>
    <td>Using <code>cat -- "--spaces in this filename--"</code> tells <code>cat</code> to stop interpreting later arguments as options.<br><br></td>
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
    <td>Start by connecting as the correct Bandit user for the level. Then list the files in the home directory and look carefully at the exact filename.<br><br></td>
  </tr>
  <tr>
    <td>Hint 2</td>
    <td>Ask yourself what the shell usually uses spaces for when it reads a command.<br><br></td>
  </tr>
  <tr>
    <td>Hint 3</td>
    <td>After you handle the spaces, ask why <code>cat</code> might still reject the filename as an option.<br><br></td>
  </tr>
  <tr>
    <td>Hint 4</td>
    <td>Try making the filename look like a path from the current directory, or tell <code>cat</code> to stop parsing options before giving it the filename.<br><br></td>
  </tr>
</table>

## 7. Commands Introduced

These commands are not just things to memorize. Each one teaches you something about remote login, filesystem orientation, shell parsing, option parsing, or file handling.

<table>
  <tr>
    <th width="30%">Command or Tool</th>
    <th width="70%">Explanation</th>
  </tr>
  <tr>
    <td><code>ssh bandit2@bandit.labs.overthewire.org -p 2220</code></td>
    <td>Connects from your local terminal to the remote OverTheWire Bandit server as user <code>bandit2</code> on port <code>2220</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>pwd</code></td>
    <td>Prints your current working directory. This helps you verify where you are after logging in.<br><br></td>
  </tr>
  <tr>
    <td><code>ls</code></td>
    <td>Lists files and directories in the current directory. In this level, it confirms that a file named <code>--spaces in this filename--</code> exists.<br><br></td>
  </tr>
  <tr>
    <td><code>cat --spaces in this filename--</code></td>
    <td>This intuitive command fails because the shell splits the filename at spaces and <code>cat</code> interprets the first argument beginning with <code>--</code> as an option.<br><br></td>
  </tr>
  <tr>
    <td><code>cat "--spaces in this filename--"</code></td>
    <td>This preserves the spaces, but it can still fail because the quoted argument begins with <code>--</code>, which <code>cat</code> may interpret as an option.<br><br></td>
  </tr>
  <tr>
    <td><code>cat ./--spaces\ in\ this\ filename--</code></td>
    <td>Reads the file by using an explicit relative path and escaping the spaces. This makes the argument begin with <code>./</code> instead of <code>--</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>cat -- "--spaces in this filename--"</code></td>
    <td>Reads the file by using the option terminator <code>--</code> before the filename. This tells <code>cat</code> to stop treating later arguments as options.<br><br></td>
  </tr>
  <tr>
    <td><code>ssh bandit3@bandit.labs.overthewire.org -p 2220</code></td>
    <td>Connects to the next Bandit account after you retrieve the password from the file.<br><br></td>
  </tr>
</table>

## 8. Walkthrough Without Credential Disclosure

This walkthrough assumes you are working from a local terminal, such as Windows Subsystem for Linux, macOS Terminal, or a Linux shell. The examples below use WSL because it gives Windows users a Linux-like command-line environment.

### Step 1

Open WSL and connect to the Bandit server as `bandit2`.

```bash
ssh bandit2@bandit.labs.overthewire.org -p 2220
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
    <td><code>bandit2</code></td>
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

List the files in the current directory.

```bash
ls
```

You should see a file named:

```text
--spaces in this filename--
```

This is the key detail. The file exists, but it has two properties that make it tricky: it contains spaces, and it begins with `--`.

### Step 4

Try the intuitive command and observe why it fails.

```bash
cat --spaces in this filename--
```

This command looks reasonable at first, but two things go wrong. The shell splits the text into multiple arguments at the spaces, and `cat` sees the first argument beginning with `--` as an option.

You may see an error similar to:

```text
cat: unrecognized option '--spaces'
Try 'cat --help' for more information.
```

That error is useful feedback. It tells you that `cat` did not treat the value as a normal filename.

### Step 5

Try quoting the filename and observe why quoting is not enough.

```bash
cat "--spaces in this filename--"
```

Quotes preserve the spaces, so the shell now passes the filename as one argument. However, the argument still begins with `--`, so `cat` may still interpret it as an option.

You may see an error similar to:

```text
cat: unrecognized option '--spaces in this filename--'
Try 'cat --help' for more information.
```

This is the key lesson: quoting solves the spaces problem, but it does not solve the option-like filename problem.

### Step 6

Read the file using an explicit relative path.

```bash
cat ./--spaces\ in\ this\ filename--
```

The `./` prefix means “look in the current directory.” By writing the filename as a path, you make the argument begin with `./` instead of `--`. The backslashes preserve the spaces.

The output is the password for the next Bandit level. Do not commit that password to GitHub.

### Step 7

You can also read the file using the option terminator.

```bash
cat -- "--spaces in this filename--"
```

The standalone `--` tells `cat` to stop parsing options. The quoted filename after it is then treated as a filename, not as an option.

You only need one of the two safe approaches. The explicit path method is often the easiest to understand. The option terminator method is useful because you will see it in many Unix-style tools.

### Step 8

Use the discovered password to log in to the next level.

```bash
ssh bandit3@bandit.labs.overthewire.org -p 2220
```

When prompted, enter the password you found in the file. Again, the terminal may not show characters while the password is typed. That is normal behavior.

At this point, you have moved from `bandit2` to `bandit3`.

## 9. Command Output and Screenshots

Use this section to include terminal output or screenshots after redacting credentials.

### Relevant Command Output

```text
$ ssh bandit2@bandit.labs.overthewire.org -p 2220
bandit2@bandit.labs.overthewire.org's password:
[successful login output omitted]

$ pwd
/home/bandit2

$ ls
--spaces in this filename--

$ cat --spaces in this filename--
cat: unrecognized option '--spaces'
Try 'cat --help' for more information.

$ cat "--spaces in this filename--"
cat: unrecognized option '--spaces in this filename--'
Try 'cat --help' for more information.

$ cat ./--spaces\ in\ this\ filename--
[REDACTED PASSWORD]
```

This output shows the central lesson. Without quoting or escaping, spaces split the filename. With quoting, the spaces are preserved, but the filename still begins with `--`. Using an explicit relative path or the option terminator handles both issues.

### Screenshot

<img width="867" height="239" alt="image" src="https://github.com/user-attachments/assets/1a66dcbe-fa9c-4bab-b1f8-4819c57c568d" />

<img width="669" height="239" alt="image" src="https://github.com/user-attachments/assets/d6109277-6c88-4e81-9813-f7816587d087" />


## 10. What Is Really Happening

In this level, you are learning that your command line is interpreted in stages.

First, the shell reads what you typed. It uses spaces to split the command into arguments unless those spaces are quoted or escaped.

When you type:

```bash
cat --spaces in this filename--
```

the shell passes several arguments to `cat`, similar to this:

```text
Argument 1: --spaces
Argument 2: in
Argument 3: this
Argument 4: filename--
```

Then `cat` interprets its arguments. Since the first argument begins with `--`, `cat` treats it like an option. That is why the error mentions an unrecognized option.

When you type:

```bash
cat "--spaces in this filename--"
```

the shell passes one argument to `cat`, but that argument still begins with `--`. Quoting affects how the shell groups the text. It does not necessarily change how the program interprets the argument.

When you type:

```bash
cat ./--spaces\ in\ this\ filename--
```

the shell preserves the spaces because they are escaped, and `cat` sees an argument that begins with `./`. That makes it clearly look like a path in the current directory.

When you type:

```bash
cat -- "--spaces in this filename--"
```

the standalone `--` tells `cat` to stop parsing options. The next argument is treated as a filename.

This is a small but important example of a broader security principle: parsing changes meaning. Many real vulnerabilities and operational failures come from misunderstanding how input is split, quoted, escaped, or interpreted by different layers.

## 11. Common Mistakes

<table>
  <tr>
    <th width="35%">Mistake</th>
    <th width="65%">Correction</th>
  </tr>
  <tr>
    <td>Typing <code>cat --spaces in this filename--</code> and assuming the file is missing.</td>
    <td>The file is not missing. The shell split the filename into separate arguments, and <code>cat</code> interpreted the first argument as an option.<br><br></td>
  </tr>
  <tr>
    <td>Thinking quotes always solve filename problems.</td>
    <td>Quotes preserve spaces, but they do not stop a command from treating an argument that begins with <code>-</code> or <code>--</code> as an option.<br><br></td>
  </tr>
  <tr>
    <td>Forgetting that spaces separate arguments.</td>
    <td>In most shell commands, spaces are not just visual separators. They define where one argument ends and another begins unless quoted or escaped.<br><br></td>
  </tr>
  <tr>
    <td>Using mismatched quotes.</td>
    <td>If you open a quote, close it. A command with an unfinished quote may leave the shell waiting for the closing quote.<br><br></td>
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

This level shows why quoting, escaping, and option parsing matter in administration, scripting, security tooling, and incident response.

In real systems, filenames, paths, usernames, log entries, and user-controlled values may contain spaces, dashes, or other special characters. If a script handles those values incorrectly, it may fail, process the wrong file, or interpret user-controlled data as command options.

Defensive engineering requires treating filenames and user-controlled strings as data that must be handled deliberately. When writing scripts or commands, avoid assuming that filenames are simple single-word strings.

## 13. Real-World Connection

This concept appears in real systems whenever automation processes files or user-controlled input. Backup scripts, log processing jobs, malware analysis workflows, file upload systems, CI/CD pipelines, and incident response tools may all encounter filenames with spaces or leading dashes.

A poorly written script might work during testing but fail in production because a real filename contains spaces or looks like an option. In security work, incorrect parsing can cause missed evidence, broken automation, inaccurate triage, or unsafe command execution.

The WSL-to-SSH workflow also mirrors real administrative work. Security analysts, system administrators, and engineers often use a local terminal to connect to remote systems, inspect files, review logs, and troubleshoot issues. Knowing which system you are currently operating on is essential.

## 14. Reflection Questions

Use these questions to check your understanding before moving to the next level. A good answer should explain the reasoning, not just repeat the command.

<table>
  <tr>
    <th width="35%">Question</th>
    <th width="65%">Learner Response</th>
  </tr>
  <tr>
    <td>What were the two separate command-line issues in this level?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>Why does <code>cat --spaces in this filename--</code> fail?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>Why does quoting the filename preserve the spaces but still fail?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>Why does <code>cat ./--spaces\ in\ this\ filename--</code> work?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What does the standalone <code>--</code> mean in <code>cat -- "--spaces in this filename--"</code>?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>How can you tell whether you are working in your local WSL shell or the remote Bandit shell?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>How does this level connect to secure scripting or defensive operations?</td>
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
    <td>OverTheWire Bandit Level 2 to Level 3</td>
    <td>Provides the official level goal and command suggestions for this exercise.</td>
  </tr>
  <tr>
    <td><code>man ssh</code></td>
    <td>Explains SSH syntax, remote login behavior, authentication, and the use of a non-default port with <code>-p</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>man cat</code></td>
    <td>Explains how <code>cat</code> reads files, handles input streams, and supports option parsing.<br><br></td>
  </tr>
  <tr>
    <td><code>man bash</code></td>
    <td>Provides background on shell syntax, arguments, quoting, escaping, and command execution.<br><br></td>
  </tr>
  <tr>
    <td>GNU Bash Manual, Quoting</td>
    <td>Explains how quoting preserves spaces and controls how the shell interprets special characters.<br><br></td>
  </tr>
  <tr>
    <td>POSIX Guideline 10</td>
    <td>Explains the convention that <code>--</code> should be accepted as a delimiter indicating the end of options.<br><br></td>
  </tr>
</table>
