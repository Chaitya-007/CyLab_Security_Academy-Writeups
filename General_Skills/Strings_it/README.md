# strings it

**Problem:** Find the flag inside a binary file named `strings`, without executing it.

**Solution:**

1. Downloaded the file and used the `strings` command to extract all human-readable text from it:
```bash
strings strings
```
`strings` scans a binary file and prints any sequence of printable characters it finds, which is useful for pulling readable data (like flags, URLs, or error messages) out of a compiled program without running it.

2. The output was long and full of unrelated readable text, so it needed to be narrowed down. Piped it through `grep` to search for the flag's known prefix:
```bash
strings strings | grep "academy{"
```

3. This isolated the matching line, which contained the flag.

**Learned:** `strings` is a safe way to inspect a binary's embedded text without executing it, which matters when the file's behavior is unknown or potentially malicious. Combining it with `grep` for a known flag format (or any known pattern) turns a wall of output into a single relevant line.

**Real-world relevance:** This is a standard first step in static malware analysis — running `strings` on a suspicious binary before ever executing it, to spot hardcoded IPs, URLs, file paths, or other IOCs without risking detonation of the payload.