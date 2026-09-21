# Veto OTT

Windows broadcast graphics application with separate Davis Cup and Billie Jean
King Cup template libraries, preview queues, and DeckLink output.

## Repository Layout

On the broadcast PC, the Git repository is `D:\` and the active application stays
in `D:\Veto OTT`. No app files need to move. Only the explicitly allowed source
files and required graphic assets are eligible for tracking.

Older folders (`Veto Live`, `Veto`, `old`, `older`), archives, installed packages,
FFmpeg binaries, shortcuts, logs, backups and the entire application `data`
directory are excluded. Do not use `git add -f` to bypass these exclusions.

This repository is a **code backup**, not a backup of the saved presets, uploaded
media, credentials or browser drafts. Back up `Veto OTT\data` separately and
privately to preserve both competition libraries and their uploaded assets.

## Run on This PC

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File "D:\Veto OTT\start_scoreboard.ps1"
```

Dashboard: http://127.0.0.1:8080/scoreboard

Do not restart or replace application code while SDI output is active.

## Fresh Installation

Install 64-bit Python 3.14 with pip and Tcl/Tk. From the cloned repository run:

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File ".\Veto OTT\setup_scoreboard.ps1" -NoStart
powershell.exe -NoProfile -ExecutionPolicy Bypass -File ".\Veto OTT\start_scoreboard.ps1"
```

Setup downloads dependencies when offline wheels are absent. Install FFmpeg
separately for video playback/export, either in PATH or at
`Veto OTT\tools\ffmpeg\bin\ffmpeg.exe`. Physical SDI also requires compatible
DeckLink hardware and the Blackmagic Desktop Video driver. Machine-specific
Windows shortcuts are not part of the Git checkout.

New installations generate unique editor and delete passwords. Read them locally
from `Veto OTT\data\first_run_credentials.json`, store them privately, and remove
that plaintext recovery file once they are recorded securely. Never upload it.
Existing installations keep their current hashed credential files and logins.

## First GitHub Push

Before committing, remove any built-in passwords or tokens from source and review
the exact staged files. Local credential files must remain excluded. A private
GitHub repository is appropriate until the code and bundled assets have been
reviewed for public distribution.

Create an empty repository on GitHub without a README, license or .gitignore.
Then run the following in PowerShell, substituting your author identity and URL:

```powershell
Set-Location D:\
$git = 'C:\Program Files\Git\cmd\git.exe'
& $git config user.name 'YOUR NAME'
& $git config user.email 'YOUR GITHUB EMAIL OR NOREPLY ADDRESS'
& $git status --short
& $git add -- .gitignore .gitattributes README.md 'Veto OTT'
& $git diff --cached --stat
& $git diff --cached
& $git commit -m 'Initial Veto OTT source'
& $git remote add origin 'https://github.com/YOUR-ACCOUNT/YOUR-REPOSITORY.git'
& $git push -u origin main
```

Complete GitHub authentication through Git's sign-in flow. Never put a password
or access token in the remote URL, source files or command history.

Reference: [GitHub: adding locally hosted code](https://docs.github.com/en/migrations/importing-source-code/using-the-command-line-to-import-source-code/adding-locally-hosted-code-to-github).
