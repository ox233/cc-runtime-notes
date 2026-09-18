# Session environment

What each runtime exposes. Values omitted throughout.

## Present on the desktop app and the CLI

| variable | notes |
| --- | --- |
| `CLAUDE_CODE_SESSION_ID` | Session identifier. |
| `CLAUDE_CODE_ACCOUNT_UUID` | Account the session belongs to. |
| `CLAUDE_CODE_ORGANIZATION_UUID` | Organisation, where one applies. |
| `CLAUDE_CODE_OAUTH_SCOPES` | Scopes granted to the session token. |
| `CLAUDE_CODE_ENTRYPOINT` | How the session was started. |
| `ANTHROPIC_BASE_URL` | API base the session talks to. |
| `CLAUDECODE` | Set to `1` inside a Claude Code session. |

The session token is not in the environment on these runtimes. It lives in
`~/.claude/.credentials.json` under `claudeAiOauth.accessToken`, mode `0600`.

## Different on the web

The web session runs in a remote sandbox rather than on your machine, so:

| variable | notes |
| --- | --- |
| `CLAUDE_CODE_REMOTE_SESSION_ID` | Present on the web, absent elsewhere. Useful for telling the runtimes apart. |

Credentials are held inside the sandbox rather than in a user home directory, so the
desktop path above does not apply. Reporting the runtime as `claude-code/web` is what
lets a diagnostic be grouped correctly.

## Reading a value

Nothing here needs a credential:

```bash
echo "$CLAUDE_CODE_ENTRYPOINT ${CLAUDE_CODE_REMOTE_SESSION_ID:+web}"
```
