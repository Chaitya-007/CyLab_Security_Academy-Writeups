# Corrupted File

**Category:** Forensics · **Difficulty:** Easy

**Problem:** A given file appears "broken." Figure out why, and fix it to recover the flag.

**Solution:**

1. Downloaded the file:
```bash
wget https://challenge-files.picoctf.net/<path>/file
```

2. Checked what type of file it was:
```bash
file file
```
Output: `data` — meaning the file's type couldn't be identified. This usually points to a corrupted or incorrect file **header** (the "magic bytes" at the start of a file that identify its type).

3. Ran `strings` to look for any readable clues:
```bash
strings file
```
The output included `JFIF` near the top — a strong indicator that this is actually a **JPEG image** (JFIF is a common JPEG-based format), even though the file extension/type wasn't recognized.

4. Knowing JPEG files should start with the magic bytes `FF D8 FF E0` (or `E1`) and end with `FF D9`, opened the file in a hex editor to inspect and fix the header:
```bash
hexeditor file
```

**Or you can use online hex editors like:** [https://hexed.it/](https://hexed.it/)

5. Found the first bytes were incorrect — `5C 78 FF E0` instead of the expected JPEG signature. Edited the first two bytes to `FF D8`, matching proper JPEG convention. Checked the trailing bytes too, and confirmed they already correctly ended in `FF D9`.

6. Saved the changes (`Ctrl+X`, then Enter to keep the same filename).
[For using online hex editor, export and save it as file.jpeg]

7. Re-checked the file type to confirm the fix worked:
```bash
file file
```
Output: `JPEG image data, JFIF standard 1.01, ...` — now correctly recognized as a JPEG.

8. Opened the repaired image to view it and find the flag:
```bash
xdg-open file
```
The flag was visible directly in the image.
[You can also directly open the file in your system's image viewer.]

Keep this as reference :

| File Format | Hexadecimal Signature | ASCII Translation |
|---|---|---|
| PDF Document | `25 50 44 46 2D` | `%PDF-` |
| PNG Image | `89 50 4E 47` | `.PNG` |
| JPEG Image | `FF D8 FF` | (Non-printable characters) |
| ZIP Archive | `50 4B 03 04` | `PK..` (Named after Phil Katz, creator of ZIP) |
| GIF Image | `47 49 46 38` | `GIF8` |


**Learned:** A file's **magic bytes** (the first few bytes of a file) determine how the OS and tools identify its type — not the file extension. Corrupting or altering just these first bytes is enough to make a perfectly valid file appear unreadable or unknown. Tools like `file` (identifies type), `strings` (extracts readable text clues), and `hexeditor` (lets you view/edit raw bytes) together let you diagnose and repair this kind of corruption.

**Real-world relevance:** Recognizing and repairing corrupted or deliberately altered file headers is a real forensic skill — malware authors and attackers sometimes disguise files by altering magic bytes to evade file-type detection or security filters, and analysts need to be able to identify a file's true type regardless of its apparent extension or header state.