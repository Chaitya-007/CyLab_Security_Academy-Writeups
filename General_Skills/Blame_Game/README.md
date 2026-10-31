# Blame Game

**Problem:** A program isn't working, and someone's commit seems to be the cause. Figure out who is responsible — the "who" turns out to be the flag.

**Solution:**

1. Unzipped the challenge files:

2. Tried `git log` on its own first:
```bash
git log
```
This showed the full repo's commit history, but nothing that looked like a flag — too much noise, no clear answer.

3. Tried restoring the file through each visible commit hash, hoping the flag would appear in an older version of the file's content:
```bash
git restore --source=<commit_hash> message.py
```
This didn't work either — the file's contents didn't contain the flag.

1. After doing some research, found that `git log` can be scoped to a single file:
```bash
git log message.py
```

1. This showed only the commits that touched `message.py`, and the **author name** on one of those commits was the flag.

**Difference between `git log` and `git log <filename>`:**
- `git log` shows the commit history for the **entire repository** — every commit, regardless of which files it touched. With many commits or files, the flag-relevant entry can get buried.
- `git log <filename>` filters that history down to only the commits that **modified that specific file**. This surfaces relevant authorship and commit messages much faster when you already know which file matters.

**Learned:** Flags (and real-world clues, like who introduced a bug or vulnerability) aren't always in file *contents* — they can be in commit *metadata*: author name, email, commit message, or timestamp. Scoping `git log` to a specific file is far more efficient than restoring and diffing every commit by hand.

**Real-world relevance:** This is effectively `git blame` territory — tracing who changed what and when is a standard step in incident response and code-review investigations, especially when tracking down who introduced a security regression.