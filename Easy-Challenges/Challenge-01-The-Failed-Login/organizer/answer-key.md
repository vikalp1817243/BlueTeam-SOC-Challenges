# KAVACH-BT-001 — Organizer Reference Answer Key

**CONFIDENTIAL — ORGANIZER / EVALUATOR ONLY**  
Do not distribute this file to participants.

## Verified reference answers

| Question | Expected answer | Marks |
|---|---|---:|
| Q1 | `203.0.113.42` | 10 |
| Q2 | 35 failed SSH password attempts from `203.0.113.42` | 10 |
| Q3 | `deploy`, targeted 11 times in failed password attempts from that IP | 10 |
| Q4 | `deploy` | 10 |
| Q5 | May 14 at `09:25:14` (year and timezone are not specified in the supplied log) | 10 |
| Q6 | Source port `45390` | 5 |
| Q7 | `/usr/bin/id` | 10 |
| Q8 | 4 distinct sudo command values | 10 |
| Q9 | 1 minute 49 seconds | 10 |
| Q10 | Suspected SSH password-guessing/brute-force activity followed by successful password authentication; later `deploy` privileged command activity is suspicious but cannot be conclusively attributed to the remote source | 15 |
| | **Total** | **100** |

## Q3 — Failed-attempt distribution from `203.0.113.42`

| Username | Failed attempts |
|---|---:|
| deploy | 11 |
| oracle | 7 |
| test | 6 |
| root | 6 |
| ubuntu | 3 |
| backup | 1 |
| admin | 1 |
| **Total** | **35** |

## Q4–Q6 — Successful authentication

```text
May 14 09:25:14 ubuntu-server sshd[1198]: Accepted password for deploy from 203.0.113.42 port 45390 ssh2
```

Related session-open record:

```text
May 14 09:25:16 ubuntu-server sshd[1198]: pam_unix(sshd:session): session opened for user deploy(uid=1002) by (uid=0)
```

## Q7–Q9 — Subsequent sudo records

| Timestamp | Account | Target user | Working directory | Command |
|---|---|---|---|---|
| 09:27:03 | deploy | root | `/home/deploy` | `/usr/bin/id` |
| 09:27:19 | deploy | root | `/home/deploy` | `/usr/bin/whoami` |
| 09:28:02 | deploy | root | `/home/deploy` | `/usr/bin/uname -a` |
| 09:29:41 | deploy | root | `/home/deploy` | `/usr/bin/last` |

Elapsed time:

- Successful authentication: `09:25:14`
- First recorded sudo command: `09:27:03`
- Difference: **1 minute 49 seconds**

## Q10 — Expected reasoning

The evidence supports this sequence:

1. The source `203.0.113.42` generated 35 failed SSH password attempts.
2. The same source later successfully authenticated using a password for `deploy`.
3. The SSH session opened for `deploy`.
4. The SSH session then records a disconnect at `09:25:25`.
5. Four later sudo command records are attributed to `deploy`, each invoking commands with target user `root`.
6. The commands (`id`, `whoami`, `uname -a`, and `last`) are consistent with basic account/system reconnaissance, but the records do not contain a session ID or remote source IP that links them to the earlier SSH connection.

Suggested assessment: **Suspected SSH password guessing/brute-force activity followed by successful account access. Later privileged activity by `deploy` is suspicious and temporally associated, but is not conclusively attributable to the remote source from this log alone.**

## Evidence limitations — important for fair grading

Do not accept or require claims beyond what this dataset establishes:

- The logs do not identify the human or system operator behind the source IP.
- The logs do not establish how the password was obtained.
- The logs do not prove that the sudo commands completed successfully.
- The logs do not establish persistence, malware execution, lateral movement, data theft, or exfiltration.
- The logs do not provide a year or timezone for the timestamps.
- A sudo record does not itself contain the remote source IP. Correlation should use account, timestamps, session context, and event sequence.
- The successful SSH session from `203.0.113.42` records a disconnect at `09:25:25`, before the first `deploy` sudo command at `09:27:03`. The log has no session identifier that links those later commands to that SSH connection.
- Do not treat all failed logins or all successful public-key logins as malicious.

## Scoring guidance for Q10

Award full marks when the participant:
- Identifies the suspicious source and repeated failures.
- Correlates the later successful password authentication to the same source.
- Identifies `deploy` as the authenticated account.
- Connects the subsequent sudo records to `deploy` and the timeline.
- Gives a cautious incident assessment and clearly separates facts from hypotheses.

Award partial marks for a correct general assessment with incomplete correlation. Deduct for unsupported certainty, incorrect attribution, or claims of persistence/exfiltration without evidence.
