# Bandit Level 15 to Level 16

In this level, you will learn how to submit data to a network service over an encrypted SSL/TLS connection.

The password for the next level is retrieved by submitting the current level’s password to a service listening on port `30001` on `localhost`. Unlike the previous level, this service expects the connection to use SSL/TLS encryption. Your job is to connect with `openssl s_client`, submit the current password, and read the service response.

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
    <td>Bandit Level 15 to Level 16<br><br></td>
  </tr>
  <tr>
    <td>Category</td>
    <td>Linux fundamentals, networking, TCP services, SSL/TLS, OpenSSL, encrypted communication<br><br></td>
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

By the end of this level, you should understand how to use `openssl s_client` to connect to a service that expects SSL/TLS encryption. You should also understand the difference between sending data over a plain TCP connection and sending data over an encrypted TLS session.

<table>
  <tr>
    <th width="30%">Learning Layer</th>
    <th width="70%">Objective</th>
  </tr>
  <tr>
    <td>Beginner</td>
    <td>You will learn how to connect as <code>bandit15</code>, retrieve the current level password, and submit it to a TLS-enabled local service.<br><br></td>
  </tr>
  <tr>
    <td>Practitioner</td>
    <td>You will practice using <code>openssl s_client</code> to connect to a service, observe certificate and handshake output, send input, and interpret the response.<br><br></td>
  </tr>
  <tr>
    <td>Advanced</td>
    <td>You will connect this exercise to a broader security principle: encryption protects communication in transit, but clients must still understand which protocol a service expects and how to validate or interpret the connection.<br><br></td>
  </tr>
</table>

## 3. Level Summary

The official level goal says the password for the next level can be retrieved by submitting the password of the current level to port `30001` on `localhost` using SSL/TLS encryption.

That gives you four useful facts:

```text
Current user: bandit15
Current password file: /etc/bandit_pass/bandit15
Target host: localhost
Target port: 30001
Connection type: SSL/TLS
```

A useful manual workflow is:

```bash
cat /etc/bandit_pass/bandit15
openssl s_client -connect localhost:30001
```

Then paste or type the current `bandit15` password into the OpenSSL session and press Enter.

A more compact approach is:

```bash
cat /etc/bandit_pass/bandit15 | openssl s_client -connect localhost:30001 -quiet
```

The service should return the password for the next level.

Official level reference:

```text
https://overthewire.org/wargames/bandit/bandit16.html
```

## 4. Concepts Introduced

<table>
  <tr>
    <th width="30%">Concept</th>
    <th width="70%">Explanation</th>
  </tr>
  <tr>
    <td>SSL/TLS</td>
    <td>SSL/TLS is used to protect data in transit between a client and a server. Modern systems generally use TLS, but many tools and older references still use the term SSL.<br><br></td>
  </tr>
  <tr>
    <td>Encrypted connection</td>
    <td>An encrypted connection protects the contents of communication from being read directly by someone observing the network path.<br><br></td>
  </tr>
  <tr>
    <td><code>openssl</code></td>
    <td><code>openssl</code> is a command-line toolkit for working with cryptographic functions, certificates, and SSL/TLS connections.<br><br></td>
  </tr>
  <tr>
    <td><code>openssl s_client</code></td>
    <td><code>s_client</code> is an OpenSSL command used to connect to SSL/TLS services. It is commonly used for testing, troubleshooting, and inspecting encrypted connections.<br><br></td>
  </tr>
  <tr>
    <td><code>-connect</code></td>
    <td>The <code>-connect</code> option tells <code>openssl s_client</code> which host and port to connect to, using the format <code>host:port</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>-quiet</code></td>
    <td>The <code>-quiet</code> option reduces some of the connection output, making it easier to see the service response.<br><br></td>
  </tr>
  <tr>
    <td>Plain TCP versus TLS</td>
    <td>A plain TCP connection sends data without TLS encryption. A TLS connection performs a handshake first, then sends application data through an encrypted session.<br><br></td>
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
    <td>This level is similar to the previous Netcat level.</td>
    <td>You are still submitting the current password to a local service, but now the service expects SSL/TLS encryption.<br><br></td>
  </tr>
  <tr>
    <td>The target host is <code>localhost</code>.</td>
    <td>The service is running on the Bandit server itself. Run the command from inside the <code>bandit15</code> SSH session, not from local WSL.<br><br></td>
  </tr>
  <tr>
    <td>The target port is <code>30001</code>.</td>
    <td>This is the port where the TLS-enabled service is listening.<br><br></td>
  </tr>
  <tr>
    <td><code>nc localhost 30001</code> is not enough.</td>
    <td>The service expects SSL/TLS. A plain TCP client will not complete the expected encrypted session.<br><br></td>
  </tr>
  <tr>
    <td><code>openssl s_client</code> prints certificate and handshake information.</td>
    <td>This output can look noisy, but it is normal. The important part is the service response after the password is submitted.<br><br></td>
  </tr>
  <tr>
    <td>The password can be typed manually or piped into the command.</td>
    <td>Typing helps learners see the interaction. Piping is cleaner and more repeatable after the process is understood.<br><br></td>
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
    <td>Start by confirming that you are logged in as <code>bandit15</code>.<br><br></td>
  </tr>
  <tr>
    <td>Hint 2</td>
    <td>Read the current level password from <code>/etc/bandit_pass/bandit15</code>.<br><br></td>
  </tr>
  <tr>
    <td>Hint 3</td>
    <td>The service is on <code>localhost</code> port <code>30001</code>, but it expects SSL/TLS encryption.<br><br></td>
  </tr>
  <tr>
    <td>Hint 4</td>
    <td>Use <code>openssl s_client</code>, not plain <code>nc</code>, to connect to the TLS-enabled service.<br><br></td>
  </tr>
  <tr>
    <td>Hint 5</td>
    <td>After you understand the manual method, try piping the password into <code>openssl s_client</code> with <code>-quiet</code>.<br><br></td>
  </tr>
</table>

## 7. Commands Introduced

These commands are not just things to memorize. Each one teaches you something about encrypted connections, user context, network services, or command-line data flow.

<table>
  <tr>
    <th width="30%">Command or Tool</th>
    <th width="70%">Explanation</th>
  </tr>
  <tr>
    <td><code>ssh bandit15@bandit.labs.overthewire.org -p 2220</code></td>
    <td>Connects to the Bandit server as <code>bandit15</code> using the password retrieved in the previous level.<br><br></td>
  </tr>
  <tr>
    <td><code>whoami</code></td>
    <td>Displays the current username. This is useful to confirm that you are operating as <code>bandit15</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>cat /etc/bandit_pass/bandit15</code></td>
    <td>Reads the current level password. This is the value that must be submitted to the service on port <code>30001</code>.<br><br></td>
  </tr>
  <tr>
    <td><code>openssl s_client -connect localhost:30001</code></td>
    <td>Opens an SSL/TLS client connection to the service listening on port <code>30001</code> on the Bandit server.<br><br></td>
  </tr>
  <tr>
    <td><code>cat /etc/bandit_pass/bandit15 | openssl s_client -connect localhost:30001 -quiet</code></td>
    <td>Pipes the current password directly into the TLS-enabled service and reduces extra OpenSSL output.<br><br></td>
  </tr>
  <tr>
    <td><code>ssh bandit16@bandit.labs.overthewire.org -p 2220</code></td>
    <td>Connects to the next Bandit account after you retrieve the password from the service response.<br><br></td>
  </tr>
</table>

## 8. Walkthrough Without Credential Disclosure

This walkthrough assumes you are working from a local terminal, such as Windows Subsystem for Linux, macOS Terminal, or a Linux shell. The examples below use WSL because it gives Windows users a Linux-like command-line environment.

### Step 1

Connect to the Bandit server as `bandit15`.

```bash
ssh bandit15@bandit.labs.overthewire.org -p 2220
```

When prompted, enter the password you retrieved from the previous level. The terminal may not show characters while you type the password. That is normal behavior.

After you log in successfully, your commands are running inside a remote Linux shell on the Bandit server.

### Step 2

Confirm that you are operating as `bandit15`.

```bash
whoami
```

You should see:

```text
bandit15
```

This matters because the current password file is readable by the `bandit15` user.

### Step 3

Read the current level password.

```bash
cat /etc/bandit_pass/bandit15
```

This prints the password for the current level. Do not commit this password to GitHub.

You will submit this value to the service listening on port `30001`.

### Step 4

Connect to the TLS-enabled local service.

```bash
openssl s_client -connect localhost:30001
```

You will likely see certificate, connection, and handshake output. This is expected.

After the connection is established, paste or type the current `bandit15` password and press Enter.

If the password is correct, the service should return the password for `bandit16`.

### Step 5

Use the pipeline method as a cleaner alternative.

Once you understand the manual method, you can send the current password directly into the TLS-enabled service:

```bash
cat /etc/bandit_pass/bandit15 | openssl s_client -connect localhost:30001 -quiet
```

This command reads the current password and pipes it into `openssl s_client`.

The service response should include the password for the next level.

### Step 6

If you see `DONE`, `RENEGOTIATING`, or `KEYUPDATE`, do not panic.

The official level note mentions that these messages may appear and points learners to the `CONNECTED COMMANDS` section of the OpenSSL manual. They are related to OpenSSL connection behavior, not necessarily evidence that the level is broken.

If the session becomes awkward interactively, the pipeline method with `-quiet` is often easier to use:

```bash
cat /etc/bandit_pass/bandit15 | openssl s_client -connect localhost:30001 -quiet
```

### Step 7

Use the discovered password to log in to the next level.

```bash
ssh bandit16@bandit.labs.overthewire.org -p 2220
```

When prompted, enter the password returned by the service. The terminal may not show characters while the password is typed. That is normal behavior.

At this point, you have moved from `bandit15` to `bandit16`.

## 9. Command Output and Screenshots

Use this section to include terminal output or screenshots after redacting credentials.

### Relevant Command Output

```text
$ ssh bandit15@bandit.labs.overthewire.org -p 2220
bandit15@bandit.labs.overthewire.org's password:
[successful login output omitted]

$ whoami
bandit15

$ cat /etc/bandit_pass/bandit15
[REDACTED CURRENT PASSWORD]

$ openssl s_client -connect localhost:30001
[certificate and TLS handshake output omitted]
[CURRENT PASSWORD SUBMITTED]
Correct!
[REDACTED NEXT PASSWORD]
```

Alternative pipeline output:

```text
$ cat /etc/bandit_pass/bandit15 | openssl s_client -connect localhost:30001 -quiet
depth=0 CN = localhost
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN = localhost
verify return:1
Correct!
[REDACTED NEXT PASSWORD]
```

This output shows the central lesson. The service on port `30001` expects a TLS connection, and submitting the current level password returns the next level password.

### Screenshots

<img width="867" height="365" alt="image" src="https://github.com/user-attachments/assets/9bfabb12-fc4d-42ae-8b74-01615a50e0be" />

<img width="867" height="764" alt="image" src="https://github.com/user-attachments/assets/ae4c9ae0-a168-4a7c-9730-b7e68e7b8563" />

<img width="867" height="764" alt="image" src="https://github.com/user-attachments/assets/107d93f2-6cad-499b-b3a3-d714d8621c3c" />

## 10. What Is Really Happening

In this level, you are interacting with a network service that requires SSL/TLS.

In the previous level, you used `nc` to send data to a plain TCP service. In this level, a plain TCP client is not enough because the service expects a TLS handshake before accepting application data.

The command:

```bash
openssl s_client -connect localhost:30001
```

opens a TLS client connection to port `30001` on `localhost`.

Because you are logged in to the Bandit server, `localhost` means the Bandit server itself. It does not mean your Windows machine or your local WSL environment.

The pipeline version:

```bash
cat /etc/bandit_pass/bandit15 | openssl s_client -connect localhost:30001 -quiet
```

connects two commands together. The `cat` command prints the current password. The pipe sends that password into `openssl s_client`. OpenSSL establishes the TLS session and sends the password to the service. The service replies with the next password.

This level teaches a key network security concept: the protocol matters. A port is not just a number. The client and server must agree on how communication is structured, whether encryption is required, and what input the service expects.

## 11. Common Mistakes

<table>
  <tr>
    <th width="35%">Mistake</th>
    <th width="65%">Correction</th>
  </tr>
  <tr>
    <td>Using <code>nc localhost 30001</code> instead of OpenSSL.</td>
    <td>This level requires SSL/TLS encryption. Use <code>openssl s_client -connect localhost:30001</code> instead of a plain TCP client.<br><br></td>
  </tr>
  <tr>
    <td>Trying to connect to port <code>30001</code> from local WSL instead of from the Bandit server.</td>
    <td>The service is listening on <code>localhost</code> from the perspective of the Bandit server. Log in as <code>bandit15</code> first, then run the OpenSSL command from the remote shell.<br><br></td>
  </tr>
  <tr>
    <td>Submitting the wrong password.</td>
    <td>The service expects the current <code>bandit15</code> password, not an older password from a previous level.<br><br></td>
  </tr>
  <tr>
    <td>Confusing SSH port <code>2220</code> with service port <code>30001</code>.</td>
    <td>SSH uses port <code>2220</code>. This level’s TLS service uses port <code>30001</code>. They are different services.<br><br></td>
  </tr>
  <tr>
    <td>Being confused by certificate or handshake output.</td>
    <td><code>openssl s_client</code> prints connection details by default. This is normal. Use <code>-quiet</code> to reduce extra output.<br><br></td>
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

This level introduces the importance of encrypted service communication.

A service can listen on a port and still require a specific protocol before it accepts useful data. In this case, the service requires SSL/TLS. That means the client must establish an encrypted session before submitting the password.

From a defensive perspective, encrypted communication protects data in transit, but it also changes how services are tested and monitored. Analysts need to understand whether a service expects plain TCP, TLS, HTTP, HTTPS, SSH, or another protocol.

This level also shows why tooling matters. Netcat is useful for plain connections, while OpenSSL is useful for testing TLS-enabled services.

## 13. Real-World Connection

TLS is used throughout modern computing. HTTPS, secure APIs, email transport, VPNs, service-to-service communication, and many internal systems rely on TLS to protect data in transit.

Security analysts and system administrators often use `openssl s_client` to test certificates, inspect handshake behavior, troubleshoot TLS issues, and confirm whether a service is reachable over an encrypted connection.

This level is simple, but it teaches a foundational idea: secure communication requires both connectivity and the correct protocol.

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
    <td>Why is <code>nc</code> not the right tool for this level?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What does <code>openssl s_client -connect localhost:30001</code> do?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What does <code>localhost</code> mean when you are logged in to the Bandit server?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What is the difference between SSH port <code>2220</code> and service port <code>30001</code>?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What does the pipeline version do?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>How does this level connect to HTTPS, secure APIs, or encrypted service communication?</td>
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
    <td>OverTheWire Bandit Level 15 to Level 16</td>
    <td>Provides the official level goal, including the requirement to submit the current password to port <code>30001</code> using SSL/TLS encryption.<br><br></td>
  </tr>
  <tr>
    <td><code>man openssl</code></td>
    <td>Explains the OpenSSL command-line toolkit and its available cryptographic and TLS-related functions.<br><br></td>
  </tr>
  <tr>
    <td><code>man s_client</code></td>
    <td>Explains how <code>openssl s_client</code> connects to SSL/TLS services and provides details about connection options.<br><br></td>
  </tr>
  <tr>
    <td><code>man ssh</code></td>
    <td>Explains SSH syntax, authentication, hostnames, and ports.<br><br></td>
  </tr>
  <tr>
    <td><code>man bash</code></td>
    <td>Provides background on pipelines, standard input, and standard output.<br><br></td>
  </tr>
</table>
