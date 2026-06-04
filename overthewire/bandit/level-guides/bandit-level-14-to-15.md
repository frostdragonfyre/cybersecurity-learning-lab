# Bandit Level 14 to Level 15

In this level, you will learn how to send data to a network service using `nc`, also known as Netcat.

The password for the next level is retrieved by submitting the current level’s password to a service listening on port `30000` on `localhost`. Your job is to understand how to connect to a local TCP service, send the correct input, and read the response.

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
    <td>Bandit Level 14 to Level 15<br><br></td>
  </tr>
  <tr>
    <td>Category</td>
    <td>Linux fundamentals, networking, TCP services, Netcat, local services, credential submission<br><br></td>
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

By the end of this level, you should understand how to connect to a TCP service using `nc`, how `localhost` refers to the current machine, and how simple network services can accept input and return output through a terminal connection.

<table>
  <tr>
    <th width="30%">Learning Layer</th>
    <th width="70%">Objective</th>
  </tr>
  <tr>
    <td>Beginner</td>
    <td>You will learn how to connect to the Bandit server as <code>bandit14</code>, read the current password file, and submit that password to a local network service.<br><br></td>
  </tr>
  <tr>
    <td>Practitioner</td>
    <td>You will practice using <code>nc</code> to connect to a TCP port, send input, and interpret the service response.<br><br></td>
  </tr>
  <tr>
    <td>Advanced</td>
    <td>You will connect this exercise to a broader security principle: services listening on ports expose interfaces that can be tested, automated, abused, monitored, or protected depending on how they are designed and controlled.<br><br></td>
  </tr>
</table>

## 3. Level Summary

The official level goal says the password for the next level can be retrieved by submitting the password of the current level to port `30000` on `localhost`.

That gives you three useful facts:

```text
Current user: bandit14
Current password file: /etc/bandit_pass/bandit14
Target host: localhost
Target port: 30000
```

A useful workflow is:

```bash
cat /etc/bandit_pass/bandit14
nc localhost 30000
```

Then paste or type the current `bandit14` password into the Netcat session and press Enter.

A more compact approach is:

```bash
cat /etc/bandit_pass/bandit14 | nc localhost 30000
```

The service should return the password for the next level.

Official level reference:

```text
https://overthewire.org/wargames/bandit/bandit15.html
```

## 4. Concepts Introduced

<table>
  <tr>
    <th width="30%">Concept</th>
    <th width="70%">Explanation</th>
  </tr>
  <tr>
    <td>TCP service</td>
    <td>A TCP service listens on a network port and accepts connections from clients. In this level, a service is listening on port <code>30000</code>.<br><br></td>
  </tr>
  <tr>
    <td>Port</td>
    <td>A port identifies a specific service on a host. The hostname tells you which machine to contact, and the port tells you which service on that machine to use.<br><br></td>
  </tr>
  <tr>
    <td><code>localhost</code></td>
    <td><code>localhost</code> refers to the current machine. In this level, after you are logged in to the Bandit server as <code>bandit14</code>, <code>localhost</code> means the Bandit server itself.<br><br></td>
  </tr>
  <tr>
    <td><code>nc</code></td>
    <td><code>nc</code>, or Netcat, is a command-line tool used to read from and write to network connections. It is often used for simple TCP testing and troubleshooting.<br><br></td>
  </tr>
  <tr>
    <td>Standard input</td>
    <td>Standard input is the data a command receives. You can type data manually into <code>nc</code>, or pipe data into it from another command.<br><br></td>
  </tr>
  <tr>
    <td>Pipeline</td>
    <td>A pipeline uses <code>|</code> to send the output of one command into another command. In this level, the current password can be piped into <code>nc</code>.<br><br></td>
  </tr>
  <tr>
    <td>Service response</td>
    <td>After a service receives input, it may return output. In this level, the service returns the password for the next Bandit level if the submitted password is correct.<br><br></td>
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
    <td>You are already authenticated as <code>bandit14</code>.</td>
    <td>The current user context allows you to read <code>/etc/bandit_pass/bandit14</code>, which contains the password that must be submitted to the service.<br><br></td>
  </tr>
  <tr>
    <td>The target host is <code>localhost</code>.</td>
    <td>The service is running on the same server you are logged in to, not on your local WSL machine.<br><br></td>
  </tr>
  <tr>
    <td>The target port is <code>30000</code>.</td>
    <td>The port tells <code>nc</code> which service to connect to on the host.<br><br></td>
  </tr>
  <tr>
    <td>The service expects the current password as input.</td>
    <td>The password for <code>bandit14</code> is used as the proof needed to retrieve the password for <code>bandit15</code>.<br><br></td>
  </tr>
  <tr>
    <td>You can type the password manually or pipe it into <code>nc</code>.</td>
    <td>Typing is easier to understand at first. Piping is cleaner, more repeatable, and less error-prone once you understand the flow.<br><br></td>
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
    <td>Start by confirming that you are logged in as <code>bandit14</code>.<br><br></td>
  </tr>
  <tr>
    <td>Hint 2</td>
    <td>Read the current level password from <code>/etc/bandit_pass/bandit14</code>.<br><br></td>
  </tr>
  <tr>
    <td>Hint 3</td>
    <td>Use <code>nc</code> to connect to <code>localhost</code> on port <code>30000</code>.<br><br></td>
  </tr>
  <tr>
    <td>Hint 4</td>
    <td>Submit the current level password to the service and read the response.<br><br></td>
  </tr>
  <tr>
    <td>Hint 5</td>
    <td>After you understand the manual method, try piping the password into <code>nc</code> directly.<br><br></td>
  </tr>
</table>

## 7. Commands Introduced

These commands are not just things to memorize. Each one teaches you something about user context, network services, or command-line data flow.

<table>
  <tr>
    <th width="30%">Command or Tool</th>
    <th width="70%">Explanation</th>
  </tr>
  <tr>
    <td><code>ssh -i bandit14.private bandit14@bandit.labs.overthewire.org -p 2220</code></td>
    <td>Connects to the Bandit server as <code>bandit14</code> using the private key downloaded in the previous level.<br><br></td>
  </tr>
  <tr>
    <td><code>whoami</code></td>
    <td>Displays the current username. This is useful to confirm that you are operating as <code>bandit14</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>cat /etc/bandit_pass/bandit14</code></td>
    <td>Reads the current level password. This is the value that must be submitted to the service on port <code>30000</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>nc localhost 30000</code></td>
    <td>Uses Netcat to connect to the service listening on port <code>30000</code> on the Bandit server.<br><br></td>
  </tr>
  <tr>
    <td><code>cat /etc/bandit_pass/bandit14 | nc localhost 30000</code></td>
    <td>Pipes the current password directly into the network service and prints the service response.<br><br></td>
  </tr>
  <tr>
    <td><code>ssh bandit15@bandit.labs.overthewire.org -p 2220</code></td>
    <td>Connects to the next Bandit account after you retrieve the password from the service response.<br><br></td>
  </tr>
</table>

## 8. Walkthrough Without Credential Disclosure

This walkthrough assumes you are already able to log in as `bandit14`. In the previous level, you downloaded the private key and used it to authenticate as `bandit14`.

### Step 1

Connect to the Bandit server as `bandit14`.

```bash
ssh -i bandit14.private bandit14@bandit.labs.overthewire.org -p 2220
```

This command uses the private key from the previous level.

If you are prompted that the key file has overly open permissions, return to your local WSL terminal and run:

```bash
chmod 600 bandit14.private
```

Then try the SSH command again.

### Step 2

Confirm that you are operating as `bandit14`.

```bash
whoami
```

You should see:

```text
bandit14
```

This matters because the current password file is readable by the `bandit14` user.

### Step 3

Read the current level password.

```bash
cat /etc/bandit_pass/bandit14
```

This prints the password for the current level. Do not commit this password to GitHub.

You will submit this value to the service listening on port `30000`.

### Step 4

Connect to the local service with Netcat.

```bash
nc localhost 30000
```

Your terminal may appear to wait for input. That means the connection is open and the service is waiting for you to type something.

Paste or type the current `bandit14` password and press Enter.

If the password is correct, the service should return the password for `bandit15`.

### Step 5

Use the pipeline method as a cleaner alternative.

Once you understand the manual method, you can send the current password directly into the service:

```bash
cat /etc/bandit_pass/bandit14 | nc localhost 30000
```

This command reads the current password and pipes it into `nc`.

The service response should include the password for the next level.

### Step 6

Use the discovered password to log in to the next level.

```bash
ssh bandit15@bandit.labs.overthewire.org -p 2220
```

When prompted, enter the password returned by the service. The terminal may not show characters while the password is typed. That is normal behavior.

At this point, you have moved from `bandit14` to `bandit15`.

## 9. Command Output and Screenshots

Use this section to include terminal output or screenshots after redacting credentials and private key material.

### Relevant Command Output

```text
$ ssh -i bandit14.private bandit14@bandit.labs.overthewire.org -p 2220
[successful login output omitted]

$ whoami
bandit14

$ cat /etc/bandit_pass/bandit14
[REDACTED CURRENT PASSWORD]

$ nc localhost 30000
[CURRENT PASSWORD SUBMITTED]
Correct!
[REDACTED NEXT PASSWORD]
```

Alternative pipeline output:

```text
$ cat /etc/bandit_pass/bandit14 | nc localhost 30000
Correct!
[REDACTED NEXT PASSWORD]
```

This output shows the central lesson. A local service is listening on port `30000`, and submitting the current level password returns the next level password.

### Screenshots

<img width="876" height="468" alt="image" src="https://github.com/user-attachments/assets/de4ce570-432b-4171-839c-c5e4f9771b5a" />

<img width="703" height="464" alt="image" src="https://github.com/user-attachments/assets/8cdeb2fb-e4bf-4429-a5e9-058e97c80b01" />

## 10. What Is Really Happening

In this level, you are interacting with a network service.

The command:

```bash
nc localhost 30000
```

opens a TCP connection to port `30000` on `localhost`.

Because you are logged in to the Bandit server, `localhost` means the Bandit server itself. It does not mean your Windows machine or your local WSL environment.

The service on port `30000` expects the current level password. If you send the correct value, the service returns the password for the next level.

The pipeline version:

```bash
cat /etc/bandit_pass/bandit14 | nc localhost 30000
```

connects two commands together. The `cat` command prints the current password. The pipe sends that password into `nc`. The `nc` command sends it to the network service. The service replies with the next password.

This level teaches a key systems concept: many services are just programs listening for input on a network port and returning output. Security work often involves identifying services, understanding what input they accept, and determining how they respond.

## 11. Common Mistakes

<table>
  <tr>
    <th width="35%">Mistake</th>
    <th width="65%">Correction</th>
  </tr>
  <tr>
    <td>Trying to connect to port <code>30000</code> from local WSL instead of from the Bandit server.</td>
    <td>The service is listening on <code>localhost</code> from the perspective of the Bandit server. Log in as <code>bandit14</code> first, then run <code>nc localhost 30000</code> from the remote shell.<br><br></td>
  </tr>
  <tr>
    <td>Submitting the wrong password.</td>
    <td>The service expects the current <code>bandit14</code> password, not an older password from a previous level.<br><br></td>
  </tr>
  <tr>
    <td>Forgetting to press Enter after typing the password.</td>
    <td>The service may not process the input until a newline is sent. Press Enter after typing or pasting the password.<br><br></td>
  </tr>
  <tr>
    <td>Confusing the Bandit SSH port with the service port.</td>
    <td>SSH uses port <code>2220</code>. This level’s local service uses port <code>30000</code>. They are different services.<br><br></td>
  </tr>
  <tr>
    <td>Thinking <code>localhost</code> always means your laptop.</td>
    <td><code>localhost</code> means the current machine where the command is running. If you are inside the Bandit SSH session, <code>localhost</code> means the Bandit server.<br><br></td>
  </tr>
  <tr>
    <td>Publishing passwords in screenshots or notes.</td>
    <td>Credentials should be redacted from public writeups. The guide should teach the method without exposing active credential material.<br><br></td>
  </tr>
</table>

## 12. Defensive or Administrative Takeaway

This level introduces a basic but important networking idea: services listen on ports, accept input, and return output.

From a defensive perspective, every listening service is an interface that must be understood and controlled. Administrators should know which services are listening, which interfaces they bind to, who can reach them, what input they accept, and what they return.

The level also shows why local services matter. A service bound to `localhost` may not be reachable from the wider network, but it can still be reached by users or processes on the same host. That matters for privilege boundaries, service design, and local attack paths.

## 13. Real-World Connection

Netcat is often used for network troubleshooting, banner grabbing, simple client testing, and security labs. It helps learners understand how raw network connections behave without needing a browser or custom client.

In real security work, analysts may use similar techniques to test whether a service is reachable, whether a port is open, what kind of response a service gives, or whether unexpected input causes unsafe behavior.

This level is simple, but it teaches a core idea: network services are interfaces, and interfaces need controls.

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
    <td>What does <code>localhost</code> mean when you are logged in to the Bandit server?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What does <code>nc localhost 30000</code> do?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>Why does the service expect the current level password?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What is the difference between SSH port <code>2220</code> and service port <code>30000</code>?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What does the pipeline version do?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>How does this level connect to service testing or network security?</td>
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
    <td>OverTheWire Bandit Level 14 to Level 15</td>
    <td>Provides the official level goal and command suggestions for this exercise.</td>
  </tr>
  <tr>
    <td><code>man nc</code></td>
    <td>Explains how Netcat opens network connections, listens on ports, and sends or receives data.<br><br></td>
  </tr>
  <tr>
    <td><code>man ssh</code></td>
    <td>Explains SSH syntax, authentication, identity files, hostnames, and ports.<br><br></td>
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
