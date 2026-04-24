# Improve Extension

Prompt-orchestrated repository improvement workflow for Qwen Code.

## What It Does

The extension adds `/improve`, a command that selects one meaningful,
locally-verifiable codebase improvement, implements it in an isolated git
worktree, and validates the result with a read-only test agent.

It supports:

- one-shot improvements with `/improve`
- directed improvements such as `/improve improve CLI error messages`
- session-scoped recurring jobs such as `/improve --every 2h`
- context-guided task selection from GitHub issues, repository specs, and
  codebase signals
- isolated `improve/<kind>-<task-slug>-YYYY-MM-DD-<hash>` branches

## Usage

```text
/improve
/improve --once
/improve improve auth flow
/improve --every 2h
/improve --every 2h uiux
/improve list
/improve clear
```

Recurring jobs require Qwen Code's experimental cron tools:

```json
{
  "experimental": {
    "cron": true
  }
}
```

You can also enable them for a session with `QWEN_CODE_ENABLE_CRON=1`.

## Contents

- `commands/improve.md`: public controller command
- `commands/improve/once.md`: internal one-shot command used by scheduled jobs
- `agents/improve-dev.md`: implementation worker
- `agents/improve-test.md`: read-only validation worker
