# Commitment Issues (Git History Recovery)

**Problem:** The flag was accidentally written into a file and then deleted. Recover it from the file's git history.

**Solution:**

1. Checked the commit history to see what changes had been made:
```bash
git log
```
Each commit showed a hash and a commit message, one of which indicated the flag had been written and then removed.

2. Restored the file's contents from the commit *before* the deletion, using that commit's hash:
```bash
git restore --source=<commit_hash> path/to/file.txt
```
In this case:
```bash
git restore --source=<commit_hash> ./message.txt
```

3. Opened the restored file to read the flag:
```bash
cat ./message.txt
```

**What the command does:** `git restore --source=<commit_hash> <file>` checks out the version of `<file>` as it existed at that specific commit and writes it into your working directory, without touching the rest of your repo or moving your branch. It's effectively a time machine for a single file. Git never truly deletes committed data from history — deleting a file and committing that deletion only removes it from the latest snapshot; the old content still exists in earlier commits until that history is rewritten or garbage-collected.

**Learned:**
- `git log` is the first step whenever a file's current state doesn't match what you expect — it shows what changed and when.
- Deleting a file (or its contents) and committing that change does **not** erase it from history. Anyone with access to the repo can recover it via `git restore --source` or `git show <commit_hash>:<path>`.

**Lessons learned:**
- Never commit secrets, flags, credentials, or sensitive data to a git repository, even temporarily — "deleting" it afterward does not remove it from history.
- If sensitive data is accidentally committed, deleting it in a new commit is not enough; it must be purged from history entirely (e.g. with `git filter-repo` or `BFG Repo-Cleaner`), and the credential should be treated as compromised and rotated.
- This mirrors a real-world incident response scenario: attackers routinely scan public repos for leaked secrets in commit history, not just in the current file tree.

**Real-world relevance:** Secret-scanning of git history is a standard part of both offensive recon (attackers hunting for leaked keys) and defensive practice (SOC/AppSec teams running tools like `gitleaks` or `trufflehog` against repos to catch this before attackers do).