# Hidden in Plainsight

**Category:** Forensics · **Difficulty:** Easy

**Problem:** Given a seemingly ordinary JPG image, discover a hidden payload tucked inside it and extract the flag.

**Solution:**

1. Inspected the image's metadata for anything unusual:
```bash
exiftool image.jpg
```
`exiftool` reads embedded metadata fields (Comment, Author, GPS data, etc.) that aren't visible when simply viewing the image. The `Comment` field contained a Base64-encoded string: c3RlZ2hpZGU6Y0VGNmVuZHZjbVE9

2. Decoded the first Base64 string:
```bash
echo "c3RlZ2hpZGU6Y0VGNmVuZHZjbVE9" | base64 -d
```
This revealed a `steghide:` prefix followed by a second, nested Base64-encoded passphrase: steghide:cEF6endvcmQ=

3. Decoded the second (inner) Base64 string to get the actual passphrase:
```bash
echo "cEF6endvcmQ=" | base64 -d
```
Output: `pAzzword`

4. Used `steghide` with the image and the recovered passphrase to extract the hidden payload:
```bash
steghide extract -sf "img.jpg" -p "pAzzword"
```
This extracted the hidden file, which contained the flag.

**Learned:** Steganography hides data *inside* a file's structure (not just its metadata) in a way that's invisible to the eye and often password-protected. Metadata fields like `Comment` are a common place attackers or challenge authors leave a clue or a layered hint (here, Base64 nested inside Base64) pointing toward the actual hidden payload and its passphrase.

**Real-world relevance:** Steganography and metadata inspection are core forensic techniques — malware and data exfiltration sometimes hide payloads inside innocuous-looking image files, and `exiftool` + `steghide` are standard tools in a forensic analyst's toolkit for uncovering them.