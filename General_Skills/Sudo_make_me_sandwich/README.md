# Sudo Make Me a Sandwich

**Problem:** Read `flag.txt` on a remote host where direct access is blocked, even with `sudo`.

**Solution:**

1. Connected to the box:
```bash
ssh -p <PORT> <hostname_or_IP>
```

2. Listed the home directory and found the target file:
```bash
ls
```
`flag.txt` was present but not readable directly.

3. Tried reading it normally — permission denied:
```bash
cat flag.txt
```

4. Tried reading it with `sudo` — still not allowed:
```bash
sudo cat flag.txt
```

5. Checked which commands I *am* allowed to run as root without a password:
```bash
sudo -l
```
The output listed `/usr/bin/emacs` (or similar) under `NOPASSWD`.

6. Since `emacs` was allowed with elevated privileges, I used it to open the file instead of `cat`:
```bash
sudo emacs flag.txt
```
With `emacs` running as root, it could open a file my own user couldn't read.

7. Viewed the flag inside the editor and exited.

**Learned:** This is a classic sudo-misconfiguration / GTFOBins pattern. When a specific binary is whitelisted under `NOPASSWD`, any command that binary can also run (or any file it can open) effectively runs with root's permissions. `sudo -l` is the first command to run on any privilege-escalation box, since it directly shows the attack surface.

**Real-world relevance:** Overly broad `sudo` entries are a common misconfiguration finding in SOC and pentest reports. Recognizing which binaries can be abused for privilege escalation (editors, pagers, interpreters) is a core skill — this is exactly what tools like GTFOBins catalog.