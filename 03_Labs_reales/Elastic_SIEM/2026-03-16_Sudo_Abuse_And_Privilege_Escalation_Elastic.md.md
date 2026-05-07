**Date:** 2026-03-13 **Tool:** Atomic Red Team + Elastic SIEM (Auditd Manager) **Status:** Detected ✅

**Evidence:**

- `process.title`: sh -c sudo -l; sudo cat /etc/sudoers; sudo vim /etc/sudoers
- `user.name`: nacho
- `user.effective.name`: root ⚠️
- `process.working_directory`: /tmp
- `file.mode`: 4755 (SUID bit)
- `@timestamp`: 2026-03-16T07:43:16Z

**MITRE:**

- Tactic: Privilege Escalation
- Technique: T1548.003 - Abuse Elevation Control Mechanism: Sudo

**Severity:** High. User nacho escalated to root via sudo abuse. Reading and attempting to modify /etc/sudoers indicates privilege enumeration and potential persistence attempt.

**Lesson learned:** The key indicator for privilege escalation via sudo is the difference between user.name and user.effective.name. When these two fields differ, a privilege escalation occurred. Combined with execution from /tmp and access to /etc/sudoers, this is a confirmed high severity incident.