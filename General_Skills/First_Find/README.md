# First Find

**Problem:** Unzip an archive and locate a specific file named `uber-secret.txt` among many nested directories.

**Solution:**

1. Unzipped the archive:
```bash
unzip files.zip
```

2. Needed to locate a file by name without manually browsing every directory.

**For Linux users:**
```bash
find . -iname "uber-secret.txt"
```
- `.`: tells the command to start searching from the current directory.
- `-name`: matches the exact file name (case-sensitive).
- `-i` (as in `-iname`): makes the match case-insensitive.

**For Windows users (Command Prompt):**
```cmd
dir /s "uber-secret.txt"
```
- `/s`: searches the current directory and all subdirectories for the named file.

3. The command returned the full path to `uber-secret.txt`, which was opened to retrieve the flag:
```bash
cat ./path/to/uber-secret.txt
```

**Learned:** `find` (Linux/macOS) and `dir /s` (Windows) search by **filename**, while `grep -r` / `findstr /s` search by **file contents**. Knowing which tool fits the task — "I know the name" vs. "I know the text inside" — saves significant time when navigating large or unfamiliar file structures.

**Real-world relevance:** Quickly locating a specific file by name across a large filesystem is a routine forensics and incident-response task — for example, tracking down a known malicious filename, a dropped payload, or a specific log file during an investigation.