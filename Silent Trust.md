# Silent Trust

**Category:** Boot2Root  
**Author:** Astra  

---

## Write-up 

I began this challenge by launching the provided virtual machine image in a VM manager. I used **virt-manager**, but any virtualization tool that allows local access to the system would be sufficient.

At first glance, the system did not expose any network services or obvious attack vectors. This suggested that the intended approach was **local analysis and misconfiguration abuse**, rather than remote exploitation.

---

## Step 1: Initial Access and Enumeration

After gaining basic access to the system, I focused on standard local enumeration. I checked running processes, installed binaries, permissions, and security configurations. Since traditional privilege escalation methods such as weak passwords or sudo misconfigurations were not present, I expanded my enumeration to include **Linux capabilities**.

Linux capabilities allow binaries to perform privileged operations without granting full root access. These are often overlooked but can be extremely powerful when misconfigured.

---

## Step 2: Identifying Dangerous Capabilities

While inspecting binaries with extended capabilities, I discovered a binary that had been assigned elevated capabilities. Although it was not running as root, the assigned capabilities allowed it to perform actions normally restricted to privileged users.

This created a silent trust boundary: the system trusted the binary more than the user, even though it could be influenced or abused.

---

## Step 3: Privilege Escalation via Capabilities

By abusing the granted capabilities, I was able to execute privileged operations and escalate my access. Unlike password-based escalation, this method bypassed authentication entirely and relied purely on capability misuse.

Once exploited correctly, this allowed me to gain full root access on the system.

---

## Step 4: Retrieving the Flag

With root privileges obtained, I navigated to the root directory and located the flag file:


Reading this file revealed the final flag.

---

## Final Flag

SECE{capabilities_are_stronger_than_passwords}
