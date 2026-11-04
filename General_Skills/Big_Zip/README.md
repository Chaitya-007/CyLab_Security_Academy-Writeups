# Big Zip

**Problem:** Unzip an archive containing many nested directories and files, and find the flag without checking each file by hand.

**Solution:**

1. Unzipped the archive:
```bash
unzip big-zip-files.zip
```

2. The extracted archive had many directories and sub-directories, each containing numerous files — far too many to search manually by opening each one.

3. Needed a way to search recursively through all files and subdirectories for the flag's format (e.g. `academy{}`):

**For Linux users:**
```bash
grep -ri "your_search_term" /path/to/directory
```
To search recursively, use the `-r` (or `-R`) flag. The basic syntax is `grep -r "your_search_term" /path/to/directory`.
- `-r` (or `-R`): searches recursively through all subdirectories.
- `-i`: ignores text case, making the search case-insensitive.
- `"your_search_term"`: the text pattern to search for (e.g. `academy{`).
- `/path/to/directory`: the directory to search in (use `.` for the current directory).

**For Windows users (Command Prompt):**
```cmd
findstr /s /i "your_search_term" *.*
```
- `/s`: searches the current directory and all subdirectories (equivalent to `grep -r`).
- `/i`: ignores case during the search (equivalent to `grep -i`).
- `"your_search_term"`: the text string to search for.
- `*.*`: targets all file types in the search location.

4. The search returned the file path containing the match, which was opened directly to retrieve the flag.

**Learned:** Recursive text search is the key tool for navigating large, deeply nested file structures. `grep -r` (Linux/macOS) and `findstr /s` (Windows) both solve this, searching every file in every subdirectory for a pattern instead of relying on manual exploration.

**Real-world relevance:** Recursive searching across large filesystems is a core skill in incident response and forensics — for example, hunting for an IOC (indicator of compromise), a malicious string, or a leaked credential across thousands of log files or disk images.