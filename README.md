<div align="center">

# ⚡ SERTA

### Simple · Efficient · Reliable · Terminal Automation

A lightweight server management and automation platform built with Python.

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat-square&logo=python&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-00FF88?style=flat-square)
![Platform](https://img.shields.io/badge/Platform-Linux%20%7C%20macOS%20%7C%20Windows%20%7C%20Android-222?style=flat-square)
![Status](https://img.shields.io/badge/Status-Active-00FF88?style=flat-square)

</div>

---

## ✨ Features

| Feature | Description |
|---|---|
| 🚀 **Fast & Lightweight** | Flask-based core. Runs on a Termux session or a $5 VPS |
| 📁 **File Management** | Upload files, full folder trees, or ZIP archives with auto-extraction |
| 🌐 **Web Hosting** | Serve static sites and web apps with Cloudflare tunnel integration |
| 🤖 **Bot Hosting** | Run Telegram, Discord, Twitter/X bots with live log polling |
| 💾 **Storage Management** | Per-server namespaced upload directories with usage tracking |
| 📊 **Logging & Monitoring** | Structured logs with real-time admin panel dashboard |
| 🔒 **Secure Auth** | CSRF-protected forms, session management, and auth utilities |
| 🌍 **Cross-Platform** | Linux · macOS · Windows · Android (Termux) |

---

## 📦 Installation

### 📱 Android (Termux)

> ⚠️ Install **Termux from [F-Droid](https://f-droid.org/en/packages/com.termux/)**, not the Play Store. The Play Store version is outdated.

```bash
# 1. Update packages
pkg update -y && pkg upgrade -y

# 2. Install dependencies
pkg install python git -y

# 3. Clone & setup
git clone https://github.com/Kaztral-ar/serta.git
cd serta
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 4. Run
python main.py
```

---

### 🐧 Linux

**Debian / Ubuntu**
```bash
sudo apt update && sudo apt install python3 python3-pip python3-venv git -y
```

**Arch Linux**
```bash
sudo pacman -S python python-pip git
```

**Fedora**
```bash
sudo dnf install python3 python3-pip git
```

**Then clone and run:**
```bash
git clone https://github.com/Kaztral-ar/serta.git && cd serta
python3 -m venv venv && source venv/bin/activate
pip install -r requirements.txt
python main.py
```

<details>
<summary>🔧 Optional: Run as a systemd service</summary>

```bash
sudo nano /etc/systemd/system/serta.service
```

Paste the following (update paths to match your install):

```ini
[Unit]
Description=SERTA Server

[Service]
WorkingDirectory=/path/to/serta
ExecStart=/path/to/venv/bin/python main.py
Restart=always

[Install]
WantedBy=multi-user.target
```

```bash
sudo systemctl enable --now serta
```

</details>

---

### 🍎 macOS

```bash
# 1. Install Homebrew (if not already installed)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# 2. Install Python & Git
brew install python git

# 3. Clone & setup
git clone https://github.com/Kaztral-ar/serta.git && cd serta
python3 -m venv venv && source venv/bin/activate
pip install -r requirements.txt

# 4. Run
python main.py
```

> ℹ️ On **Apple Silicon (M1/M2/M3)**, all commands work the same. Homebrew installs to `/opt/homebrew` instead of `/usr/local`.

---

### 🪟 Windows

> ℹ️ Use **PowerShell** or **Windows Terminal**. WSL2 (Ubuntu) is also fully supported — follow the Linux section instead.

```powershell
# 1. Install Python & Git via winget
winget install Python.Python.3.11 Git.Git

# 2. Clone & setup
git clone https://github.com/Kaztral-ar/serta.git; cd serta
python -m venv venv
.\venv\Scripts\Activate.ps1
pip install -r requirements.txt

# 3. Run
python main.py
```

> ⚠️ If `Activate.ps1` is blocked by execution policy, run this first:
> ```powershell
> Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
> ```

---

### 🐳 Docker

**Pull & run** (when image is published):
```bash
docker pull kaztral/serta:latest
docker run -d -p 5000:5000 --name serta kaztral/serta:latest
```

**Build from source:**
```bash
git clone https://github.com/Kaztral-ar/serta.git && cd serta
docker build -t serta .
docker run -d -p 5000:5000 -v $(pwd)/uploads:/app/uploads serta
```

**With docker-compose:**
```yaml
# docker-compose.yml
services:
  serta:
    build: .
    ports:
      - "5000:5000"
    volumes:
      - ./uploads:/app/uploads
      - ./logs:/app/logs
```
```bash
docker compose up -d
```

> ℹ️ Mount `./uploads` and `./logs` as volumes to persist data across container restarts.

---

## 🚀 Quick Start

```bash
# 1 — Clone
git clone https://github.com/Kaztral-ar/serta.git

# 2 — Enter directory
cd serta

# 3 — Create virtual environment
python -m venv venv

# 4 — Activate (Linux/macOS/Termux)
source venv/bin/activate
# Activate (Windows PowerShell)
.\venv\Scripts\Activate.ps1

# 5 — Install dependencies
pip install -r requirements.txt

# 6 — Run SERTA
python main.py
# → Server starts at http://localhost:5000

# 7 — Deactivate when done
deactivate
```

---

## 📁 Project Structure

```
serta/
├── main.py            # Entry point — Flask app, routes, runtime
├── requirements.txt   # Python dependencies
├── uploads/           # User-uploaded files (per-server namespaced)
├── logs/              # Structured runtime & access logs
├── static/            # CSS, JS, and assets served directly
├── templates/         # Jinja2 HTML templates
├── database/          # Local DB / config persistence
└── README.md
```

---

## ⚙️ Requirements

| Requirement | Version |
|---|---|
| 🐍 Python | 3.10 or higher |
| 🔀 Git | Any recent version |
| 🌐 Flask | Installed via `requirements.txt` |
| 💻 OS | Linux · macOS · Windows · Android (Termux) |

---

## 🔧 Virtual Environment

```bash
# Create
python -m venv venv

# Activate — Linux / macOS / Termux
source venv/bin/activate

# Activate — Windows
.\venv\Scripts\Activate.ps1

# Deactivate
deactivate
```

---

## 🤝 Contributing

Contributions, bug reports, and feature requests are welcome!

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/my-feature`)
3. Commit your changes (`git commit -m 'Add my feature'`)
4. Push to the branch (`git push origin feature/my-feature`)
5. Open a Pull Request

---

## 📜 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

## 👨‍💻 Author

**Gokul AR** · [@Kaztral-ar](https://github.com/Kaztral-ar)

---

<div align="center">

Made with ❤️ using Python

⭐ Star this repo if you find it useful!

</div>
