# SSOT_SETUP (Agent-Only)

Use this guide to run AI_TEAM as a Single Source of Truth (SSOT) across multiple devices and projects.

## 1) Goal
- Keep one canonical AI_TEAM repo per device.
- Let each project consume it via `.AI_TEAM`.
- Avoid per-project persona drift.

## 2) Recommended Topology
- Device-level SSOT path: `~/.AI_TEAM`
- Project-level link path: `<project>/.AI_TEAM`
- Consumer projects read persona docs through `.AI_TEAM/*`

## 3) Setup Mode A (Default): Symlink

### 3.1 One-time per device
```bash
git clone git@github.com:Lbin91/AI_TEAM.git ~/.AI_TEAM
```

If already cloned:
```bash
git -C ~/.AI_TEAM pull --ff-only
```

### 3.2 Per project
```bash
ln -sfn ~/.AI_TEAM /path/to/project/.AI_TEAM
```

### 3.3 Verify
```bash
test -L /path/to/project/.AI_TEAM && echo "symlink-ok"
test -f /path/to/project/.AI_TEAM/AGENTS.md && echo "docs-ok"
```

## 4) Setup Mode B (Fallback): Git Submodule
Use this only when an IDE/bot cannot follow symlinks outside workspace boundaries.

```bash
cd /path/to/project
git submodule add git@github.com:Lbin91/AI_TEAM.git .AI_TEAM
git submodule update --init --recursive
```

Update later:
```bash
git submodule update --remote .AI_TEAM
```

## 5) Runtime Read Order for Agents
Inside each consumer project:
1. `./.AI_TEAM/AGENTS.md`
2. `./.AI_TEAM/README.md`
3. `./.AI_TEAM/PERSONA_GUIDE.md`
4. `./.AI_TEAM/personas/*.md`
5. `./.AI_TEAM/AI_TEAMMATE_TEMPLATE.md`

## 6) Update Policy
- Edit and commit only in the canonical repo (`~/.AI_TEAM`) on each device.
- Push to `origin/main`.
- Pull latest before starting a new session:
```bash
git -C ~/.AI_TEAM pull --ff-only
```

## 7) Zsh Automation (Recommended)
If you want one command per project, add this block to `~/.zshrc`:

```bash
# >>> AI_TEAM SSOT >>>
export AITEAM_REPO_URL="git@github.com:Lbin91/AI_TEAM.git"
export AITEAM_SSOT_DIR="$HOME/.AI_TEAM"

# Ensure canonical SSOT repo exists and is up to date.
aiteam-sync() {
  if [ -d "$AITEAM_SSOT_DIR/.git" ]; then
    git -C "$AITEAM_SSOT_DIR" pull --ff-only || return 1
  else
    git clone "$AITEAM_REPO_URL" "$AITEAM_SSOT_DIR" || return 1
  fi
}

# Link current project to SSOT repo as .AI_TEAM.
aiteam-link() {
  local project_path="${1:-$PWD}"
  ln -sfn "$AITEAM_SSOT_DIR" "$project_path/.AI_TEAM" || return 1
  test -L "$project_path/.AI_TEAM" && test -f "$project_path/.AI_TEAM/AGENTS.md" || return 1
  echo "[AI_TEAM] linked: $project_path/.AI_TEAM -> $AITEAM_SSOT_DIR"
}

# One-shot setup from current project folder.
aiteam-use() {
  aiteam-sync || return 1
  aiteam-link "${1:-$PWD}" || return 1
  echo "[AI_TEAM] ready"
}

# Quick status for current project.
aiteam-status() {
  local project_path="${1:-$PWD}"
  echo "repo:  $AITEAM_SSOT_DIR"
  echo "link:  $project_path/.AI_TEAM"
  if [ -L "$project_path/.AI_TEAM" ]; then
    echo "target: $(readlink "$project_path/.AI_TEAM")"
  else
    echo "target: (not a symlink)"
  fi
}
# <<< AI_TEAM SSOT <<<
```

Reload shell:
```bash
source ~/.zshrc
```

Daily usage from each project root:
```bash
aiteam-use
aiteam-status
```

Optional usage with explicit path:
```bash
aiteam-use /path/to/project
```

## 8) Guardrails
- Do not maintain duplicate persona copies inside consumer projects.
- Do not fork per project unless governance explicitly requires divergence.
- If divergence is required, use a documented branch policy, not ad-hoc edits.
