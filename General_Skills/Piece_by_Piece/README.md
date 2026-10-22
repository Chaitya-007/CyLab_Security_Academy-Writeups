# Piece_by_Piece (General Skills, Easy)

**Problem:** After SSH login, the home directory has multiple file parts. These parts need to be combined and extracted to reveal the flag.

## Solution

### 1. Log in over SSH
```bash
ssh <username>@<hostname_or_IP> -p <PORT>
```
* `-p <PORT>` = connect to a custom port instead of the default 22.

### 2. Look around
```bash
ls
```
* `ls` lists files; `cat` prints a file's contents.
* The hint says: the flag is a split, password-protected zip, and the password is `<password>`.

### 3. Combine the parts in order
```bash
cat file_1.txt file_2.txt file_3.txt  > <filename>.zip
```
* `cat` joins files one after another into one stream.
* `>` redirects that output into a new file (`<filename>.zip`). It overwrites if the file exists; `>>` appends instead.
* Order matters. The wrong order corrupts the zip.

**Shortcut with a wildcard:**
```bash
cat file_* > <filename>.zip
```
* `*` matches any characters, so `file_*` expands to `file_1.txt file_2.txt file_3.txt`, sorted alphabetically.

### 4. Verify it's a zip (optional)
```bash
file flag.zip
```
* `file: command not found` on this box, so use the manual check instead:
```bash
head -c 4 flag.zip | xxd
ls -l flag.zip
```
* `head -c 4` = read only the first 4 bytes.
* `xxd` = show bytes as hex. A zip starts with `50 4b 03 04` (`PK..`).
* `ls -l` = long listing with file size. It should equal the sum of the five parts.

### 5. Extract with the password
```bash
unzip -P <password> flag.zip
```
* `-P <password>` = supply the password on the command line. Without it, `unzip` prompts for it.
* No `unzip`? Use Python:
```bash
python3 -c "import zipfile; zipfile.ZipFile('flag.zip').extractall(pwd=b'<password>')"
```

### 6. You will get your flag.

## Wildcard / shortcut cheat sheet

| Pattern | Meaning | Example |
|---|---|---|
| `*` | any number of any characters | `part_*` matches all parts |
| `?` | exactly one character | `part_a?` matches `part_aa`..`part_az` |
| `[a-e]` | one character from a range | `part_a[a-e]` matches `part_aa`..`part_ae` |
| `{aa,ab,ac}` | brace expansion, explicit list | `cat part_{aa,ab,ac,ad,ae} > flag.zip` |
| `ls -v` | natural number sort (`part2` before `part10`) | `cat $(ls -v part*) > out` |
| `>` / `>>` | overwrite / append output to a file | `cat part_* > flag.zip` |

## Flags used

| Command | Flag | Meaning |
|---|---|---|
| `ssh` | `-p` | port number |
| `ls` | `-l` | long listing (size, permissions, date) |
| `ls` | `-a` | include hidden files |
| `ls` | `-v` | natural version sort |
| `head` | `-c N` | first N bytes |
| `unzip` | `-P pass` | password for the archive |

## Learned
Split files can be rebuilt with `cat` and a wildcard in the right order, a zip can be checked by its `PK` magic bytes, and `unzip -P` extracts password-protected archives.