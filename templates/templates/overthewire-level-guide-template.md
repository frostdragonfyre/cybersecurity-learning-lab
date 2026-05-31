# OverTheWire Level Guide Template

This template is designed for teaching OverTheWire levels without reducing them to answer dumps. Each guide should help the learner understand the underlying Linux, networking, web, cryptography, or security concept while preserving the problem-solving process.

The goal is to explain how to think through the level, what the commands are doing, why the solution works, and how the concept appears in real systems. Active passwords, direct credential dumps, and unexplained copy-paste solutions should be avoided.

## 1. Level Information

<table>
  <tr>
    <th width="35%">Field</th>
    <th width="65%">Response</th>
  </tr>
  <tr>
    <td>Wargame</td>
    <td>Enter the OverTheWire wargame name, such as Bandit, Natas, Leviathan, Krypton, Narnia, Behemoth, Utumno, Maze, or Vortex.<br><br></td>
  </tr>
  <tr>
    <td>Level</td>
    <td>Enter the level number or range, such as Bandit Level 0 or Bandit Level 0 to Level 1.<br><br></td>
  </tr>
  <tr>
    <td>Category</td>
    <td>Enter the main topic, such as Linux fundamentals, file permissions, command-line navigation, SSH, encoding, web security, cryptography, scripting, or privilege boundaries.<br><br></td>
  </tr>
  <tr>
    <td>Difficulty</td>
    <td>Enter beginner, intermediate, advanced, or wargame-specific difficulty.<br><br></td>
  </tr>
  <tr>
    <td>Spoiler posture</td>
    <td>Enter teaching notes, guided hints, partial walkthrough, full walkthrough for retired content, or private notes.<br><br></td>
  </tr>
  <tr>
    <td>Password policy</td>
    <td>State whether the guide avoids publishing active passwords, credentials, or direct answer strings.<br><br></td>
  </tr>
</table>

## 2. Learning Objective

Describe the primary concept the learner should understand after completing this level. The objective should be specific enough to guide the lesson, but broad enough to transfer beyond the exact challenge.

<table>
  <tr>
    <th width="30%">Learning Layer</th>
    <th width="70%">Objective</th>
  </tr>
  <tr>
    <td>Beginner</td>
    <td>Explain the basic skill the learner should gain, such as connecting with SSH, listing files, reading file contents, navigating directories, or using manual pages.<br><br></td>
  </tr>
  <tr>
    <td>Practitioner</td>
    <td>Explain the operational skill being developed, such as selecting the right command, interpreting command output, testing assumptions, or chaining simple tools together.<br><br></td>
  </tr>
  <tr>
    <td>Advanced</td>
    <td>Explain the deeper systems or security principle, such as process execution, permission models, shell parsing, trust boundaries, encoding semantics, protocol behavior, or privilege separation.<br><br></td>
  </tr>
</table>

## 3. Level Summary

Summarize what the learner is being asked to do in plain language. Avoid revealing the final password or direct answer at the start.

Response:

## 4. Concepts Introduced

Identify the concepts that are necessary to understand the level. Define terms in a way that is clear to beginners but still technically precise.

<table>
  <tr>
    <th width="30%">Concept</th>
    <th width="70%">Explanation</th>
  </tr>
  <tr>
    <td>Concept 1</td>
    <td>Explain the first core concept. For example, SSH provides encrypted remote shell access to a system where the user has valid credentials.<br><br></td>
  </tr>
  <tr>
    <td>Concept 2</td>
    <td>Explain the second core concept. For example, a command-line flag changes how a program behaves at runtime.<br><br></td>
  </tr>
  <tr>
    <td>Concept 3</td>
    <td>Explain the third core concept when needed. For example, hidden files are not special security objects; they are conventionally hidden from default directory listings.<br><br></td>
  </tr>
</table>

## 5. What the Learner Should Notice

Document the observations that should guide the learner toward the solution. These should be clues, not just answers.

<table>
  <tr>
    <th width="35%">Observation</th>
    <th width="65%">Why It Matters</th>
  </tr>
  <tr>
    <td>Observation 1</td>
    <td>Explain why this observation matters and how it narrows the problem.<br><br></td>
  </tr>
  <tr>
    <td>Observation 2</td>
    <td>Explain what the learner should infer from this observation.<br><br></td>
  </tr>
  <tr>
    <td>Observation 3</td>
    <td>Explain how this observation connects to a command, concept, or next step.<br><br></td>
  </tr>
</table>

## 6. Guided Hints

Use progressive hints. The first hint should point toward the relevant concept. Later hints may become more specific, but should still encourage reasoning.

<table>
  <tr>
    <th width="20%">Hint Level</th>
    <th width="80%">Hint</th>
  </tr>
  <tr>
    <td>Hint 1</td>
    <td>Provide a conceptual hint that identifies the general area to investigate without giving away the command.<br><br></td>
  </tr>
  <tr>
    <td>Hint 2</td>
    <td>Provide a more specific hint that points toward a command, option, file property, or behavior to inspect.<br><br></td>
  </tr>
  <tr>
    <td>Hint 3</td>
    <td>Provide a near-solution hint that still requires the learner to execute and interpret the result.<br><br></td>
  </tr>
</table>

## 7. Commands Introduced

Document commands used in the level and explain what they do. Commands should be taught as tools for reasoning, not memorized incantations.

<table>
  <tr>
    <th width="30%">Command or Tool</th>
    <th width="70%">Explanation</th>
  </tr>
  <tr>
    <td><code>example-command</code></td>
    <td>Explain what the command does, why it is relevant, and what output the learner should pay attention to.<br><br></td>
  </tr>
  <tr>
    <td><code>example-command -option</code></td>
    <td>Explain how the option changes the command behavior and why that matters for the level.<br><br></td>
  </tr>
  <tr>
    <td><code>man example-command</code></td>
    <td>Explain how to use the manual page to discover options, syntax, and examples.<br><br></td>
  </tr>
</table>

## 8. Walkthrough Without Credential Disclosure

Provide a teaching-oriented walkthrough. Avoid publishing active passwords or direct credential values. Explain the reasoning process and describe what the learner should observe.

### Step 1

Describe the first action and why it is appropriate.

```bash
# Add command only if appropriate and allowed by the spoiler posture.
```

Explain what the command is doing.

Response:

### Step 2

Describe the next action and how it follows from the previous observation.

```bash
# Add command only if appropriate and allowed by the spoiler posture.
```

Explain what the learner should observe.

Response:

### Step 3

Describe how the learner confirms the result without publishing restricted answer material.

```bash
# Add command only if appropriate and allowed by the spoiler posture.
```

Explain how to verify the concept.

Response:

## 9. Command Output and Screenshots

Use this section to include terminal output, screenshots, or other evidence that helps explain the level. Avoid including active passwords, credentials, tokens, private keys, or restricted answer material. Redact sensitive material before committing screenshots or output.

### Relevant Command Output

```text
Paste relevant command output here.
```

Explain what the output shows and why it matters.

Response:

### Screenshot

```markdown
![Screenshot description](../../assets/screenshots/example-screenshot.png)
```

Explain what the screenshot shows, what the learner should notice, and whether any sensitive information has been redacted.

Response:

## 10. What Is Really Happening

Explain the underlying system behavior. This is where the guide should become valuable beyond the immediate level.

For example, explain how the shell parses input, how Linux represents files and directories, how permissions are enforced, how standard input and output work, how SSH authenticates users, how encodings transform data, or how a web application processes a request.

Response:

## 11. Common Mistakes

Document mistakes that learners commonly make and explain how to correct the underlying misunderstanding.

<table>
  <tr>
    <th width="35%">Mistake</th>
    <th width="65%">Correction</th>
  </tr>
  <tr>
    <td>Example mistake</td>
    <td>Explain why the mistake happens and what the learner should understand instead.<br><br></td>
  </tr>
  <tr>
    <td>Example mistake</td>
    <td>Explain how to troubleshoot the issue without simply giving the answer.<br><br></td>
  </tr>
</table>

## 12. Defensive or Administrative Takeaway

Explain what this level teaches from a defensive, administrative, or real-world operations perspective. Even beginner levels can connect to secure administration, auditability, least privilege, credential hygiene, logging, or user training.

Response:

## 13. Real-World Connection

Explain where this concept appears outside the wargame. Connect the lesson to Linux servers, cloud instances, web applications, enterprise administration, incident response, software development, identity systems, or secure operations.

Response:

## 14. Reflection Questions

Use these questions to test understanding and support teaching.

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
    <td>What observation pointed toward the solution?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>Which command or behavior mattered most?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>Why does this concept matter in real systems?</td>
    <td><br><br></td>
  </tr>
  <tr>
    <td>What would you explain differently to a beginner?</td>
    <td><br><br></td>
  </tr>
</table>

## 15. References

Add references that support learning without bypassing the exercise.

<table>
  <tr>
    <th width="35%">Reference</th>
    <th width="65%">Why It Is Useful</th>
  </tr>
  <tr>
    <td>OverTheWire level page</td>
    <td>Provides the official level objective and any constraints or hints supplied by the platform.<br><br></td>
  </tr>
  <tr>
    <td>Relevant manual page</td>
    <td>Helps the learner understand command syntax, options, and behavior.<br><br></td>
  </tr>
  <tr>
    <td>Additional documentation</td>
    <td>Add Linux, networking, web, cryptography, or programming references where useful.<br><br></td>
  </tr>
</table>
