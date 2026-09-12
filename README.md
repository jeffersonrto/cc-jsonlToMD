# claude-chat-to-md

Convert [Claude Code](https://docs.anthropic.com/en/docs/claude-code) chat sessions to clean, readable Markdown — including subagent conversations.

Claude Code persists full chat history as JSONL files under `~/.claude/projects/`. This tool reads those files and produces well-formatted Markdown with proper headings, code blocks, and collapsible sections for tool results and subagent conversations.

## Usage

### List sessions

```bash
python3 main.py --list
```

```
#    Date                 ID           Title                                              Project
------------------------------------------------------------------------------------------------------------------------
1    2025-10-15 14:30     a1b2c3d4..   Refactor auth middleware                            dev/myapp
2    2025-10-14 09:15     e5f6a7b8..   Add user settings page                              dev/myapp
3    2025-10-13 16:45     c9d0e1f2..   Debug CI pipeline                                   dev/infra
```

### Convert a session

```bash
# By index (from --list)
python3 main.py 1 -o chat.md

# By UUID prefix
python3 main.py a1b2c3 -o chat.md

# By title substring
python3 main.py "auth middleware" -o chat.md

# Most recent session
python3 main.py --latest -o chat.md
```

### Filter by project

```bash
python3 main.py --list --project myapp
python3 main.py --latest --project myapp -o chat.md
```

### Export all sessions

```bash
python3 main.py --all --output-dir ./exports/
```

### Options

| Flag | Description |
|---|---|
| `--list`, `-l` | List all available sessions |
| `--latest` | Convert the most recent session |
| `--all` | Convert all sessions |
| `--project`, `-p` | Filter sessions by project path substring |
| `--output`, `-o` | Output file (default: stdout) |
| `--output-dir`, `-d` | Output directory for `--all` mode |
| `--no-subagents` | Exclude subagent conversations |
| `--no-tool-results` | Exclude tool call results |

## Output format

- **User messages** → `## User` sections with code blocks
- **Assistant messages** → `## Assistant` sections with highlighted `> [!note] Message` callouts
- **Tool actions** → grouped under `### Actions` with `####` descriptive subheaders
- **Tool results** → collapsible Obsidian callouts (`> [!note]- Command Result`)
- **Subagent conversations** → collapsible Obsidian callouts (`> [!abstract]- Subagent Conversation`)
- **Code** → fenced code blocks with language hints and dynamic fences
- **Diffs** → displayed as unified diff format
- System tags (`<ide_opened_file>`, `<system-reminder>`, `<local-command-caveat>`) are stripped

## How it works

Claude Code stores sessions at:

```
~/.claude/projects/<encoded-project-path>/<session-uuid>.jsonl
```

Each line is a JSON object: `user` messages, `assistant` messages (with tool_use blocks), `tool_result` responses, and metadata. Subagent conversations live in a `subagents/` subdirectory alongside the main session.

## Requirements

Python 3.10+ — no external dependencies.
