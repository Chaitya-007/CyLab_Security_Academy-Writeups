# Static Ain't Always Noise

**Category:** General Skills · **Difficulty:** Easy

**Problem:** A binary file named `static` is given, along with a bash script `ltdis.sh`. Find the flag hidden somewhere inside the binary.

**Solution:**

### 1. First, understand what the given script actually does

Before running anything blindly, I read through `ltdis.sh` line by line:

```bash
objdump -Dj .text $1 > $1.ltdis.x86_64.txt
```
This runs `objdump`, a tool that **disassembles** a binary — it converts the compiled machine code back into human-readable assembly instructions. The `-D` flag disassembles everything, and `-j .text` tells it to only show the `.text` section, which is the part of the binary that actually contains the program's executable code. The output is saved into a `.txt` file.

```bash
strings -a -t x $1 > $1.ltdis.strings.txt
```
This runs `strings`, a tool that extracts all readable (printable) text from a binary file — things like hardcoded messages, file paths, or flags. The `-t x` flag also prints the **file offset** (position) of each string in hexadecimal, which helps locate exactly where in the file that string lives.

So in plain terms: this script takes a binary and produces two reports — one showing its assembly code, and one showing any readable text buried inside it.

### 2. Run the script on the given binary

```bash
chmod +x ltdis.sh
./ltdis.sh static
```

This created two files:
- `static.ltdis.x86_64.txt` — the disassembly
- `static.ltdis.strings.txt` — the extracted strings

### 3. Think about where the flag is likely to be

A CTF flag is just a piece of text (like `picoCTF{...}`), and text like that shows up in `strings` output, not really in raw assembly instructions. So instead of reading through pages of disassembly, I checked the strings file first.

### 4. Look through the strings output

```bash
cat static.ltdis.strings.txt
```

Scrolling through, most of it was normal binary "noise" — library names, symbol names, section headers like `.text`, `.rodata`, etc. But one line stood out, clearly in flag format:

**Shortcut:** The same result could've been reached without the script at all, just by running:
```bash
strings static
```
`strings` alone already does step 2's text-extraction job; the disassembly step wasn't actually needed to find this particular flag.

**Learned:**
- `strings` pulls out any readable text embedded in a compiled binary, which is often enough to find flags, hardcoded secrets, or hints without ever running the program.
- `objdump -D` shows the actual assembly instructions, useful when you need to understand program *logic*, not just find text.
- Always read a provided script first before running it blindly — understanding *what* a tool does helps you decide whether you even need its full output, or if a simpler command gets you there faster.

**Real-world relevance:** Static analysis — inspecting a binary without executing it — is a core malware-analysis technique. Analysts routinely use `strings` as a first pass to spot hardcoded IPs, URLs, or suspicious text before deciding whether deeper (and riskier) dynamic analysis is needed.