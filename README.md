<div align="center">
  <img src="banner.jpg" alt="Serta — Universal Server Builder" width="100%"/>
</div>

<br/>

<div align="center">

[![Python](https://img.shields.io/badge/Python-3.8%2B-00e5ff?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)
[![Flask](https://img.shields.io/badge/Flask-Latest-7c4dff?style=flat-square&logo=flask&logoColor=white)](https://flask.palletsprojects.com/)
[![License](https://img.shields.io/badge/License-MIT-00e5ff?style=flat-square)](#license)
[![Single File](https://img.shields.io/badge/Single%20File-main.py-7c4dff?style=flat-square)](#)

</div>

---

## What is Serta?

Serta is a single-file Python CLI tool that spins up production-ready servers in seconds — no config sprawl, no boilerplate. Pick a server type, answer a few prompts, and you have a running Flask instance with an admin panel, file management, Cloudflare tunnel support, and bot hosting baked in.

Everything lives in one file: `main.py`.

---

## Features

### 🌐 Web Server
Host static sites or any folder as a live web server. Includes an admin panel, file upload widget (individual files, full folder trees, or ZIP archives), and optional Cloudflare tunnel for instant public URLs.

### 📦 File Storage Server
A self-hosted file cabinet. Upload, download, browse, and manage files through a clean web UI. Optional login protection keeps your data private.

### 🤖 Bot Hosting
Run Discord, Telegram, Slack, or any generic Python bot as a managed subprocess. Upload your bot script via the admin panel, set env tokens, install pip dependencies, and control the bot's lifecycle (start / stop / restart) with live log streaming — all from the browser.

### ☁ Cloudflare Tunnels
One-click public URLs via `cloudflared`. No port-forwarding, no router config. Works on any network.

### 🔐 Security
- PBKDF2-HMAC-SHA256 password hashing (260k iterations, per-project salt)
- CSRF token protection on all mutating endpoints
- Path-traversal guards on every file operation
- `secure_filename` enforcement on all uploads

---

## Requirements

- Python 3.8+
- Internet connection (for tunnel support and auto-installing dependencies)

Flask, Flask-SQLAlchemy, and Werkzeug are installed automatically on first run if they are missing.

---

## Quickstart

```bash
# Clone or download main.py, then:
python main.py
```

Serta walks you through everything interactively:

```
1. Run startup checks (Python version, network, Flask)
2. Create a new project or load an existing one
3. Choose a server type: Web · Storage · Bot
4. Set a port and admin password
5. Server starts — admin panel at http://127.0.0.1:<port>/admin
```

---

## Project Structure

Projects are stored under `~/.serta_projects/` and are fully self-contained:

```
~/.serta_projects/
└── my-project/
    ├── usb_config.json   ← project config (port, type, hashed password, etc.)
    ├── README.md         ← auto-generated per-project readme
    ├── site/             ← web server: hosted files (web type)
    ├── files/            ← storage server: uploaded files (storage type)
    └── bot/              ← bot hosting: uploaded script + logs (bot type)
```

---

## Server Types

### Web Server
| Route | Description |
|---|---|
| `/` | Serves the site directory |
| `/admin` | Admin panel — upload, manage, set hosted entry |
| `/admin/upload` | Multi-tab file uploader (Files · Folder · ZIP) |
| `/admin/tunnel` | Cloudflare tunnel management |

### Storage Server
| Route | Description |
|---|---|
| `/` | File browser |
| `/upload` | Upload files |
| `/download/<path>` | Download a file |
| `/admin` | Admin panel |

### Bot Hosting
| Route | Description |
|---|---|
| `/admin` | Bot admin panel |
| `/admin/bot/upload` | Upload bot script |
| `/admin/bot/start` | Start bot subprocess |
| `/admin/bot/stop` | Stop bot subprocess |
| `/admin/bot/restart` | Restart bot subprocess |
| `/admin/bot/logs` | Live log stream (polling) |

---

## Upload Modes

The admin upload widget supports three modes:

- **Files** — pick one or more individual files
- **Folder** — select an entire local folder; the directory tree is preserved server-side using `webkitRelativePath`
- **ZIP** — upload a `.zip` archive; Serta extracts it, strips the top-level wrapper folder (like GitHub zips have), and preserves the internal structure

---

## Bot Platforms

| Platform | Library auto-installed | Required env var |
|---|---|---|
| Discord | `discord.py` | `DISCORD_TOKEN` |
| Telegram | `python-telegram-bot` | `TELEGRAM_TOKEN` |
| Slack | `slack-bolt` | `SLACK_BOT_TOKEN`, `SLACK_SIGNING_SECRET` |
| Generic | _(your deps)_ | _(anything)_ |

---

## Configuration Reference

`usb_config.json` is written by Serta and lives inside each project directory. Key fields:

| Field | Description |
|---|---|
| `name` | Project name |
| `server_type` | `web` · `storage` · `bot` |
| `port` | Server port |
| `secret_key` | Flask secret key (auto-generated) |
| `admin_password_hash` | `salt$pbkdf2_hash` |
| `bot_type` | `discord` · `telegram` · `slack` · `generic` |
| `bot_entry` | Path to the bot's entry script |
| `bot_env` | Dict of env vars injected at bot startup |
| `bot_pip_deps` | List of pip packages installed before first run |

---

## License

MIT — do whatever you want with it.

---

<div align="center">
  <sub>Built by <a href="https://github.com/kaztral-ar">Kaztral</a> · Single file. Zero fuss.</sub>
</div>
