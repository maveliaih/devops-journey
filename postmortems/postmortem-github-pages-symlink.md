# Postmortem: GitHub Pages Build Failure Due to Broken Symlink

## Summary

GitHub Pages deployment failed on every push to `main`. The build process was crashing during artifact packaging with a `tar` error. 

**Root cause**: A dangling symbolic link `stage-01-linux/practice/current` committed to the repository, pointing to an absolute path that only existed on the local VM.

*   **Duration**: ~30 minutes  
*   **Impact**: GitHub Pages site unavailable  
*   **Severity**: Low (personal learning repo)

---

## Timeline


| Time | Event |
|:---|:---|
| **T+0** | Enabled GitHub Pages for `devops-journey` repo |
| **T+2m** | First build triggered, failed immediately |
| **T+8m** | Identified Jekyll build error, added `.nojekyll` file |
| **T+15m** | Opened build logs, found the actual error on line 64 |
| **T+25m** | Removed symlink, pushed fix |
| **T+28m** | Build passed, site deployed successfully |

---

## Root Cause

During Stage 01 Linux practice, a symlink was created as part of an exercise:
`ln -s $STAGE/practice/files $STAGE/practice/current`

This symlink used an **absolute path** (`/home/ubuntu/...`), which does not exist in the GitHub build environment. When GitHub Pages triggered a build, the `tar` command failed while trying to archive the broken link:

```text
tar: ./stage-01-linux/practice/current: File removed before we read it
Error: Process completed with exit code 1
```

---

## What Led Me in the Wrong Direction

Initially, I assumed **Jekyll** was the only cause. Adding `.nojekyll` was a "blind fix" based on the first visible error. This is a classic debugging mistake: fixing a symptom instead of reading the full log to find the root cause.

---

## Resolution

I removed the broken symlink and staged the deletion:

```bash
# Remove the broken symlink
rm stage-01-linux/practice/current

# Stage the deletion explicitly
git add stage-01-linux/practice/current

# Commit and push
git commit -m "fix: remove broken symlink causing GitHub Pages build failure"
git push
```

---

## Lessons Learned

1.  **Read the full log**: The real error was on line 64, but I acted on line 1.
2.  **Absolute paths are evil**: Symlinks with absolute paths only work on the machine where they were created. Use relative paths or aliases.
3.  **Check your commits**: `git status` before `git add .` would have revealed the symlink.
4.  **Namespace navigation**: For personal shortcuts, use **shell aliases** in `~/.bashrc` instead of creating files in the project directory.

---

## Prevention

*   Run `git status` and review changes before staging.
*   Add local practice artifacts to `.gitignore`.
*   Prefer **aliases** for directory jumping: `alias tostage='cd ...'`.
