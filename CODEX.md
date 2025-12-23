# Conductor for Codex CLI

## Installation

### Option 1: Install Commands (Recommended)

Copy the Conductor prompt files to your Codex prompts directory:

```bash
# Clone the repository
git clone https://github.com/fcoury/conductor.git /tmp/conductor

# Create prompts directory if needed
mkdir -p ~/.codex/prompts

# Copy the prompt files
cp /tmp/conductor/prompts/*.md ~/.codex/prompts/
```

### Option 2: Install as a Skill

For automatic context activation, install as a skill:

```bash
# Create skills directory if needed
mkdir -p ~/.codex/skills

# Copy the skill
cp -r /tmp/conductor/skills/conductor-development ~/.codex/skills/conductor
```

Or install directly to a specific repository:

```bash
# From your project root
mkdir -p .codex/skills
cp -r /path/to/conductor/skills/conductor-development .codex/skills/conductor
```

## Commands

After installing the prompt files, invoke commands using `/prompts:` prefix:

| Command | Description |
|---------|-------------|
| `/prompts:conductor-setup` | Set up Conductor environment for a project |
| `/prompts:conductor-new-track` | Create a new track (feature or bug fix) |
| `/prompts:conductor-implement` | Execute tasks from the current track's plan |
| `/prompts:conductor-status` | Display progress of all tracks |
| `/prompts:conductor-revert` | Revert a track, phase, or task |

### Command Examples

```
# Set up Conductor in a new project
/prompts:conductor-setup

# Create a new feature track
/prompts:conductor-new-track DESCRIPTION="Add user authentication"

# Check project status
/prompts:conductor-status

# Start implementing the next track
/prompts:conductor-implement

# Implement a specific track
/prompts:conductor-implement TRACK_NAME="auth_20251223"

# Revert a task
/prompts:conductor-revert task "Create login form"
```

## Skill Activation

If you installed Conductor as a skill, it activates automatically when:

- A `conductor/` directory exists in the project
- You mention "tracks", "specs", "plans", or "conductor" in your requests
- Files like `conductor/tracks.md` or `conductor/workflow.md` are present

You can also explicitly invoke the skill with `$conductor`.

## Context

If a user mentions a "plan" or asks about the plan, and they have used Conductor in the current session, they are likely referring to the `conductor/tracks.md` file or one of the track plans (`conductor/tracks/<track_id>/plan.md`).

## Skill Precedence

Codex searches skills in this order (highest to lowest):

1. `$CWD/.codex/skills` - Current working directory
2. `$REPO_ROOT/.codex/skills` - Repository root
3. `~/.codex/skills` - User home (recommended for global access)
4. `/etc/codex/skills` - System-wide
5. Built-in skills

## Resources

- [Codex CLI Skills Documentation](https://developers.openai.com/codex/skills.md)
- [Codex CLI Slash Commands](https://developers.openai.com/codex/guides/slash-commands/)
- [Agent Skills Specification](https://agentskills.io/specification)
- [Conductor GitHub](https://github.com/fcoury/conductor)
