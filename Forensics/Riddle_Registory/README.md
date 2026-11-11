# Riddle Registry

**Category:** Forensics · **Difficulty:** Easy

**Problem:** A PDF file looks like garbled nonsense, but a flag is hidden within its metadata.

**Solution:**

1. Inspected the PDF's metadata using `exiftool`:
```bash
exiftool confidential.pdf
```

2. The **Author** field contained an encoded string rather than a normal name.

3. Decoded the string (Base64) to reveal the flag:
```bash
echo "<encoded_string_from_Author_field>" | base64 -d
```

**Learned:** PDF metadata fields (Author, Title, Creator, Producer, etc.) can hold arbitrary text, including encoded data that isn't visible when simply opening the document. `exiftool` works across many file formats, not just images, making it a go-to first step whenever a challenge mentions "hidden" or "metadata."

**Real-world relevance:** Document metadata often leaks more than intended — author names, software versions, internal usernames, file paths, or even hidden revision history. Checking metadata is a routine step in both forensic investigations and OSINT reconnaissance (e.g. metadata scraped from publicly posted PDFs can reveal internal usernames or software versions used by an organization).