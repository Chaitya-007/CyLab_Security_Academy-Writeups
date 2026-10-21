# Ping Command (picoCTF 2026, General Skills, Easy)

**Problem:** Ping Command.

**Solution:**
1. How Command Injection Works in Ping Forms => 
   - When a poorly secured web application takes user input and passes it directly to a system shell command behind the scenes, it looks something like this:
   ``` bash
   # What the server executes internally:
ping -c 2 [YOUR_INPUT]
 
   ```
2.  If the application fails to sanitize or validate what you type, you can use shell separators (like ;, &&, or |) to terminate the ping command early and chain a completely new command after it.
3. Examples of Command Chaining => 
   - If you enter an IP followed by a separator, the server executes both:
   a. Listing Files: Entering 8.8.8.8; ls causes the server to run:
   ``` bash
   ping -c 2 8.8.8.8; ls
   ```
   - This forces the server to return the directory contents to your screen.
   b. Reading the Secret: If you spot a file like flag.txt or secret.txt, entering 8.8.8.8; cat flag.txt forces the server to read and print the file's contents back to you.

**Learned:** Command injection vulnerabilities in ping commands and how to exploit them for file listing and reading.