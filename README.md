<div align="center">



# Zoom Downloader

**Download your Zoom cloud recordings — fast, simple, in parallel.** ⚡
<img width="1355" height="713" alt="image" src="https://github.com/user-attachments/assets/6dbc7e51-4dcc-414c-96ec-f09a318d6736" />
<img width="639" height="696" alt="image" src="https://github.com/user-attachments/assets/9ce0ab75-ebad-4f5b-99d4-afccc053fde2" />
<img width="415" height="243" alt="image" src="https://github.com/user-attachments/assets/988f9992-d1f0-4c72-8a96-7a488af1156d" />



*Built for students and teams who want to keep and review recorded sessions after the course ends.* 🎓

`Native desktop app` · `Parallel CDN download` · `Auto resume` · `Transcript (VTT)` · `CLI`

<sub>Developed by <b>Mohamed Hassan</b></sub>

</div>

---

## 📖 Overview

Zoom cloud recordings are easy to lose once a course or a meeting series is over. **Zoom Downloader** is a desktop app that takes your recording **share links + passcodes** and downloads everything straight from Zoom's CDN using **parallel connections**: same quality, much faster than clicking "Download" one recording at a time.

Paste all your links, hit one button, and get a clean, organized folder. 📁

<!-- Add a screenshot here: ![Zoom Downloader](docs/screenshot.png) -->

---

## ✨ Features

| | Feature | Details |
|---|---|---|
| 🖥️ | **Native desktop app** | A dark Qt window, not a browser tab |
| 🚀 | **Direct CDN download** | Captures the signed video URL from Zoom's player, then downloads it with parallel connections (up to 16 per file) |
| 📋 | **Queue system** | Add more links at any time; they join the running queue and take their turn automatically |
| 💾 | **Auto resume** | The list is saved to disk. Close the app, lose the internet, or reboot, then press the same button and it continues |
| ⏸️ | **Pause & Resume** | Pause stops new downloads and keeps the parts already written |
| 🔑 | **Passcode per recording** | A passcode on each line, plus a global *Default passcode* as a fallback |
| 🏷️ | **Flexible naming** | Custom names, or number several rows as a sequence (`Lecture 1…12`) |
| 🛡️ | **No overwrites** | A duplicate name is saved as `Name (2)` |
| 🎞️ | **Choose what to get** | Video (`mp4`), audio only (`m4a`), and/or transcript (`vtt`) |
| 📅 | **Rename by date** | Organize any existing folder as `Name YYYY-MM-DD.mp4`, with dates read from the video metadata |
| 🧰 | **Also a CLI** | Script and automate downloads from the terminal |

---

## 🚀 Installation

> ℹ️ Installation needs an internet connection once, to fetch the Python packages and the Chromium engine.

### 🐧 Linux

```bash
tar -xzf zoom-joiner-1.4.3-linux-x86_64.tar.gz
cd zoom-joiner-1.4.3

./setup.sh                 # install for the current user (~/.local)
# or
sudo ./setup.sh --system   # install for all users (/opt + /usr/local/bin)
```

`setup.sh` does everything for you: checks Python, creates a virtual environment, installs the app, downloads Chromium, creates the launchers (`zoom-joiner` and `zoom-joiner-gui`), and adds a **Zoom Downloader** icon to your applications menu.

To remove everything:

```bash
./setup.sh --uninstall
```

### 🪟 Windows

Open **PowerShell** in the project folder and run:

```powershell
powershell -ExecutionPolicy Bypass -File .\setup.ps1
```

It installs **Zoom Downloader** for the current user and adds a Start menu shortcut. No admin rights needed.

To remove it (your queue and settings are kept):

```powershell
.\setup.ps1 -Uninstall
```

### 📦 Requirements

- Python **3.10+**
- Chromium (installed automatically through Playwright) or Google Chrome

---

## 🧭 How to Use

Open **Zoom Downloader** from your applications menu (or run `zoom-joiner-gui` in a terminal), then:

1. 📨 **Copy the share link** from the email or meeting chat where Zoom shared the recording.
2. 🔑 **Copy the passcode.** If the link already contains `?pwd=...`, you can leave it empty.
3. 📋 **Paste the links** into the box on the left and press **Add to the list**.
4. 📂 **Choose the folder** where the files should be saved.
5. ⬇️ Press **Download all recordings**.

If you close the app or the connection drops, open it again and press the same button. It continues from where it stopped.

### 📝 Input format

One recording per line (the name is optional):

```
share-link  passcode  name
```

```
https://us06web.zoom.us/rec/share/AbCdEf...  123456  Weekly Team Sync
https://us06web.zoom.us/rec/share/XyZ123...  654321  Client Review
```

> 💡 **Where do I find the link?** Zoom sends the recording link by e-mail or in the meeting chat. It starts with `https://.../rec/share/` and usually ends with `?pwd=123456`. That code is the passcode.

---

## 🎛️ Interface at a Glance

| Section | What it does |
|---|---|
| **Top bar** | `Download all recordings` · `Pause` · progress bar · app status |
| **1 · Paste the recording links** | Paste links, then `Add to the list` or `Paste from clipboard` |
| **2 · Options** | Default passcode, save folder, connections per file, video / audio / transcript |
| **Organize an existing folder** | Rename files by date with an optional base name |
| **3 · Recording list** | Every recording with its live status; right-click to rename |
| **Activity log** | Live log of everything the app does |
| **How to use** | Built-in help window |

---

## 🗂️ Naming & Organizing

### ✏️ Rename items in the list

- **Right-click** a row (or **double-click** it) to rename it
- Select several rows and choose **Name as a sequence** to number them in one go (e.g. `Lecture 1 … 12`)
- The recording name becomes the saved file name. Two files never overwrite each other, and a duplicate is saved as `Name (2)`

### 📅 Organize an existing folder

Already have a folder full of recordings? Use **Rename files by date**:

- Type a **base name** to unify every file as `Name YYYY-MM-DD.mp4` (numbered when two recordings share a date)
- Or leave it empty to **only add the missing dates**
- The date is read from the **video metadata**, so files downloaded earlier work too
- It runs on the folder selected in **Save to**

---

## 🔒 Restricted Recordings

If the owner restricted the recording, Zoom asks you to sign in first:

1. Open the link once in your browser and sign in. 🌐
2. Come back to the app and retry.

---

## 💻 Command Line

```bash
# One recording, with audio too
zoom-joiner download \
  --url "https://us06web.zoom.us/rec/share/AbCdEf..." --passcode 123456 \
  --out ~/Downloads/zoom-recordings --audio

# From a file (one line per recording: url passcode name)
zoom-joiner download -f recordings.txt --parallel 3

# Maximum speed: 16 connections per file
zoom-joiner download -f recordings.txt --connections 16
```

Launch the desktop app from the CLI:

```bash
zoom-joiner app      # or: zoom-joiner-gui
```

Check your environment:

```bash
zoom-joiner doctor
```

---

## 💾 Where Is My Data?

| What | Location (Linux) |
|---|---|
| Saved queue (for auto resume) | `~/.local/share/zoom-joiner/queue.json` |
| Default download folder | `~/Downloads/zoom-recordings` |

---

## 🛠️ Build From Source

```bash
git clone https://github.com/<your-username>/Zoom-Downloader.git
cd Zoom-Downloader

make install              # creates a venv, installs packages and Chromium
source .venv/bin/activate
zoom-joiner doctor        # check the environment
```

Or manually:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -e .
playwright install chromium
```

Development commands:

```bash
make test      # pytest
make lint      # ruff
make format    # ruff format
make bundle    # distributable archive: dist/zoom-joiner-<ver>-linux-x86_64.tar.gz
```

### 🧱 Project structure

```
zoom-joiner/
├── src/zoom_joiner/
│   ├── cli.py            # command-line interface
│   ├── app.py            # native desktop app (Qt / PySide6)
│   ├── store.py          # saves the queue for auto resume
│   ├── config.py         # reads YAML / JSON / CSV / TXT
│   ├── models.py         # data models and statuses
│   ├── orchestrator.py   # parallelism, retries, cancellation
│   ├── report.py         # CSV + JSON + HTML reports
│   └── backends/         # Chromium / Playwright backend
├── setup.sh              # Linux installer
├── setup.ps1             # Windows installer
├── tests/                # unit tests
├── deploy/               # desktop entry + icons
└── Makefile
```

---

## 🐞 Known Issues & Feedback

This project is **still in testing**. If you hit a bug or a defect, please:

1. Open an **[Issue](../../issues)** and include:
   - 💻 Your OS and version
   - 🔁 Steps to reproduce
   - 📸 A screenshot or the Activity log output
2. Or contact me directly and I'll be happy to fix it. 🙏

---

## 🤝 Contributing

Ideas, bug fixes and feature requests are welcome! 💡

1. Fork the repo
2. Create your branch: `git checkout -b feature/my-feature`
3. Commit your changes: `git commit -m "Add my feature"`
4. Push the branch: `git push origin feature/my-feature`
5. Open a Pull Request

---

## ⚠️ Disclaimer

Zoom Downloader does not bypass Zoom's protections: you need a valid **link and passcode**, and recordings that require sign-in still do. Please only download recordings you own or have permission to access, and respect your institution's and Zoom's terms of use and privacy rules. This project is not affiliated with or endorsed by Zoom Video Communications, Inc.

---

## 📄 License

MIT. See [LICENSE](LICENSE).

---

<div align="center">

Developed with ❤️ by **Mohamed Hassan**

⭐ If this tool saved you time, consider giving the repo a star!

</div>
