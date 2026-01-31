# Crypto Vault

**Category:** Web  
**Author:** —  

---

## Write-up (First Person)

I started this challenge by visiting the provided URL. At first glance, the webpage appeared extremely simple and almost useless, which immediately aligned with the hint: *“The lame old trick!”*. This suggested that the vulnerability was something very basic and often overlooked rather than a complex web exploit.

Keeping the second hint in mind — *“Maybe search for something that could help”* — I avoided overthinking the challenge and focused on classic web enumeration techniques. Instead of attacking inputs or looking for hidden parameters, I checked for files that developers commonly forget to secure.

One of the first things I tried was accessing `robots.txt`. This is a well-known but frequently ignored file that often reveals sensitive or hidden paths meant to be excluded from search engines but still accessible to users.

The `robots.txt` file immediately revealed a hidden directory related to the application. Navigating to that directory exposed content that was not intended to be publicly visible. Inside, I found the flag directly embedded within the page, confirming that the challenge relied on a simple but effective enumeration trick.

This perfectly matched the challenge’s theme: the trick was old, simple, and easy to miss — but extremely effective if you know where to look.

---

## Final Flag
SECE{w3lc0m3_t0_th3_cr7pt0_v4ult_0f_s3cr3ts_4nd_h1dd3n_m3ss4g3s_m4st3r_h4ck3r}
