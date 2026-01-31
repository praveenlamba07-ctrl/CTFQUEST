# Shadow Backup

**Category:** Boot2Root  
**Author:** Astra  

---

## Write-up (First Person)

I started this challenge by booting the provided virtual machine using a VM manager. I used **virt-manager**, though any virtualization tool that allows interaction with the bootloader would work.

From the description and the nature of the challenge, it was clear that this machine was vulnerable due to a **local misconfiguration**, rather than any network-based issue.

---

## Step 1: Accessing the System

After starting the VM, I accessed the **GRUB boot menu** and edited the default boot entry. In the line that begins with `linux`, I appended the following parameter:


Booting with this option caused the system to skip the normal initialization process and start directly with a **root shell**, without requiring authentication.

---

## Step 2: Preparing the Filesystem

Initially, the root filesystem was mounted as read-only. To allow modifications, I remounted it with write permissions:


This gave me full control over the system.

---

## Step 3: Privilege Confirmation

Since the system was already running as root due to the modified boot process, I proceeded to locate the root flag without needing further privilege escalation.

---

## Step 4: Retrieving the Flag

I navigated to the root directory and located the flag file:


Reading this file revealed the final flag.

---

## Final Flag

SECE{sudo_secure_path_is_not_your_friend}
