**Date:** 2026-03-13 **Tool:** Atomic Red Team + Elastic SIEM (Auditd Manager) **Status:** Detected ✅

##### **Description:**
 
The attacker established persistence by appending a malicious command to the user's .bash_profile file. This command would execute automatically every time the user logs in, providing persistent code execution without requiring elevated privileges.

**Evidence:**

- `file.path`: /home/nacho/.bash_profile
- `process.title`: sh -c echo 'echo "Hello from Atomic Red Team T1546.004" > /tmp/T1546.004' >> ~/.bash_profile
- `process.working_directory`: /tmp ⚠️
- `auditd.data.syscall`: openat
- `event.action`: opened-file
- `tags`: bash_profile_modified
- `user.name`: nacho
- `@timestamp`: 2026-03-13T06:59:54Z

**MITRE:**

- Tactic: Persistence
- Technique: T1546.004 - Event Triggered Execution: .bash_profile and .bashrc

**Severity:** High. Modification of shell profile files allows persistent execution on every user login without elevated privileges.

**IOCs:**

- Write access to /home/user/.bash_profile or .bashrc
- openat syscall on shell profile files
- sh spawned from /tmp writing to profile files
- tag: bash_profile_modified

**Lesson learned:** Without specific file watch rules using auditctl -w, this modification was completely invisible in Elastic. After adding the watch rule, the openat syscall was captured immediately. This highlights that detection coverage is entirely dependent on audit rules configured. In production, monitoring shell profile files should be a baseline rule in any Linux environment.