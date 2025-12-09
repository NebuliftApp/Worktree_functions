# Git Worktree Helper Functions

Shell functions for managing git worktrees with parallel development workflows.

## Installation

1. **Create the functions file** at `~/.zsh_worktree_functions`

Manually create this file and paste the function definitions from your source.

2. **Update configuration variables** in `~/.zsh_worktree_functions`:

```bash
MAIN_REPO="/Users/your-username/path/to/your/repo"
WORKTREE_BASE="/Users/your-username/path/to/repo-worktrees"
ITERM_PROFILE="Default"  # Your iTerm profile name
```

3. **Add to your `~/.zshrc`:**

```bash
# Git Worktree Functions
source ~/.zsh_worktree_functions
```

4. **Reload your shell:**

```bash
source ~/.zshrc
```

## Available Functions

### `start-feature <branch-name>`
Creates a new worktree from master, copies git-ignored files (`.github/`, `.idea/`, `.vscode/`), and launches GitHub Copilot in a new terminal tab.

**Example:**
```bash
start-feature JIRA-123-add-authentication
```

### `rebase-feature <branch-name>`
Rebases the specified worktree branch onto the latest master. Fetches master from origin and rebases the feature branch.

**Example:**
```bash
rebase-feature JIRA-123-add-authentication
```

### `push-feature <branch-name>`
Pushes the specified branch to origin with upstream tracking (`-u origin <branch>`).

**Example:**
```bash
push-feature JIRA-123-add-authentication
```

### `delete-feature <branch-name>`
Deletes the worktree directory and local branch. Prompts for confirmation before deletion.

**Example:**
```bash
delete-feature JIRA-123-add-authentication
```

### `list-features`
Shows all git worktrees for the configured repository.

**Example:**
```bash
list-features
```

### `show-worktree-functions`
Displays help information about all available commands.

**Example:**
```bash
show-worktree-functions
```

## Complete Workflow Example

```bash
# 1. Start new feature (opens new tab with copilot)
start-feature JIRA-456-user-profile

# 2. Work on the feature in copilot session...

# 3. Get latest changes from master
rebase-feature JIRA-456-user-profile

# 4. Push to remote for PR
push-feature JIRA-456-user-profile

# 5. After PR is merged, cleanup
delete-feature JIRA-456-user-profile
```

## Configuration

The functions use three main variables:

- **`MAIN_REPO`** - Absolute path to your main git repository
- **`WORKTREE_BASE`** - Directory where worktrees will be created
- **`ITERM_PROFILE`** - iTerm2 profile name to use for new tabs (default: "Default")

Worktrees are created at: `$WORKTREE_BASE/<branch-name>/`

## Requirements

- macOS (uses AppleScript for terminal tab management)
- iTerm2 (required)
- GitHub Copilot CLI (`copilot` command)
- zsh shell
