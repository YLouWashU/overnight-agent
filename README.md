# overnight-agent

Schedule Claude Code to resume automatically when your usage refreshes. Works like handing off to a junior engineer before clocking out.

## Usage

Invoke with `/overnight-agent` in a Claude Code conversation.

### Modes

- **Pause** — When you invoke `/overnight-agent`, it asks what to focus on, when your usage refreshes, and what permission level to run with, then schedules a cron job.
- **Resume** — When cron fires, Claude wakes up, reads your brief, and works through the tasks.
- **Recap** — Use `/overnight-agent recap` to see the status of all overnight sessions in the current project.

## Example

```
You: /overnight-agent
Usage is running low. Before I hand off — what should the next session focus on?
You: Continue refactoring the auth module
Anything else? no
When does your usage refresh? tomorrow at 9am
Got it — scheduling for 09:03.
What permission level for that run? B (Accept edits only)
Anything else? no
Briefed. Resuming at 09:03. See you later.
```

At 9:03am, Claude wakes up and picks up where you left off.

## How it works

- Brief and state are saved to `.claude/overnight/<session_id>/`
- A cron job fires once at the scheduled time, then removes itself
- Uses `--continue` or `-r <session_id>` to resume from where you left off

## Requirements

- Claude Code CLI
- `crontab` available on your system
- One of: `--dangerously-skip-permissions`, `--permission-mode acceptEdits`, or `--permission-mode auto`