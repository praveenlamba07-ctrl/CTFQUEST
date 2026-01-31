# Simplistic

**Category:** Boot2Root  
**Author:** —  

---

## Write-up 

I began the **Simplistic** challenge by performing basic reconnaissance on the target machine. A web server was running on port 80, so I navigated to it in the browser. The homepage presented a minimal diagnostic tool called **NetDiag v1.0**, which appeared to test network connectivity by pinging a supplied IP address.

### Phase 1: Web Enumeration & Initial Access

Inspecting the functionality of the NetDiag tool, I noticed that it accepted an IP address as input and returned the output of a `ping` command. Through testing and source inspection, it became clear that the user input was passed directly into a shell command without any sanitization.

This indicated a **command injection vulnerability**. Since shell metacharacters were not filtered, I was able to append arbitrary commands to the ping execution.

Using the following payload in the IP input field:

The server executed both the ping command and the file read operation. This allowed me to retrieve the user flag directly from the filesystem.

---

## Phase 2: Privilege Escalation

With initial access confirmed, I focused on escalating privileges to root. After gaining a shell as the web user, I began system enumeration to identify potential misconfigurations.

One of the first checks I performed was searching for binaries with the **SUID bit** set. Running a standard SUID enumeration command revealed an unusual and dangerous configuration:


The `find` binary was configured with SUID permissions, meaning it would execute commands with root privileges. Since `find` supports the `-exec` option, this immediately presented a clear escalation path.

I exploited this misconfiguration by executing a shell via `find` while preserving elevated privileges:


This command spawned a root shell, confirming successful privilege escalation.

With root access obtained, I navigated to the root directory and retrieved the final flag.




---

## Summary

This challenge demonstrated how chaining **basic web vulnerabilities** with **poor system permission management** can lead to full system compromise:

- Unsanitized user input led to command injection
- SUID misconfiguration on a powerful binary enabled privilege escalation

Despite its simplicity, the challenge effectively reinforced core security principles such as input validation and the principle of least privilege.
final flag 
SECE{r00t_v14_su1d_f1nd}

