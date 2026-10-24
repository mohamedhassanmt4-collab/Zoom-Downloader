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

Overview

Zoom cloud recordings are easy to lose once a course or a meeting series ends. Zoom Downloader is a desktop application that takes your recording share links and passcodes and downloads the files directly from Zoom's CDN using parallel connections. The quality is the same as the original, and it is much faster than downloading one recording at a time from the browser.

Paste your links, press one button, and get an organized folder of recordings.

<!-- Add a screenshot here: ![Zoom Downloader](docs/screenshot.png) -->

What's new in 1.5.2

More accurate progress bar: it reaches 100% only after the file is fully saved, and stays at 99% while the parts are merged.
A contact card inside the app for feedback and suggestions.
Rename by date now works on recordings downloaded earlier.
Features
Native desktop app. A dark Qt interface, not a browser tab.
Direct CDN download. Captures the signed video URL from Zoom's player and downloads it with up to 16 parallel connections per file.
Queue. Add links at any time; they join the running queue and are processed in turn.
Automatic resume. The queue is saved to disk, so closing the app, losing the connection, or rebooting does not lose progress.
Pause and resume. Pausing stops new downloads and keeps the parts already written.
Passcode per recording, with a default passcode as a fallback.
Flexible naming. Custom names, or sequence numbering for several rows at once (for example, Lecture 1 to 12).
No overwrites. A duplicate name is saved as Name (2).
Choose what to download: video (mp4), audio only (m4a), and transcript (vtt).
Rename by date. Organize an existing folder as Name YYYY-MM-DD.mp4, using the date stored in the video metadata.
Command-line interface for scripting and automation.
Download

Download one file for your system from the Releases page:

System	File	Install
🪟 Windows	zoom-downloader-windows.zip	Extract, then run setup.ps1
🐧 Linux (x86_64)	zoom-downloader-linux-x86_64.tar.gz	Extract, then run ./setup.sh
Installation

An internet connection is required once during installation, to fetch the Python packages and the Chromium engine.

Requirements: Python 3.10 or later. Chromium is installed automatically through Playwright; an existing Google Chrome also works.

🐧 Linux
bash
tar -xzf zoom-downloader-linux-x86_64.tar.gz
cd zoom-downloader

./setup.sh                 # install for the current user (~/.local)
# or
sudo ./setup.sh --system   # install for all users (/opt and /usr/local/bin)

The script checks Python, creates a virtual environment, installs the application, downloads Chromium, creates the launchers (zoom-joiner and zoom-joiner-gui), and adds a Zoom Downloader entry to the applications menu.

To uninstall:

bash
./setup.sh --uninstall
🪟 Windows
Extract zoom-downloader-windows.zip.
Open PowerShell inside the extracted zoom-downloader folder and run:
powershell
powershell -ExecutionPolicy Bypass -File .\setup.ps1

This installs the application for the current user and adds a Start menu shortcut. Administrator rights are not required.

To uninstall (your queue and settings are kept):

powershell
.\setup.ps1 -Uninstall
Usage

Launch Zoom Downloader from the applications menu, or run zoom-joiner-gui in a terminal.

Copy the share link from the email or meeting chat where Zoom shared the recording.
Copy the passcode. If the link already contains ?pwd=..., the passcode can be left empty.
Paste the links into the box on the left and press Add to the list.
Choose the folder where the files will be saved.
Press Download all recordings.

If the app is closed or the connection drops, open it again and press the same button; the download continues from where it stopped.

Input format

One recording per line. The name is optional.

share-link  passcode  name
https://us06web.zoom.us/rec/share/AbCdEf...  123456  Weekly Team Sync
https://us06web.zoom.us/rec/share/XyZ123...  654321  Client Review

Zoom sends the recording link by email or in the meeting chat. It starts with https://.../rec/share/ and usually ends with ?pwd=123456, where the value after pwd= is the passcode.

Interface overview
Section	Purpose
Top bar	Download all recordings, Pause, progress bar, and application status
1. Paste the recording links	Paste links, then Add to the list or Paste from clipboard
2. Options	Default passcode, save folder, connections per file, and video, audio, or transcript
Organize an existing folder	Rename files by date, with an optional base name
3. Recording list	Each recording with its live status; right-click to rename
Activity log	Live log of the application's actions
How to use	Built-in help window
Naming and Organizing
Renaming items in the list
Right-click a row, or double-click it, to rename it.
Select several rows and choose Name as a sequence to number them in one step.
The recording name becomes the saved file name. Two files never overwrite each other; a duplicate is saved as Name (2).
Organizing an existing folder

Use Rename files by date on any folder of recordings:

Enter a base name to unify every file as Name YYYY-MM-DD.mp4. Files that share a date are numbered.
Leave the base name empty to only add missing dates.
The date is read from the video metadata, so files downloaded earlier are supported.
The operation runs on the folder selected in Save to.
Restricted Recordings

If the recording owner has restricted access, Zoom asks you to sign in first. Open the link once in your browser, sign in, then retry in the application.

Command Line
bash
# One recording, including audio
zoom-joiner download \
  --url "https://us06web.zoom.us/rec/share/AbCdEf..." --passcode 123456 \
  --out ~/Downloads/zoom-recordings --audio

# From a file (one line per recording: url passcode name)
zoom-joiner download -f recordings.txt --parallel 3

# Maximum speed: 16 connections per file
zoom-joiner download -f recordings.txt --connections 16

Other commands:

bash
zoom-joiner app       # launch the desktop app (same as zoom-joiner-gui)
zoom-joiner doctor    # check the environment (Playwright and Chromium)

The CLI also retains an older feature for joining live meetings in bulk (zoom-joiner run and zoom-joiner gui). It is no longer part of the desktop app. Run zoom-joiner --help for details.

Data Locations
Item	Location (Linux)
Saved queue (used for automatic resume)	~/.local/share/zoom-joiner/queue.json
Default download folder	~/Downloads/zoom-recordings
Building from Source
bash
git clone https://github.com/mohamedhassanmt4-collab/Zoom-Downloader.git
cd Zoom-Downloader

make install              # creates a virtual environment, installs packages and Chromium
source .venv/bin/activate
zoom-joiner doctor        # verify the environment

Manual setup:

bash
python3 -m venv .venv
source .venv/bin/activate
pip install -e .
playwright install chromium

Development commands:

bash
make test      # run the test suite (pytest)
make lint      # lint (ruff)
make format    # format (ruff format)
make bundle    # build a distributable archive in dist/
Project structure
zoom-joiner/
├── src/zoom_joiner/
│   ├── app.py            # desktop application (Qt / PySide6)
│   ├── cli.py            # command-line interface
│   ├── store.py          # persists the queue for automatic resume
│   ├── config.py         # reads YAML, JSON, CSV, and TXT
│   ├── models.py         # data models and statuses
│   ├── orchestrator.py   # parallelism, retries, and cancellation
│   ├── report.py         # CSV, JSON, and HTML reports
│   └── backends/         # Chromium / Playwright backend
├── setup.sh              # Linux installer
├── setup.ps1             # Windows installer
├── tests/                # unit tests
├── deploy/               # desktop entry and icons
└── Makefile
Reporting Issues

This project is in beta. If you find a bug, please open an Issue and include:

Your operating system and version
Steps to reproduce the problem
A screenshot or the Activity log output, if available

You can also reach out through the contact card inside the application.

Contributing

Bug fixes, ideas, and feature requests are welcome.

Fork the repository.
Create a branch: git checkout -b feature/my-feature
Commit your changes: git commit -m "Add my feature"
Push the branch: git push origin feature/my-feature
Open a pull request.
⚠️ Disclaimer

Zoom Downloader does not bypass Zoom's protections. A valid link and passcode are required, and recordings that require sign-in still do. Download only recordings that you own or have permission to access, and respect Zoom's terms of use and your institution's privacy rules. This project is not affiliated with or endorsed by Zoom Video Communications, Inc.

License

Released under the MIT License. See LICENSE.

<div align="center">

Developed by Mohamed Hassan

</div>
