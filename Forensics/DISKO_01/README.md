# DISKO 1

**Category:** Forensics · **Difficulty:** Easy

**Problem:** Find the flag inside a given disk image file.

**Solution:**

1. Downloaded the disk image:
```bash
wget https://artifacts.picoctf.net/c/538/disko-1.dd.gz
```

```
bash
file disko-1.dd.gz
```

Output
```
bash
disko-1.dd.gz: gzip compressed data, was "disko-1.dd", last modified: Wed Sep 23 01:42:12 2026, from Unix, original size modulo 2^32 52428800
```


Breakdown of the Output

• ```disko-1.dd.gz```: This is the name of the file you inspected. The .gz extension stands for gzip compression.
• ```gzip compressed data```: This confirms the file is genuinely compressed using the gzip format.
• ```was "disko-1.dd"```: This shows the original filename before it was compressed. A .dd file is a raw bit-for-bit copy of a storage device, commonly created using the dd command for backups or digital forensics.
• ```last modified: Wed Sep 23 01:42:12 2026```: This is the exact timestamp when the original disko-1.dd file was last changed before compression.
• ```from Unix```: This indicates the file was compressed on a Unix-like operating system, such as Linux or macOS.
• ```original size modulo 2^32 52428800```: This tells you the uncompressed size of the file in bytes. 52428800 bytes equals exactly 50 MiB (52,428,800 / 1024 / 1024). The "modulo 2^32" note simply means the gzip format only uses 32 bits to store file sizes, which accurately displays any file under 4 GB.

2. Unzipped it (the `.gz` extension means it's gzip-compressed):
```bash
gunzip disko-1.dd.gz
```

2. After unzipping, the file `disko-1.dd` was a raw disk image.

3. Extracted readable text from the disk image and filtered for the flag's prefix:
```bash
strings disko-1.dd | grep "academy{"
```

**Learned:** `strings` dumps *every* readable text string in a file, which is unusable on a large disk image — piping it through `grep` for a known pattern (like `academy{`) narrows thousands of lines down to the one that matters.

**Real-world relevance:** Searching raw disk images for known text patterns is a basic disk-forensics technique, used to recover evidence or artifacts without needing to mount or fully parse the filesystem.