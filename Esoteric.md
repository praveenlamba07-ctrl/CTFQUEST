# Esoteric

**Category:** Steganography  
**Author:** Astra  

---

## Write-up 

I started this challenge by carefully reading the description. It clearly mentioned that nothing should be ignored, including the **title and description**, which immediately suggested that the password or clue might be hidden in plain sight. The challenge also provided a long encoded-looking string inside the flag format, indicating multiple layers of hiding.

---

## Step 1: Extracting the Files

The challenge provided a ZIP file named `images.zip`. Based on the hint that the **title would help**, I tried using the title **“esoteric”** as the password. This worked, and I was able to extract the contents of the archive.

---

## Step 2: Metadata Analysis

Next, I examined the image metadata. Inside one of the metadata fields, I noticed a sequence of hexadecimal values separated by dots:

I converted these hexadecimal values into ASCII:

- 63 → c  
- 72 → r  
- 40 → @  
- 63 → c  
- 6b → k  
- 5f → _  
- 6d → m  
- 33 → 3  

This decoded to:


This looked like a password rather than a message.

---

## Step 3: Steganography Extraction

Using the decoded value `cr@ck_m3` as a password, I ran a steghide extraction on the image file. This successfully extracted a file named `dict.txt`.

---

## Step 4: Dictionary Mapping

The extracted `dict.txt` contained a custom substitution dictionary mapping letters to unusual words. For example:

- H → giffo  
- E → itach  
- L → zillo  
- O → miitai  
- S → varal  
- _ → ou  
- D → chou  
- I → jit  
- R → monk  

---

## Step 5: Decoding the Flag Text

I then took the encoded string provided in the challenge description and mapped each word back to its corresponding character using the dictionary.

After completing the full mapping, the decoded message became:


---

## Final Flag 
SECE{HELLO_SOLDIER}


---

## Conclusion

This challenge relied entirely on **careful observation and layered decoding**. By paying attention to the title, analyzing metadata, extracting hidden files, and applying a custom dictionary, I was able to uncover the hidden message. The key lesson was to never ignore descriptive hints, as every detail mattered in solving the challenge.


