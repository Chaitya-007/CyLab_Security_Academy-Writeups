#### Secret of the Polyglot — picoCTF 2024

**Category:** Forensics
**Difficulty:** Easy 

#### Overview

The provided file (flag2of2-final.pdf) is a polyglot file—a single file engineered to be valid in two different formats simultaneously. In this case, it functions as both a **PNG** image and a **PDF** document, with each format containing one half of the flag. 

#### Solution Steps

1. **Download the challenge file:** 

bash

wget <url>

Use code with caution.

Copy code text to clipboard.
2. **Check the file type:** 

bash

file flag2of2-final.pdf

Use code with caution.

Copy code text to clipboard.

*Output:* Identified as a PNG image data file despite its .pdf extension.
3. **Inspect metadata:** 

bash

exiftool flag2of2-final.pdf

Use code with caution.

Copy code text to clipboard.

*Output:* Standard PNG metadata only; no hidden flags or encoded strings found.
4. **Search for plain-text strings:** 

bash

strings flag2of2-final.pdf | grep "academy{"

Use code with caution.

Copy code text to clipboard.

*Output:* No matches returned.
5. **Extract the second half of the flag (PDF):**
Opened flag2of2-final.pdf in a standard PDF viewer, which displayed the second half of the flag.
6. **Extract the first half of the flag (PNG):**
Renamed/saved the file with a .png extension (flag2of2-final.png) and opened it in an image viewer, revealing the first half of the flag.
7. **Combine both halves:**
Joined the first half from the PNG image with the second half from the PDF document to obtain the complete flag.