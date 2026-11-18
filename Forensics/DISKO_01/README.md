# DISKO 1

**Category:** Forensics · **Difficulty:** Easy

**Problem:** Find the flag inside a given disk image file.

**Solution:**

1. Downloaded the disk image:
```bash
wget https://artifacts.picoctf.net/c/538/disko-1.dd.gz
```

2. Unzipped it (the `.gz` extension means it's gzip-compressed):
```bash
gunzip disko-1.dd.gz
```

3. After unzipping, the file `disko-1.dd` was a raw disk image.

4. Extracted readable text from the disk image and filtered for the flag's prefix:
```bash
strings disko-1.dd | grep picoCTF
```

**Learned:** `strings` dumps *every* readable text string in a file, which is unusable on a large disk image — piping it through `grep` for a known pattern (like `picoCTF`) narrows thousands of lines down to the one that matters.

**Real-world relevance:** Searching raw disk images for known text patterns is a basic disk-forensics technique, used to recover evidence or artifacts without needing to mount or fully parse the filesystem.