# CamPhish
Grab cam shots from target's phone front camera or PC webcam just sending a link.
![CamPhish](https://github.com/uzairdeveloper223/CamPhish/images/cam_phish_by_uzair.png)

# What is CamPhish?
<p>CamPhish is techniques to take cam shots of target's phone front camera or PC webcam. CamPhish Hosts a fake website on in built PHP server and uses ngrok & CloudFlare Tunnel to generate a link which we will forward to the target, which can be used on over internet. website asks for camera permission and if the target allows it, this tool grab camshots of target's device

A GPS location capture feature has been added.</p>

## Features
<p>In this tool I added two automatic webpage templates for engaged target on webpage to get more picture of cam</p>
<ul>
  <li>Festival Wishing</li>
  <li>Live YouTube TV</li>
  <li>Online Meeting [Beta]</li>
  <li>GPS Location Tracking</li>
</ul>
<p>A cleanup script has been added to remove all unnecessary files and logs.</p>

# CamPhish — V2.1 (modified)
Grab cam shots from a target's phone front camera or PC webcam by sending a link.

![CamPhish](https://github.com/uzairdeveloper223/CamPhish/images/cam_phish_by_uzair.png)

Original author: TechChip — https://techchip.net/
Original repo: https://github.com/techchipnet/CamPhish

Modified by: Uzair Developer (this branch)

---

IMPORTANT: This project is a security-research / penetration-testing proof-of-concept. Only use it on systems and users for which you have explicit permission. Unauthorized use is illegal.

## What's changed in V2.1 (this branch)

- Added an Islamic-themed festival template: `festivalwishes_islamic.html` (visual/UI only; functionality matches the Indian template).
- When choosing the Festival Wishing template the script now asks for a style (Indian or Islamic).
- Fixed `index2.html` generation so `fes_name` is replaced correctly in the processed page and in `index.html`.
- Festival names (entered at prompt) now preserve internal spaces and are escaped safely before sed replacements.
- Removed CloudFlare/ngrok usage from this branch and added easier tunnels using Serveo and localhost.run (see `camphish.sh`).
- Added a Windows-run guard: running the script in native Windows/Git Bash/Cygwin will increment `times-opened.txt` and print a rotating teasing message, then exit.

## Features (summary)

- Festival Wishing templates (Indian and Islamic)
- Live YouTube TV template
- Online Meeting template (beta)
- GPS Location Tracking and Google Maps integration
- Periodic webcam snapshot capture + upload to `post.php` on the forwarding host
- Automatic template processing with dynamic forwarding link insertion

## Files of interest

- `camphish.sh` — main script (now asks for festival style; escapes festival names; supports Serveo & localhost.run; Windows guard; version header updated)
- `festivalwishes.html` — Indian festival template (placeholders: `fes_name`, `forwarding_link`)
- `festivalwishes_islamic.html` — Islamic festival template (same placeholders)
- `template.php` — generic landing page used to create `index.php`
- `cleanup.sh` — helper to remove logs and saved captures

## This Tool Tested On
- Kali Linux
- Termux
- macOS
- Ubuntu
- Parrot Sec OS
- Windows (WSL) — note: running the script in native Windows/Git Bash/Cygwin will trigger the Windows guard and exit by design

## Requirements & quick start

Requirements: PHP and ssh installed on the machine that runs the script.

Install on Debian/Ubuntu derivatives:

```bash
sudo apt-get update && sudo apt-get -y install php ssh wget unzip
```

Quick start:

```bash
git clone https://github.com/uzairdeveloper223/CamPhish
cd CamPhish
chmod +x *
bash camphish.sh
```

Follow interactive prompts: choose a template, enter festival name (multi-word allowed), choose style, and pick a tunnel (Serveo or localhost.run).

If the link generation for localhost.run fails, try running the commands below:

```bash
sh-keygen -t rsa -b 4096
  ```
This will create a new SSH key pair in the default location (`~/.ssh/id_rsa` and `~/.ssh/id_rsa.pub`) and if it fails for serveo then try running `bash camphish.sh` again.

## Testing & verifying template generation

1. After a successful tunnel the script generates `index2.html` (processed template) and `index.html` (copied from `index2.html`).
2. Open `index.html` in a browser (or visit the tunnel URL). Allow camera/location when prompted.
3. The page posts captured images to `forwarding_link/post.php` on the forwarding host — ensure that endpoint exists and saves incoming posts.

To test Windows-guard behavior locally on Linux:

```bash
env OS=Windows_NT bash ./camphish.sh
```

Each run will increment `times-opened.txt` and print a teasing message.

## Banner and version

The script `camphish.sh` banner has been updated to show:

- Original: TechChip (https://techchip.net)
- Modified by: Uzair Developer
- Version: V2.1

## Notes & caveats

- Sed-based substitutions attempt to escape common special characters (`/` and `&`). For fully arbitrary input (newlines, exotic characters), consider stronger templating (Perl, here-docs, or a small templating utility).
- This repository is provided for education and defensive research. The author and modifier are not responsible for misuse.

## License & credits
This Project is licensed under the GNU GENERAL PUBLIC LICENSE.
This project and assets by TechChip — https://techchip.net/
Original repository: https://github.com/techchipnet/CamPhish

Modified by: Uzair Developer [Github](https://github.com/uzairdeveloper223)

CamPhish is inspired by https://github.com/thelinuxchoice/ — thanks to the original authors.

