# scripts

A collection of random utility scripts.

## rando

Creates a git worktree and launches Claude Code in a new terminal window to work on a task.

**Usage:**
```bash
rando [-m] "your idea message"
```

**Options:**
- `-m`: Create worktree from master branch instead of current branch

**What it does:**
1. Creates a timestamped branch (e.g., `rando_20231008_143022`)
2. Creates a git worktree in `../rando_worktrees/[branch_name]`
3. Symlinks files/directories specified in `.rando` config file (if present)
4. Launches Claude Code in a new Ghostty window with:
   - No permission prompts (`--dangerously-skip-permissions`)
   - A "finisher" agent that can commit, push, and create draft PRs
   - Your task message

**Configuration:**
Create a `.rando` file in your repo root to specify files/directories to symlink:
```
# .rando example
node_modules
.env
dist
```
- One path per line
- Supports comments with `#`
- Paths are relative to repo root

**Examples:**
```bash
# Create worktree from current branch
rando "add login button to homepage"

# Create worktree from master branch
rando -m "refactor user authentication"
```

**Cleanup:**
Use `rando-clean` to remove old worktrees.
