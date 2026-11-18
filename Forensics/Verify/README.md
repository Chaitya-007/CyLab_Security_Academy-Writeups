# Verify

**Category:** General Skills · **Difficulty:** Easy

**Problem:** Given a target SHA-256 checksum, find the matching file among many in a `files` folder and decrypt it to get the real flag.

**Solution:**

1. Connected to the server and listed the files:
```bash
ssh -p <port> ctf-player@<host>
```
2. Check what is present
```bash
ls 
```
Output:
```
checksum.txt  decrypt.sh  files/
```

The files folder contains many SHA256 hashes.

3. **Find the Correct Hash**
   We have a checksum of a hash we need to find. 

4. By using the `sha256sum` command, we can compute the SHA-256 hash of each file in the `files` directory
```bash
sha256sum files/* 
```

5. To find the matching file, we can pipe the output of `sha256sum` to `grep` with the target checksum:
```bash
sha256sum files/* | grep <given_target_checksum>
```

6. The previous step should give you the filename of the hash you need.

Use decrypt.sh script to decrypt the file and get the flag:
```bash
./decrypt.sh files/<matching_filename>
```

**Learned:** A checksum (SHA-256) uniquely verifies a file's integrity — piping `sha256sum files/*` through `grep` for a known hash is an efficient way to identify one specific file among many without checking each manually.

**Real-world relevance:** Verifying file integrity via checksums is a standard practice for confirming downloaded software or data hasn't been tampered with — a core concept in secure software distribution and incident response (e.g. matching a file against a known-malware hash database).