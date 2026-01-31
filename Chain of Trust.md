# Chain of Trust

**Category:** Boot2Root  
**Author:** Astra  

---

## Write-up 

I began this challenge with access to a hardened Debian-based system used for internal operations. From the outset, there were no weak passwords, no brute-force opportunities, and no direct privilege escalation paths, which made it clear that this machine required a **chain-based exploitation approach**.

After gaining initial access, I performed thorough enumeration of the system. I inspected running processes, filesystem permissions, scheduled tasks, environment variables, and custom scripts to understand how execution contexts were structured. The system relied heavily on **implicit trust relationships** between components, rather than explicit security controls.

Individually, the misconfigurations I discovered were minor and not immediately exploitable. However, by carefully analyzing how one process trusted the output or behavior of another, I was able to chain these weaknesses together. This included abusing trusted execution paths, inherited permissions, and assumptions made by higher-privileged scripts about lower-privileged inputs.

By controlling these inputs and executing them in the correct sequence, I was able to break the intended trust boundaries. This incremental abuse of small mistakes eventually allowed me to escalate privileges and gain root access to the system.

Once root access was achieved, I retrieved the flag to confirm full system compromise.

---

## Final Flag
SECE{ch41n_th3_m1st4k3s_n0t_c0mm4nds}
