# Tar Pit

**Category:** Boot2Root  
**Author:** Harper  

---

## Write-up 

When I started this challenge, I was given access to a Linux host that appeared properly configured on the surface. There were no immediately exposed services or obvious vulnerabilities, which indicated that the challenge would require **thorough enumeration and attention to detail**.

After obtaining initial low-privilege access, I began standard Linux enumeration. I checked user permissions, running processes, cron jobs, SUID binaries, and sudo rules. This aligned well with the challenge description, which emphasized mismanaged development and maintenance environments.

During this process, I discovered a subtle but critical misconfiguration: the current user was allowed to run the `tar` binary with **sudo privileges**. While `tar` may appear harmless, it is a known living-off-the-land binary that can be abused to execute arbitrary commands when run as root.

Using this sudo permission, I crafted a `tar` command that executed a shell with elevated privileges. Since the command was executed through `sudo`, this resulted in an immediate privilege escalation to root.

With root access achieved, the system was fully compromised, and I was able to retrieve the final flag.

---

## Final Flag
SECE{b2r_sudo_tar_pwned}
