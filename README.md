<div align="center">



# Zoom Downloader

**Download your Zoom cloud recordings — fast, simple, in parallel.** ⚡
<img width="1355" height="713" alt="image" src="https://github.com/user-attachments/assets/6dbc7e51-4dcc-414c-96ec-f09a318d6736" />
<img width="639" height="696" alt="image" src="https://github.com/user-attachments/assets/9ce0ab75-ebad-4f5b-99d4-afccc053fde2" />
<img width="415" height="243" alt="image" src="https://github.com/user-attachments/assets/988f9992-d1f0-4c72-8a96-7a488af1156d" />



*Built for students and teams who want to keep and review recorded sessions after the course ends.* 🎓

`Native desktop app` · `Parallel CDN download` · `Auto resume` · `Transcript (VTT)` · `CLI`

<sub>Developed by <b>Mohamed Hassan</b></sub>

⬇️ Download  •  ✨ Features  •  🚀 Install  •  🧭 Usage  •  🗂️ Organize  •  🐞 Issues

</div> <!-- Add a screenshot here: <p align="center"><img src="docs/screenshot.png" width="860" alt="Zoom Downloader"></p> -->
📖 Overview

Zoom cloud recordings are easy to lose once a course or a meeting series ends. Zoom Downloader takes your recording share links and passcodes and downloads the files straight from Zoom's CDN using parallel connections: same quality, much faster than downloading one recording at a time.

Paste your links, press one button, and get a clean, organized folder.

⚡ Fast	🔁 Resumable	🗂️ Organized
Up to 16 parallel connections per file	Survives closing the app, a lost connection, or a reboot	Custom names, sequences, and rename-by-date

[!NOTE] New in 1.5.2: the progress bar now reaches 100% only after the file is fully saved (it holds at 99% while parts are merged), there is a contact card inside the app for feedback, and rename-by-date works on recordings downloaded earlier.

<a id="download"></a>

⬇️ Download

Get one file for your system from the Releases page:

System	File	Install


🪟 Windows	zoom-downloader-windows.zip	Extract, then run setup.ps1



🐧 Linux (x86_64)	zoom-downloader-linux-x86_64.tar.gz	Extract, then run ./setup.sh

<a id="features"></a>

✨ Features
	Feature	Details
🖥️	Native desktop app	A dark Qt window, not a browser tab
🚀	Direct CDN download	Captures the signed video URL from Zoom's player and downloads it with parallel connections
📋	Queue	Add links at any time; they join the running queue and take their turn
💾	Automatic resume	The queue is saved to disk, so nothing is lost if the app closes
⏸️	Pause and resume	Pausing stops new downloads and keeps the parts already written
🔑	Passcode per recording	A passcode on each line, plus a default passcode as a fallback
🏷️	Flexible naming	Custom names, or number several rows at once (Lecture 1 to 12)
🛡️	No overwrites	A duplicate name is saved as Name (2)
🎞️	Choose what to get	Video (mp4), audio only (m4a), and/or transcript (vtt)
📅	Rename by date	Organize any folder as Name YYYY-MM-DD.mp4 using the video metadata
💻	Command line	Scriptable downloads for automation

<a id="install"></a>

🚀 Install

[!NOTE] Installation needs an internet connection once, to fetch the Python packages and the Chromium engine.

Requirements: Python 3.10+ and Chromium (installed automatically through Playwright; an existing Google Chrome also works).



🐧 Linux
bash
tar -xzf zoom-downloader-linux-x86_64.tar.gz
cd zoom-downloader


./setup.sh                 # install for the current user (~/.local)
# or
sudo ./setup.sh --system   # install for all users (/opt + /usr/local/bin)

setup.sh does everything for you: checks Python, creates a virtual environment, installs the app, downloads Chromium, creates the launchers (zoom-joiner and zoom-joiner-gui), and adds a Zoom Downloader icon to your applications menu.

To remove everything:

bash
./setup.sh --uninstall


🪟 Windows
Download zoom-downloader-windows.zip and extract it (right-click → Extract All).


Open PowerShell inside the extracted zoom-downloader folder and run:

powershell

powershell -ExecutionPolicy Bypass -File .\setup.ps1


It installs Zoom Downloader for the current user and adds a Start menu shortcut. No admin rights needed.

To remove it (your queue and settings are kept):

powershell
.\setup.ps1 -Uninstall

<a id="usage"></a>

🧭 Usage

Open Zoom Downloader from your applications menu (or run zoom-joiner-gui in a terminal).

Step	What to do
1	📨 Copy the share link from the email or meeting chat where Zoom shared the recording
2	🔑 Copy the passcode. If the link already contains ?pwd=..., you can leave it empty
3	📋 Paste the links into the box on the left and press Add to the list
4	📂 Choose the folder where the files should be saved
5	⬇️ Press Download all recordings

[!TIP] If you close the app or the connection drops, open it again and press the same button. It continues from where it stopped.

📝 Input format

One recording per line. The name is optional.

share-link  passcode  name
https://us06web.zoom.us/rec/share/AbCdEf...  123456  Weekly Team Sync
https://us06web.zoom.us/rec/share/XyZ123...  654321  Client Review
Field	Required	Description
Share link	✅	Starts with https://.../rec/share/
Passcode	⚠️	Required unless the link already ends with ?pwd=...
Name	➖	Used as the saved file name
🎛️ Options
Option	Default	Description
Default passcode	Empty	Used for any link without its own passcode
Save to	~/Downloads/zoom-recordings	Destination folder
Connections per file	16	Parallel connections for each file
Video file (mp4)	On	Download the video recording
Audio only (m4a)	Off	Download the audio track only
Transcript (vtt)	Off	Download the transcript
<details> <summary><b>🖼️ Interface overview</b></summary> <br>
Section	Purpose
Top bar	Download all recordings, Pause, progress bar, application status
1 · Paste the recording links	Paste links, then Add to the list or Paste from clipboard
2 · Options	Default passcode, save folder, connections per file, video, audio, transcript
Organize an existing folder	Rename files by date, with an optional base name
3 · Recording list	Each recording with its live status; right-click to rename
Activity log	Live log of the application's actions
How to use	Built-in help window
</details>

<a id="organize"></a>

🗂️ Naming & Organizing
✏️ Rename items in the list
Action	Result
Right-click a row, or double-click it	Rename that recording
Select several rows → Name as a sequence	Numbers them in one step (for example, Lecture 1 to 12)
Two recordings with the same name	The second is saved as Name (2); files never overwrite each other
📅 Organize an existing folder

Use Rename files by date on any folder of recordings. It runs on the folder selected in Save to.

Base name	Result
Entered (for example, DAV-R)	Every file becomes DAV-R YYYY-MM-DD.mp4; files that share a date are numbered
Left empty	Only the missing dates are added to the existing names

The date is read from the video metadata, so files downloaded earlier work too.

🔒 Restricted Recordings

[!IMPORTANT] If the owner restricted the recording, Zoom asks you to sign in first. Open the link once in your browser, sign in, then retry in the app.

🩺 Troubleshooting
Problem	Solution
Zoom asks to sign in	See Restricted Recordings above
Passcode error	Check the passcode, or set the Default passcode in Options
Download stopped after a connection drop	Open the app and press Download all recordings again; it resumes
Installer cannot find Python	Install Python 3.10 or later, then run the installer again
Environment problems	Run zoom-joiner doctor to check Playwright and Chromium
<details> <summary><b>💻 Command line</b></summary> <br>
bash
# One recording, including audio
zoom-joiner download \
  --url "https://us06web.zoom.us/rec/share/AbCdEf..." --passcode 123456 \
  --out ~/Downloads/zoom-recordings --audio

# From a file (one line per recording: url passcode name)
zoom-joiner download -f recordings.txt --parallel 3

# Maximum speed: 16 connections per file
zoom-joiner download -f recordings.txt --connections 16
Command	Purpose
zoom-joiner download ...	Download recordings from the terminal
zoom-joiner app	Launch the desktop app (same as zoom-joiner-gui)
zoom-joiner doctor	Check the environment (Playwright and Chromium)
zoom-joiner --help	List all commands

The CLI also retains an older feature for joining live meetings in bulk (zoom-joiner run and zoom-joiner gui). It is no longer part of the desktop app.

</details> <details> <summary><b>💾 Data locations</b></summary> <br>
Item	Location (Linux)
Saved queue (used for automatic resume)	~/.local/share/zoom-joiner/queue.json
Default download folder	~/Downloads/zoom-recordings
</details> <details> <summary><b>🛠️ Build from source</b></summary> <br>
bash
git clone https://github.com/mohamedhassanmt4-collab/Zoom-Downloader.git
cd Zoom-Downloader

make install              # creates a virtual environment, installs packages and Chromium
source .venv/bin/activate
zoom-joiner doctor        # verify the environment

Or manually:

bash
python3 -m venv .venv
source .venv/bin/activate
pip install -e .
playwright install chromium
Command	Purpose
make test	Run the test suite (pytest)
make lint	Lint (ruff)
make format	Format (ruff format)
make bundle	Build a distributable archive in dist/
</details> <details> <summary><b>🧱 Project structure</b></summary> <br>
Path	Purpose
src/zoom_joiner/app.py	Desktop application (Qt / PySide6)
src/zoom_joiner/cli.py	Command-line interface
src/zoom_joiner/store.py	Persists the queue for automatic resume
src/zoom_joiner/config.py	Reads YAML, JSON, CSV, and TXT
src/zoom_joiner/models.py	Data models and statuses
src/zoom_joiner/orchestrator.py	Parallelism, retries, and cancellation
src/zoom_joiner/report.py	CSV, JSON, and HTML reports
src/zoom_joiner/backends/	Chromium / Playwright backend
setup.sh, setup.ps1	Linux and Windows installers
tests/	Unit tests
deploy/	Desktop entry and icons
</details>
🐞 Reporting Issues

This project is in beta. If you find a bug, please open an Issue and include:

Include	Why it helps
💻 Your operating system and version	Reproduce platform-specific problems
🔁 Steps to reproduce	Find the cause faster
📸 A screenshot or the Activity log output	Shows the exact error

You can also reach out through the contact card inside the app.

🤝 Contributing

Bug fixes, ideas, and feature requests are welcome.

🍴 Fork the repository
🌿 Create a branch: git checkout -b feature/my-feature
💾 Commit your changes: git commit -m "Add my feature"
📤 Push the branch: git push origin feature/my-feature
🔀 Open a pull request
⚠️ Disclaimer

[!WARNING] Zoom Downloader does not bypass Zoom's protections. A valid link and passcode are required, and recordings that require sign-in still do. Download only recordings that you own or have permission to access, and respect Zoom's terms of use and your institution's privacy rules. This project is not affiliated with or endorsed by Zoom Video Communications, Inc.

📄 License

Released under the MIT License. See LICENSE.

<div align="center">

Developed with ❤️ by Mohamed Hassan

⭐ If this tool saved you time, consider giving the repository a star.

</div>
