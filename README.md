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
Table of Contents
		
Overview	Usage	Command line
Features	Options	Data locations
Download	Naming and organizing	Building from source
Installation	Troubleshooting	Contributing
Overview

Zoom cloud recordings are easy to lose once a course or a meeting series ends. Zoom Downloader is a desktop application that takes your recording share links and passcodes and downloads the files directly from Zoom's CDN using parallel connections. Quality is identical to the original, and it is much faster than downloading one recording at a time from the browser.

Paste your links, press one button, and get an organized folder of recordings.

<!-- Add a screenshot here: ![Zoom Downloader](docs/screenshot.png) -->
What's new in 1.5.2
Change	Details
Accurate progress bar	Reaches 100% only after the file is fully saved; stays at 99% while parts are merged
Contact card	A small card inside the app for feedback and suggestions
Rename by date	Now also works on recordings downloaded earlier
Features
Feature	Details
Native desktop app	Dark Qt interface, not a browser tab
Direct CDN download	Captures the signed video URL from Zoom's player, then downloads with up to 16 parallel connections per file
Queue	Add links at any time; they join the running queue and are processed in turn
Automatic resume	The queue is saved to disk, so closing the app, losing the connection, or rebooting does not lose progress
Pause and resume	Pausing stops new downloads and keeps the parts already written
Passcode per recording	A passcode on each line, with a default passcode as a fallback
Flexible naming	Custom names, or sequence numbering for several rows at once
No overwrites	A duplicate name is saved as Name (2)
Output formats	Video (mp4), audio only (m4a), transcript (vtt)
Rename by date	Organizes a folder as Name YYYY-MM-DD.mp4 using the date in the video metadata
Command line	Scriptable downloads for automation
Download

Download one file for your system from the Releases page.

System	File	Install
🪟 Windows	zoom-downloader-windows.zip	Extract, then run setup.ps1
🐧 Linux (x86_64)	zoom-downloader-linux-x86_64.tar.gz	Extract, then run ./setup.sh
🚀 Installation

ℹ️ Installation needs an internet connection once, to fetch the Python packages and the Chromium engine.

Requirements
Requirement	Notes
Python 3.10 or later	Checked by the installer
Chromium	Installed automatically through Playwright; an existing Google Chrome also works
Operating system	Windows or Linux (x86_64)
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
Usage

Launch Zoom Downloader from the applications menu, or run zoom-joiner-gui in a terminal.

Step	Action
1	Copy the share link from the email or meeting chat where Zoom shared the recording
2	Copy the passcode. If the link already contains ?pwd=..., the passcode can be left empty
3	Paste the links into the box on the left and press Add to the list
4	Choose the folder where the files will be saved
5	Press Download all recordings

If the app is closed or the connection drops, open it again and press the same button; the download continues from where it stopped.

Input format

One recording per line. The name is optional.

share-link  passcode  name
https://us06web.zoom.us/rec/share/AbCdEf...  123456  Weekly Team Sync
https://us06web.zoom.us/rec/share/XyZ123...  654321  Client Review
Field	Required	Description
Share link	Yes	Starts with https://.../rec/share/
Passcode	If not in the link	The value after ?pwd=, or the passcode Zoom sent with the link
Name	No	Used as the saved file name
Interface overview
Section	Purpose
Top bar	Download all recordings, Pause, progress bar, application status
1. Paste the recording links	Paste links, then Add to the list or Paste from clipboard
2. Options	Default passcode, save folder, connections per file, video, audio, transcript
Organize an existing folder	Rename files by date, with an optional base name
3. Recording list	Each recording with its live status; right-click to rename
Activity log	Live log of the application's actions
How to use	Built-in help window
Options
Option	Default	Description
Default passcode	Empty	Used for any link without its own passcode
Save to	~/Downloads/zoom-recordings	Destination folder
Connections per file	16	Number of parallel connections for each file
Video file (mp4)	On	Download the video recording
Audio only (m4a)	Off	Download the audio track only
Transcript (vtt)	Off	Download the transcript
Naming and Organizing
Renaming items in the list
Action	Result
Right-click a row, or double-click it	Rename that recording
Select several rows, then choose Name as a sequence	Numbers them in one step (for example, Lecture 1 to 12)
Two recordings with the same name	The second is saved as Name (2); files never overwrite each other
Organizing an existing folder

Use Rename files by date on any folder of recordings. It runs on the folder selected in Save to.

Base name	Result
Entered (for example, DAV-R)	Every file becomes DAV-R YYYY-MM-DD.mp4; files that share a date are numbered
Left empty	Only missing dates are added to existing names

The date is read from the video metadata, so files downloaded earlier are supported.

Troubleshooting
Problem	Solution
Zoom asks to sign in	The owner restricted the recording. Open the link once in your browser, sign in, then retry in the app
Download fails with a passcode error	Check the passcode, or set the Default passcode in Options
Download stops after a connection drop	Open the app and press Download all recordings again; it resumes from where it stopped
Installer cannot find Python	Install Python 3.10 or later, then run the installer again
Environment problems	Run zoom-joiner doctor to check Playwright and Chromium
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
Command	Purpose
zoom-joiner download ...	Download recordings from the terminal
zoom-joiner app	Launch the desktop app (same as zoom-joiner-gui)
zoom-joiner doctor	Check the environment (Playwright and Chromium)
zoom-joiner --help	List all commands

The CLI also retains an older feature for joining live meetings in bulk (zoom-joiner run and zoom-joiner gui). It is no longer part of the desktop app.

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
Command	Purpose
make install	Development environment and Chromium
make test	Run the test suite (pytest)
make lint	Lint (ruff)
make format	Format (ruff format)
make bundle	Build a distributable archive in dist/
Project structure
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
Reporting Issues

This project is in beta. Please open an Issue and include:

Information	Why it helps
Operating system and version	Reproduce platform-specific problems
Steps to reproduce	Find the cause faster
Screenshot or Activity log output	Shows the exact error

You can also reach out through the contact card inside the application.

Contributing

Bug fixes, ideas, and feature requests are welcome.

Step	Command
1. Fork the repository	
2. Create a branch	git checkout -b feature/my-feature
3. Commit your changes	git commit -m "Add my feature"
4. Push the branch	git push origin feature/my-feature
5. Open a pull request	
⚠️ Disclaimer

Zoom Downloader does not bypass Zoom's protections. A valid link and passcode are required, and recordings that require sign-in still do. Download only recordings that you own or have permission to access, and respect Zoom's terms of use and your institution's privacy rules. This project is not affiliated with or endorsed by Zoom Video Communications, Inc.

License

Released under the MIT License. See LICENSE.

<div align="center">

Developed by Mohamed Hassan

</div>
