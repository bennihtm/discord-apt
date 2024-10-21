# Discord APT repository
This repo is updated every 3 hours and hosted by Cloudflare.

Original Repo: https://github.com/palfrey/discord-apt

## Usage instructions

1. Create a file `/etc/apt/sources.list.d/discord.list` with the contents `deb [signed-by=/usr/share/keyrings/discord-benni.gpg.asc] https://discord-apt.bendaha.eu.org/debian/ ./`
2. Download the file https://discord-apt.bendaha.eu.org/discord-benni.gpg.asc to `/usr/share/keyrings/discord-benni.gpg.asc`
3. `sudo apt-get update`
4. Install the desired version

| Version | Command                               |
| ------- | ------------------------------------- |
| Stable  | `sudo apt-get install discord`        |
| PTB     | `sudo apt-get install discord-ptb`    |
| Canary  | `sudo apt-get install discord-canary` |

BTW, if you want full-colour emojis, install `fonts-noto-color-emoji`. The discord packages really should depend on that, but apparently don't for some reason.

(I have no interest in PRs to improve these instructions or helper scripts for this. They're not very hard, but I don't want to provide free support here for anyone who can't follow those instructions. If you disagree with this, either bug Discord into supporting this themselves or fork this repo and do whatever in your fork.)

## Manual update instructions

This should not be needed, as `.github/workflows/update.yml` should do this, but just in case..

1. `pip install -r requirements.txt`
2. `python get_new_package.py`
   - If this says `already have discord-<version>.deb` and there's no new .debs in the repo, there's nothing to do further.
3. `export KEY_PASSPHRASE=<key phrase for the Discord Apt Repository key>`
4. `make debian/Release.gpg`, which should regenerate all the other files.
5. Commit, push, etc and the Github Pages automation will deal with the rest.
