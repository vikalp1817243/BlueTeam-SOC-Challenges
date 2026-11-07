# KAVACH-BT-001: The Login That Shouldn't Have Happened

**Difficulty:** Easy  
**Category:** Linux Log Analysis · Authentication Monitoring  
**Challenge ID:** KAVACH-BT-001

## Scenario

Your organization's Ubuntu server has triggered a security alert following unusual SSH authentication activity. You have been provided with an authentication log file containing routine system activity as well as potentially suspicious events.

Investigate the activity and answer the following questions using the supplied evidence.

**Evidence file:** `evidence/kavach_01_auth.log`

---

## Challenge questions

### Q1. Which IP address generated the highest number of failed SSH login attempts?

**Answer:**  
_Write your answer here._

**Hidden**

- **Hint 1:** `Failed password`
- **Hint 2:** Group events by source IP

---

### Q2. How many failed SSH login attempts originated from the IP address identified in Q1?

**Answer:**  
_Write your answer here._

**Hidden**

- **Hint 1:** Count matching failures
- **Hint 2:** Filter by the identified IP

---

### Q3. Which username was targeted most frequently by the suspicious IP address?

**Answer:**  
_Write your answer here._

**Hidden**

- **Hint 1:** Examine usernames
- **Hint 2:** Compare frequency per account

---

### Q4. Which username successfully authenticated from the suspicious IP address?

**Answer:**  
_Write your answer here._

**Hidden**

- **Hint 1:** Look for `Accepted password`
- **Hint 2:** Correlate the source IP

---

### Q5. At what exact timestamp did the successful SSH authentication occur?

**Answer:**  
_Write your answer here._

**Hidden**

- **Hint 1:** Use the successful login record
- **Hint 2:** Check the timestamp at the start of the line

---

### Q6. What was the source port used during the successful SSH authentication?

**Answer:**  
_Write your answer here._

**Hidden**

- **Hint 1:** Inspect the same login record
- **Hint 2:** Find the value after `port`

---

### Q7. What was the first `sudo` command recorded for the authenticated account after the successful login?

**Answer:**  
_Write your answer here._

**Hidden**

- **Hint 1:** Search for `sudo:`
- **Hint 2:** Check the earliest matching timestamp

---

### Q8. How many distinct `sudo` commands were recorded for the authenticated account after the successful login?

**Answer:**  
_Write your answer here._

**Hidden**

- **Hint 1:** Focus on the authenticated account
- **Hint 2:** Count unique command paths

---

### Q9. How much time elapsed between the successful SSH authentication and the first recorded `sudo` command?

**Answer:**  
_Write your answer here._

**Hidden**

- **Hint 1:** Compare the two timestamps
- **Hint 2:** Calculate the time difference

---

### Q10. Based on the authentication logs, what is the most likely security incident? Identify the key evidence, and state what the logs cannot conclusively attribute.

**Answer:**  
_Write your answer here._

**Hidden**

- **Hint 1:** Reconstruct the event sequence
- **Hint 2:** Correlate failures, login success, and sudo activity

---

## Want to level up?

### SOC Analyst Challenge — Incident Investigation

Think you have solved the questions? Take your investigation further.

Use the detailed [SOC lab challenge](soc-lab-challenge.md). Investigate the complete log dataset, reconstruct the incident timeline, distinguish suspicious activity from normal system activity, and prepare a professional incident report.

Your report can then be submitted to the designated AI evaluator using the evaluation prompt provided by the organizers. The evaluator will assess your findings and award a score out of **100**.

**Your objective:** Think like a SOC analyst, not just someone running Linux commands.

---

## Submission guidance

- Base your answers on the supplied log file.
- Include relevant log evidence wherever possible.
- Use timestamps exactly as recorded in the dataset.
- Do not make claims that the supplied logs cannot establish.
- For Q10, explain the evidence behind your assessment rather than giving only an incident label.
