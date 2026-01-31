# Crypto Vault

**Category:** Web  
**Author:** Astra  

---

## Write-up 

I started this challenge by visiting the provided URL. The web application was named **CryptoVault** and presented itself as a secure message storage service. The goal was to retrieve the flag in the `SECE{}` format.

From the beginning, the hint *“The lame old trick!”* suggested that the vulnerability would be something very common and often overlooked.

---

## Phase 1: Web Enumeration and SQL Injection

The application contained a login form that required a username and password. Since no valid credentials were provided, I tested the login functionality for basic input validation issues.

I quickly identified that the login form was vulnerable to **SQL Injection**, as user input was directly used in a backend SQL query without proper sanitization.

To bypass authentication, I entered the following payload in the username field:


I entered any value in the password field.

This payload modified the SQL query in such a way that the condition always evaluated to true, effectively bypassing the authentication check. As a result, I was logged in as an administrative user.

---

## Phase 2: Accessing Encrypted Data

After logging in, I gained access to the admin dashboard. An option labeled **“Admin: View All Notes”** was available, which exposed multiple encrypted messages belonging to different users.

Each note was Base64-encoded and appeared to be part of a larger encrypted message. These ciphertexts were clearly intended to be combined to form the final flag.

---

## Phase 3: Cryptanalysis (Repeating-Key XOR)

The challenge description mentioned multiple layers of encryption, but the structure of the ciphertexts suggested a **repeating-key XOR cipher**.

Since the flag format was known (`SECE{...}`), I used a **known-plaintext attack**. I assumed that the first decrypted message would begin with `SECE{`, and used this to recover the XOR key by XORing the decoded ciphertext with the expected plaintext.

Using this method, I successfully recovered the repeating XOR key:


---

## Phase 4: Decrypting the Flag

With the key identified, I decoded all Base64 ciphertexts and applied the repeating-key XOR decryption to each one. Each decrypted segment formed part of the final flag.

After concatenating all decrypted segments, I obtained the complete flag.

---

## Final Flag

SECE{w3lc0m3_t0_th3_cr7pt0_v4ult_0f_s3cr3ts_4nd_h1dd3n_m3ss4g3s_m4st3r_h4ck3r}
