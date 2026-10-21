# Undo (picoCTF 2026, General Skills, Easy)

**Problem:** Printer Shares.

**Solution:**
1. Connected via smb => 
   ``` smbclient -L //<IP_ADDRESS_or_HOSTNAME> -p <PORT> -N ```
2. -L lists shares
    -p 35629 specifies the non-standard port
    -N tries a null session (no password) — many CTF print-server boxes allow anonymous/guest access
3. Connect to the relevant share => smbclient //<IP_ADDRESS_or_HOSTNAME>/<SHARE_NAME> -p <PORT> -N.
4. Inside the smb:\> prompt:
   - Use `ls` to list files
   - Use `get <filename>` to download the file to your local machine
```bash
<commands you ran>
```

**Learned:** How to connect to SMB shares and download files.