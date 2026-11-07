# KAVACH BLUE TEAM ARENA
## Challenge 01 — The Login That Shouldn't Have Happened

| Field | Details |
|---|---|
| Challenge ID | `KAVACH-BT-001` |
| Difficulty | Easy |
| Category | Linux Log Analysis · Authentication Monitoring · Initial Triage |
| Evidence | `evidence/kavach_01_auth.log` |
| Evidence format | Linux authentication-style text log |
| Suggested time | 35–50 minutes |
| Maximum score | 100 points |
| Required environment | Any computer with a text editor and command-line tools |

---

## 1. Situation

You are the junior analyst on duty for the Blue Team at **Northbridge Analytics**, a fictional company. The infrastructure team has forwarded an authentication log from one of its Ubuntu servers after an automated monitoring rule reported unusual SSH activity.

The alert itself is deliberately vague:

> **Alert:** Unusual authentication activity observed on `ubuntu-server`. Review the attached authentication records and determine whether the activity requires escalation.

The server is used by several employees and service operators. Routine activity in the log includes SSH public-key logins, scheduled tasks, administrative commands, account-management events and normal session activity.

Your job is not to find one suspicious line and stop. You must establish whether the evidence forms a coherent incident, distinguish it from routine activity, and explain what the available records do—and do not—prove.

You have received one evidence file:

```text
evidence/kavach_01_auth.log
```

The file contains 1,000 timestamped records. It is a **synthetic training dataset**; the organization, host activity and events are fictional.

For the short-form question sheet, see [questions.md](questions.md). Organizer-only evaluation material and the reference answer key are in the private `organizer/` directory.

## 2. Mission

Perform an initial SOC investigation and produce an evidence-based assessment.

At the end of the investigation, you should be able to answer:

1. Is there a suspicious authentication pattern?
2. Which source and account are most strongly associated with it?
3. Did the log record a successful authentication after the failures?
4. What activity followed that authentication?
5. Is there evidence of privileged command execution?
6. What conclusions can reasonably be made, and what remains unverified?

Do not assume that every failed login is part of the same activity. Do not assume that every successful login is malicious. Use timestamps, source addresses, usernames, process identifiers and session details to support your conclusions.

## 3. Rules of engagement

- Work only with the supplied log file.
- Do not attempt to connect to, scan or attack any real system.
- Do not treat an IP address or username as malicious without supporting evidence.
- Preserve the original evidence file. Perform analysis on a copy if you need to transform it.
- Record the commands, filters or scripts used for important findings.
- Where the log does not provide enough information, explicitly state **“not established by the supplied evidence.”**
- Timestamps are shown as recorded in the file. No timezone is supplied; do not invent one.

## 4. Investigation tasks

### Task A — Establish a baseline (10 points)

Before identifying an incident, understand what normal-looking activity exists in the evidence.

1. Identify at least **four distinct categories** of events present in the log. For each category, provide one example record or a short description.
2. Explain the difference between:
   - `Failed password`
   - `Accepted password`
   - `Accepted publickey`
3. Identify at least two reasons why a successful SSH login should not automatically be classified as malicious.
4. Explain why the presence of many failed logins alone is insufficient to conclude that an account was compromised.

**Expected submission:** A short baseline summary. Do not paste the entire log.

### Task B — Find and characterize suspicious authentication activity (20 points)

Investigate failed SSH authentication attempts across the dataset.

1. Identify the source address that deserves the highest priority for investigation. Explain why it stands out compared with other sources.
2. Determine the total number of failed password attempts associated with that source.
3. Determine the usernames targeted by that source and provide a count for each username.
4. Describe the time span covered by the repeated attempts. Include the first and last observed timestamps.
5. Based on the sequence and distribution of attempts, state whether the activity is more consistent with:
   - a single mistyped password,
   - password guessing / brute-force-like activity,
   - routine administrative access, or
   - insufficient evidence to distinguish these.

Choose one and justify it using at least **three separate observations** from the log.

**Expected submission:** A compact table of targeted usernames and counts, plus a short evidence-based explanation.

### Task C — Determine whether authentication succeeded (15 points)

A pattern of failed logins is important, but the investigation must establish whether any authentication succeeded.

1. Search for successful password-based SSH authentication associated with the source identified in Task B.
2. Record the timestamp, account name, source address, source port and SSH process ID for the relevant event.
3. Locate the corresponding session-open record. Explain how its account and process information relates to the successful authentication record.
4. Determine whether the supplied evidence supports the statement **“the source successfully authenticated as the targeted account.”** Explain the evidence chain.
5. Identify one other successful SSH login in the dataset that should not be merged into this incident without additional evidence. Explain which field(s) distinguish it.

**Expected submission:** A short authentication finding with at least two correlated records.

### Task D — Reconstruct activity after authentication (20 points)

Continue the investigation beyond the successful login. Be careful: chronological proximity and a matching account name do not, by themselves, prove that a later command came from the same remote SSH session.

1. Identify all `sudo` command records explicitly attributed to the account involved in the suspicious authentication.
2. Put those commands in chronological order. For each, record:
   - timestamp,
   - invoking account,
   - target user,
   - working directory,
   - command executed,
   - terminal identifier, if present.
3. Explain what the commands appear to be checking or doing. Distinguish basic system discovery from an action that changes system state.
4. Determine whether the records show that the account invoked commands with root privileges. Explain the significance of the `USER=root` field.
5. Compare the timestamps of the successful SSH authentication, its session records (including any disconnect), and the later `sudo` commands. State the elapsed time between the successful authentication and the first recorded `sudo` command, then explain whether the supplied log conclusively links that command to the remote source.

**Expected submission:** A chronological activity table and a short interpretation. Do not infer that a command succeeded beyond what the log actually records.

### Task E — Separate signal from noise (10 points)

A SOC analyst must avoid both missing real activity and escalating unrelated events.

1. Find two examples of activity that may initially look suspicious but should not automatically be attributed to the incident.
2. For each example, state which fields or contextual differences prevent you from confidently linking it to the suspicious source.
3. Explain why matching only on the username is weaker than correlating username, source address, timestamp and session/process information.
4. Identify one limitation of the supplied log that prevents a definitive conclusion about the full scope of the activity.

**Expected submission:** Two short false-positive / unrelated-activity assessments.

### Task F — Build an incident timeline (10 points)

Create a timeline containing at least **six milestones** from the evidence. It must include:

- the beginning of the repeated authentication failures,
- a representative point during the repeated attempts,
- the final observed failure from the suspicious source,
- the successful authentication,
- the session-open event,
- the session disconnect event, if present,
- the first subsequent privileged command,
- and the last relevant privileged command.

For each milestone, include the timestamp, event description and the evidence field(s) that support it.

Your timeline must be chronological. Do not include unrelated routine events merely to make it longer.

**Expected submission:** A table with columns `Timestamp`, `Event`, `Evidence`, and `Interpretation`.

### Task G — Analyst assessment and response (15 points)

Write a concise SOC handoff note for the next analyst or incident responder.

Your note must include:

1. **Verdict:** Benign, suspicious, or confirmed compromise. Choose the strongest conclusion justified by the supplied evidence and explain the confidence level.
2. **Affected asset:** Identify the host shown in the records.
3. **Account:** Identify the account associated with the suspicious successful authentication.
4. **Indicators:** List the relevant source address, authentication pattern, and later account-level privileged activity. Clearly distinguish observed records from activity attributed to the remote source.
5. **Immediate actions:** Recommend at least four proportionate response steps. Include evidence preservation and account/session containment considerations.
6. **Scope limitations:** List at least two things that cannot be established from this authentication log alone. For example, do not claim data exfiltration, persistence or malware execution unless you have evidence for them.
7. **Further evidence required:** Name at least three additional log sources or artifacts you would request to continue the investigation.

Your recommendations should be practical. Do not recommend destructive actions before preserving relevant evidence.

---

## 5. Submission format

Submit one investigation report in Markdown or PDF.

Use the following structure:

```text
KAVACH-BT-001-Report/
├── report.md
├── timeline.md
└── commands-used.txt
```

Your report must contain:

- answers to Tasks A–G;
- the targeted-username count table;
- the correlated authentication evidence;
- the post-authentication command table;
- the incident timeline;
- your verdict, confidence and recommended actions;
- the commands or scripts used to reach your findings.

You may use `grep`, `awk`, `sort`, `uniq`, Python or other local analysis tools. Tool choice is not graded. The quality of your reasoning and evidence correlation is.

## 6. Scoring rubric

| Area | Points | What is assessed |
|---|---:|---|
| Task A — Baseline | 10 | Understanding of log types and normal activity |
| Task B — Authentication analysis | 20 | Correct aggregation, pattern recognition and reasoning |
| Task C — Authentication correlation | 15 | Correlation of source, account, timestamp and session |
| Task D — Post-authentication activity | 20 | Accurate command reconstruction and privilege interpretation |
| Task E — Noise handling | 10 | False-positive awareness and evidence limitations |
| Task F — Timeline | 10 | Chronological accuracy and supporting evidence |
| Task G — SOC handoff | 15 | Defensible verdict, containment and follow-up plan |
| **Total** | **100** | |

### Scoring principles

- A correct value without supporting evidence may receive partial credit.
- Unsupported claims reduce the score, even if the final verdict happens to be correct.
- Treating all failed logins or all successful logins as one incident will lose points.
- A strong report distinguishes **observed facts**, **reasonable inferences** and **unknowns**.
- Copying output from a single command without explaining its significance is not a complete investigation.

## 7. Completion criteria

A successful submission does more than identify an IP address. It demonstrates that the analyst can:

- establish a baseline from noisy authentication records;
- identify and quantify a suspicious pattern;
- correlate failed attempts with a later successful authentication;
- connect authentication evidence to subsequent privileged activity;
- build a defensible incident timeline;
- avoid overclaiming beyond the available evidence;
- communicate findings and recommend sensible next steps.

**The objective is not to find the suspicious line. The objective is to explain the incident using evidence.**

---

*End of participant challenge brief. This document intentionally contains no answer key or solution walkthrough.*
