# Professor's Vault

**Category:** Web Exploitation (JWT)  
**Author:** Astra  

---

## Write-up (First Person)

I started this challenge by interacting with the web application themed around *La Casa de Papel*. The objective was clear: gain access to the vault, which was restricted exclusively to users with the **Professor** role. The hint *“Forged What ..?”* immediately suggested an issue related to **token forgery**, most likely involving JSON Web Tokens (JWT).

---

## Initial Reconnaissance

The application provided two main functionalities: user registration and login. I registered a new user and logged in successfully. After authentication, I was redirected to the `/profile` page, which displayed my account details:

- **Username:** testuser123  
- **Role:** hostage  

The page also clearly stated that vault access was restricted to the Professor, confirming that **role-based authorization** was enforced on the client side.

Inspecting the browser cookies revealed that authentication was handled using a **JWT**. I copied the token and decoded it to inspect its contents.

---

## JWT Analysis

Decoding the JWT payload revealed the following claims:

- `username`: testuser123  
- `role`: hostage  
- `secret_plan`: X0YGUAAwQPJ4chY9LPcIcgI8aQY8zelI9  
- `iat`: issued-at timestamp  

The JWT header indicated that the token was signed using the **HS256** algorithm. This meant the server relied on a shared secret key to verify token integrity.

The presence of the `secret_plan` field and the challenge hint strongly implied that the JWT secret was weak and possibly guessable.

---

## Exploitation: Weak JWT Secret

Based on the challenge theme, I suspected that the signing secret might be related to *La Casa de Papel*. I created a small custom wordlist containing common references from the series and attempted to brute-force the JWT secret.

By recomputing the HMAC-SHA256 signature using candidate secrets and comparing it against the original token signature, I was able to identify the correct signing key.

Once the secret was discovered, I forged a new JWT by modifying the payload and changing my role from `hostage` to `professor`. I then re-signed the token using the recovered secret.

---

## Gaining Vault Access

After replacing the original JWT in the browser cookies with the forged token, I refreshed the page and navigated to the vault endpoint. This time, access was granted successfully, confirming that the server trusted the role claim inside the JWT without additional verification.

Inside the vault, the flag was revealed.

---

## Final Flag

