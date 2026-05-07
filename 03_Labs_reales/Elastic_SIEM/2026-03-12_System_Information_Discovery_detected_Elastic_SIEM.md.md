**Date:** 2026-03-13 **Tool:** Atomic Red Team + Elastic SIEM (Auditd Manager) **Status:** Detected ✅

#### **Description:** 

The attacker executed system reconnaissance commands after compromising the host. Commands like uname, hostname and lsmod were used to gather information about the operating system, kernel version and loaded modules.

**Evidence:**

- `process.name`: uname, hostname
- `process.args`: uname -a
- `process.working_directory`: /tmp ⚠️
- `auditd.data.syscall`: execve
- `event.action`: executed
- `user.name`: nacho
- `@timestamp`: 2026-03-13T05:20:25Z

**MITRE:**

- Tactic: Discovery
- Technique: T1082 - System Information Discovery

**Severity:** Low in lab context, Medium in production because working directory /tmp is abnormal for legitimate processes.

**IOCs:**

- Execution from /tmp
- uname -a executed by interactive user
- hostname executed via sh -c from PowerShell parent process

**Lesson learned:** Auditd without execve rules does not capture process execution. After adding the rules, all commands were visible in Elastic. The process.title field showed the full execution chain including parent process PowerShell spawning sh which spawned the discovery commands.