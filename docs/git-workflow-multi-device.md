# Git Workflow: Multi-Device Development Pattern

**Disciplined Solo Development** - Safe test-to-production promotion strategy

## 🎯 Overview

This workflow enables safe code synchronization between a test repository (`Sec-PBQ-New_Features`) and a production repository (`Sec-PBQ`) across multiple devices (Desktop, Laptop, Chromebook) without breaking production.

## 🛡️ Philosophy

**Why not "Cowboy Method"?**

When developing across 3 devices, you're essentially a 3-person team where every member is you. If you push broken code to `main` from your Desktop, you break your Chromebook setup instantly when you `git pull`. This workflow adds a safety layer while maintaining solo developer speed.

---

## 📖 The Six-Phase Workflow

### 📋 Phase 1: Create Production Backup

**Purpose**: Create a frozen snapshot of production before any changes.

```bash
cd ~/path/to/Sec-PBQ
git checkout main
git pull origin main
git checkout -b main-release-backup
git push -u origin main-release-backup
```

**Result**: `main-release-backup` branch is your rollback point.

**Do this**: Once, before your first sync.

---

### 📋 Phase 2: Link Test Repo to Production

**Purpose**: Add production repo as a second remote in your test repo.

```bash
cd ~/path/to/Sec-PBQ-New_Features
git remote add release git@github.com:8eight8toes8/Sec-PBQ.git
git remote -v  # verify both 'origin' and 'release' remotes exist
```

**Result**: Your test repo can now push directly to production repo.

**Do this**: Once, during initial setup.

---

### 📋 Phase 3: Create Sync Branch in Test Repo

**Purpose**: Stage all new features/fixes in a dedicated branch for testing.

```bash
git checkout main
git pull origin main
git checkout -b pbq-sync-v2
git add .
git commit -m "Sync PBQ features and fixes to production"
```

**Optional but recommended**: Test locally before syncing.

```bash
npm start  # or npm run dev
# Verify everything works
# Ctrl+C to stop
```

**Do this**: Every time you want to promote code from test to production.

---

### 📋 Phase 4: Push Sync Branch to Production

**Purpose**: Send your tested code to the production repo (as a branch, not `main` yet).

```bash
git push release pbq-sync-v2
```

**Result**: Production repo on GitHub now has a `pbq-sync-v2` branch with your new code.

---

### 📋 Phase 5: Merge into Production Main

**Purpose**: Officially promote the new code to production's `main` branch.

```bash
cd ~/path/to/Sec-PBQ
git fetch origin
git checkout main
git pull origin main
git checkout pbq-sync-v2  # optional: verify/test again in production context
git checkout main
git merge pbq-sync-v2
git push origin main
```

**Result**: Production `main` branch now contains your new features.

---

### 📋 Phase 6: Cleanup

**Purpose**: Delete the sync branch after successful merge.

```bash
git branch -d pbq-sync-v2
git push origin --delete pbq-sync-v2
```

---

## ⚡ Why This Works for Multi-Device Setup

| Device | Action | Outcome |
|--------|--------|----------|
| **Desktop** | Creates `pbq-sync-v2`, tests, merges to production `main` | Source of new code |
| **Chromebook** | Runs `git pull origin main` | Gets tested code from production |
| **Laptop** | Runs `git pull origin main` | Gets tested code from production |
| **Backup** | `main-release-backup` branch exists on GitHub | Instant rollback available |

**Safety Net**: If Desktop pushes broken code, Chromebook and Laptop don't see it until you merge to production `main`. You can test thoroughly before the merge.

---

## 🚨 Emergency Rollback

If the new code breaks production:

```bash
cd ~/path/to/Sec-PBQ
git checkout main
git reset --hard origin/main-release-backup
git push --force origin main  # use with caution - rewrites history
```

**Warning**: `--force` push rewrites history. Only use this when you need to undo a broken deployment.

---

## 📝 Quick Reference

### Initial Setup (Do Once)
```bash
# In production repo:
cd ~/path/to/Sec-PBQ
git checkout -b main-release-backup
git push -u origin main-release-backup

# In test repo:
cd ~/path/to/Sec-PBQ-New_Features
git remote add release git@github.com:8eight8toes8/Sec-PBQ.git
```

### Regular Sync (Do Every Time)
```bash
# In test repo:
cd ~/path/to/Sec-PBQ-New_Features
git checkout -b pbq-sync-v2
git add .
git commit -m "Sync features to production"
npm start  # test
git push release pbq-sync-v2

# In production repo:
cd ~/path/to/Sec-PBQ
git fetch origin
git checkout main
git merge pbq-sync-v2
git push origin main
git branch -d pbq-sync-v2
git push origin --delete pbq-sync-v2
```

---

## 🎯 When to Use vs Cowboy Method

### Use This Workflow When:
- Working across multiple devices
- Changes involve executable code (JavaScript, React components, API calls)
- You want to test before making code "official"
- Breaking production would disrupt your other devices

### Use Cowboy Method When:
- Fixing typos in comments
- Updating README text
- Changing color hex codes
- Minor non-breaking changes

---

## 📚 Further Reading

- [Git Branching - Basic Branching and Merging](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
- [GitHub Flow](https://guides.github.com/introduction/flow/)
- [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials)

---

*Last updated: December 2025*
