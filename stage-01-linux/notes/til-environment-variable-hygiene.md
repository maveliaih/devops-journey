# TIL: Environment Variable Hygiene — Why Generic Names Are Dangerous

**Date**: Stage 01 — Linux + Terminal  
**Category**: Shell · Best Practices · CI/CD

---

## What Happened

Following the Stage 01 learning guide, I added this line to `~/.bashrc` to simplify navigation:
`export STAGE="$HOME/devops-journey/stage-01-linux"`

The intent was to type `cd $STAGE` instead of the full path. It worked fine in the terminal, but later, while debugging a GitHub Pages failure, I realised that `STAGE` is a name used by many deployment tools to indicate an environment tier (staging, production, etc.). 

If a tool ran in my shell and inherited `$STAGE` containing a file path, it could crash or behave unexpectedly.

---

## Why Generic Variable Names Are Risky

When you `export` a variable in `~/.bashrc`, it becomes part of the environment for every process you launch — including CI tools, build scripts, and package managers.


| Variable | Used by |
|:---|:---|
| **CI** | GitHub Actions, CircleCI (detects CI environment) |
| **ENV / NODE_ENV** | Ruby/Rails, Node.js apps, Webpack, Vite |
| **STAGE** | Serverless Framework, various deploy scripts |
| **TARGET** | Make, CMake, cross-compilation toolchains |
| **PLATFORM** | Various build systems |

---

## How I Fixed It

### Step 1: Remove the export from `~/.bashrc`
Open the file, delete or comment out the `export STAGE=...` line, then reload:
```bash
source ~/.bashrc
```

### Step 2: Remove the variable from the current session
```bash
unset STAGE
```

### Step 3: Replace with a shell function
Functions are safer than aliases because they don't leak into child processes and allow for error handling:

```bash
# Add to ~/.bashrc
tostage() {
  cd "$HOME/devops-journey/stage-01-linux" || return 1
}
```

---

## What I Should Have Done From the Start

*   **Bad** (Generic & Global): `export STAGE="..."`
*   **Better** (Unique Prefix): `export DV_STAGE_PATH="..."`
*   **Best** (Function for Navigation): `tostage() { cd ... }`

**Rule of thumb**: If a variable is only for personal navigation, **never export it**.

---

## Industry Standard: `direnv`

For project-specific variables, the standard tool is **direnv**. It automatically loads/unloads variables when you enter/leave a directory via a `.envrc` file.

```bash
# Install and hook into bash
sudo apt install direnv
echo 'eval "$(direnv hook bash)"' >> ~/.bashrc

# Usage in project directory
echo 'export DV_STAGE_PATH="$PWD"' > .envrc
direnv allow
```

---

## Key Takeaways

1. **`export` is global**: Every process you launch inherits exported variables.
2. **Avoid Collisions**: Generic names (`STAGE`, `ENV`, `TARGET`) collide with CI/CD tools.
3. **Navigation != Environment**: For jumping between folders, use shell functions.
4. **Namespace Personal Vars**: Prefix them (e.g., `DV_`, `MY_`).
5. **Use direnv**: Best for project-specific variables that shouldn't leak globally.
