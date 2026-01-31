# Cyber Sync

**Category:** Boot2Root  
**Author:** —  

---

## Write-up 

I started this boot2root challenge by analyzing the provided system image. The target appeared to be a Linux host with no immediately obvious external attack surface, which suggested that the intended solution would rely on local enumeration and abuse of internal trust relationships.

After gaining initial low-privilege access, I focused on standard enumeration techniques. I examined running services, user permissions, scheduled tasks, environment variables, and installed software. During this process, I noticed that Python was being used extensively by internal scripts executed in higher-privileged contexts.

Further inspection revealed a misconfiguration in how Python libraries were being loaded. A writable directory was included in the Python module search path for a script executed with elevated privileges. This allowed me to place a malicious Python module with the same name as a legitimate library, effectively hijacking the import process.

By crafting a malicious Python library and ensuring it was imported by the privileged script, I was able to execute arbitrary code as root. This technique, known as **Python library hijacking**, allowed me to bypass normal privilege boundaries without exploiting any traditional vulnerability.

Once the malicious module was executed, I gained a root shell and confirmed full compromise of the system. I then retrieved the root flag as proof of successful exploitation.

---

## Final Flag
SECE{Pyth0n_L1b_H1j4ck_1s_P0w3rful!}


