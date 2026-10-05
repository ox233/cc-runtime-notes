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

### Variables on the web runtime

Reconstructed from the CLI, so treat every row as a guess until someone confirms it from
a web session.

| variable | present on web? | notes |
| --- | --- | --- |
| `CLAUDE_CODE_SESSION_ID` | ? | Present on CLI and desktop. |
| `CLAUDE_CODE_REMOTE_SESSION_ID` | assumed yes | The only marker that tells web apart. |
| `CLAUDE_CODE_ACCOUNT_UUID` | ? | |
| `CLAUDE_CODE_ORGANIZATION_UUID` | ? | May be absent on personal accounts. |
| `CLAUDE_CODE_OAUTH_SCOPES` | ? | Scope list may differ from the CLI. |
| `CLAUDE_CODE_ENTRYPOINT` | ? | Expected to differ. This is how the runtime is detected. |
| `ANTHROPIC_BASE_URL` | ? | May point at a different base on web. |

To confirm or correct the table:

```bash
env | grep -E '^CLAUDE_CODE_|^ANTHROPIC_BASE_URL' | sort
```

## Reading a value

Nothing here needs a credential:

```bash
echo "$CLAUDE_CODE_ENTRYPOINT ${CLAUDE_CODE_REMOTE_SESSION_ID:+web}"
```
