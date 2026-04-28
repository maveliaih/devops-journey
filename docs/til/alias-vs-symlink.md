# Notes: Shell Aliases vs Symlinks — Navigation
# Shortcuts Done Right

**Date**: Stage 01 — Linux + Terminal  
**Category**: Shell · Bash · Best Practices

---

## Содержание
- [Context](#context)
- [Symlink vs Alias — Key Difference](#symlink-vs-alias--key-difference)
- [What I Did](#what-i-did)
- [Why This Approach](#why-this-approach)
- [Key Takeaways](#key-takeaways)

---

## Context

During Stage 01 practice (Block 1), I created a symlink for quick navigation to the stage directory:

`ln -s $STAGE/practice/files $STAGE/practice/current`

This symlink was committed to the repository and caused the GitHub Pages build to fail — `tar` tried to read it during artifact packaging and crashed because the target path didn’t exist in the GitHub CI environment.

See full details: [postmortem-github-pages-symlink.md](postmortems/postmortem-github-pages-symlink.md)

After fixing the issue, I replaced the symlink-based approach with a shell alias. This note documents what I did, why, and the key difference between the two approaches.

## Symlink vs Alias — Key Difference

*   **Symlink** (`ln -s target link_name`) is a real file on disk.
    *   Exists in the filesystem — visible via `ls -la`, can be committed to git.
    *   Works for any program, not just the terminal.
    *   This is why `tar` found it and tried to read it during the GitHub Pages build.
*   **Alias** (`alias name='command'`) exists only in your shell session.
    *   Not a file — nothing is written to disk.
    *   Git cannot see it, other programs cannot see it.
    *   Only works in an interactive terminal session.
    *   Does not get passed to child processes or CI environments.

> **Simple analogy**: a symlink is like a desktop shortcut (a real file). An alias is like a personal abbreviation that only exists in your head — or in your shell config.

## What I Did

**Problem**: After removing the symlink, I needed a quick way to navigate to the stage directory without typing the full path every time.  
**Solution**: Created a shell alias and added it to `~/.bashrc` so it persists across sessions.

```bash
# Add alias to ~/.bashrc
echo "alias tostage='cd ~/devops-journey/stage-01-linux'" >> ~/.bashrc

# Apply immediately to current session without restarting terminal
source ~/.bashrc

# Verify it works
tostage
pwd
```

## Why This Approach

*   **Why alias and not symlink**: Alias exists only in the shell — git cannot see it, CI tools cannot see it. No risk of accidentally committing it.
*   **Why add to `~/.bashrc`**: An alias declared directly in the terminal lives only for that session. Adding it to the config makes it load automatically.
*   **Scope of `~/.bashrc`**: This file is personal. It only loads for my user on this machine.
*   **Why not export**: `export` makes a variable available to all child processes (like `$STAGE` did). An alias is safer as it doesn't affect child processes at all.

## Key Takeaways


| Feature | Symlink | Alias |
|:---|:---:|:---:|
| **Exists on disk** | Yes | No |
| **Visible to git** | Yes | No |
| **Visible to other programs** | Yes | No |
| **Persists after terminal close** | Yes | Only in `~/.bashrc` |
| **Risk of committing** | High | None |
| **Safe for CI environments** | No | Yes |

---

**Summary**: Use **symlinks** when you need a persistent filesystem shortcut that other programs can follow. Use **aliases** when you need a personal navigation shortcut in the terminal.
