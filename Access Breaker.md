# Access Breaker

**Category:** Reversing  
**Author:** Astra  

---

## Write-up (First Person)

When I began this challenge, I was given an unknown binary that required a secret key to grant access. The description hinted that the program was honest in its logic but deliberately unclear in how it revealed the correct input, which strongly suggested a reversing-based solution.

I started by performing basic reconnaissance on the binary. Using standard analysis techniques, I examined the strings and overall structure to understand how user input was being handled. This revealed that the program compared the provided key against an internally generated value rather than a hardcoded string.

Next, I analyzed the control flow of the program to determine how the key was validated. By stepping through the relevant functions and observing the transformations applied to the input, I was able to reverse the logic and reconstruct the expected key. The operations were simple but intentionally obscured to discourage guessing, matching the challenge’s hint that the program “doesn’t speak plainly.”

Once the transformation logic was understood, deriving the correct input became straightforward. Supplying the reconstructed key to the binary resulted in successful access being granted.

---

## Final Flag
SECE{rev4fun_2025}
