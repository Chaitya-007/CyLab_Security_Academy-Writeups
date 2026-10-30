# Collaborative Development

**Problem:** A team has been working on a flag-printing program across multiple git branches. Each branch holds a piece of the flag, and they need to be collected from all of them.

**Solution:**

1. Listed all branches, including remote-tracking ones:
```bash
git branch -a
```

2. Switched to each branch one by one:
```bash
git checkout <branch_name>
```

3. On each branch, checked the relevant file(s) for a piece of the flag:
```bash
cat flag.py   # or whatever the file was named on that branch
```

4. Repeated steps 2–3 for every branch listed, then combined all the pieces in order to reconstruct the full flag.

**Learned:** In git, branches can diverge significantly, each carrying its own commits and file states. `git branch -a` is essential for discovering work that isn't visible on the current branch (including remote branches not yet checked out locally), and `git checkout` lets you inspect each one's isolated state.

**Real-world relevance:** This mirrors real collaborative dev workflows, where different team members' work lives on separate branches before merging. From a security standpoint, it's also a reminder that sensitive data committed to *any* branch — not just `main` — is part of the repo's history and discoverable by anyone with clone access.