# Pick One

**Category:** Infra  
**Author:** captain_mj  

---

## Write-up 

I began this challenge by examining the provided build artifact that had been exported as part of a backup process. The description immediately suggested a common infrastructure mistake: assuming that deleting sensitive data during a build process permanently removes it from the final artifact.

After extracting the contents of the file, I noticed that it was not a simple archive but an exported container image. This indicated that the artifact preserved the full layer history created during the build process.

I inspected the image metadata and layer structure to understand how it was assembled. By reviewing the build history, I observed that a file containing sensitive data had been copied into the image during an earlier build step and then removed in a later step. While the file no longer appeared in the final filesystem view, I knew that container layers are immutable.

Digging into the earlier layers confirmed this suspicion. The supposedly deleted file was still present in one of the lower layers of the image. This demonstrated a classic container security pitfall: removing a file in a later layer does not erase it from the image’s history.

Recovering the file from the affected layer revealed the hidden flag, confirming that sensitive data had been unintentionally preserved in the exported artifact.

---

## Final Flag
SECE{layers_never_forget}
