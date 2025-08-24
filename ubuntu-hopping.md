Created: 2025-8-24
---

# Switching from Windows to Ubuntu

I'm now pretty comfortable in Ubuntu. Below is a small guide (to myself) on alternatives and switching from Windows.

With Pewdiepie's new Linux psyopping, this may be useful to new people taking the leap. Maybe.

## Bitlocker/Encryption

Right now TPM backed full disk encryption is [experimental on 25.10](https://discourse.ubuntu.com/t/ubuntu-desktop-25-10-the-questing-quokka-roadmap/61159). We await, for now one has to type 2 passwords to log in if you want encryption to a Windows level.

With the current installer wizard, I don't believe it sets up 2nd drive unlocking on boot, so you need to mess with `fstab` and stuffs I believe, which is quite spooky.

## Onedrive

Currently it appears [abraunegg's onedrive](https://github.com/abraunegg/onedrive) is the easiest onedrive solution. You will need to edit a config to [set up](https://github.com/abraunegg/onedrive/blob/b4179d1f27ea8a3800f003b12fe3a8c6a89e7a80/docs/usage.md#compatibility-with-obsidian) Obsidian. Apparently Obsidian saves every keystroke and is quite bad for your drive's lifespan. 

You will also see a warning upon every login that [Curl has bugs](https://github.com/abraunegg/onedrive/discussions/2997) due to Ubuntu/Debian shipping a crappy version, and that we should petition Ubuntu to fix things. Thanks Canonical

![OneDrive Warning that Curl is out of date](onedrivewarning.png)

I suspect I may be moving away from Onedrive in the future and a simpler Google Drive client may be on the play in future.

## Cryptomator

With cloud storage, I like to encrypt the files that go in the cloud as well.

Cryptomator is available, but I always have trouble with AppImages (I wish there was an inbuilt AppImage handler) so instead I go with their PPA for auto updates as well. I don't think AppImage does auto updates.

The biggest issue is that snaps can't access the default mount location, so you will have to edit the default path. [See this discussion](https://github.com/cryptomator/cryptomator/discussions/3922) for details.


## Voidtool's Everything

[Voidtool's everything](https://www.voidtools.com/) is a super duper useful tool on Windows for instant search of your whole filestylem. Useful for devs trying to find all their configuration files and stuff.x 

[fsearch](https://github.com/cboxdoerfer/fsearch) This is a hairer app to install, but it should be pretty safe, problem is the search style isn't the same.

## Steam

Honestly beautiful work. May need to explicitly set the Proton version

## Remote Desktop

Tailscale is a godsend mild learning curve with setting up permissions. It appears to launch before login so must be a system wide installation. Windows works seamlessly to remote into Ubuntu AND my trackpad shortcut to middle click actually works. Only huge bug I notice is huuge FPS drop about 5 minutes into the session, which my be alleviated by enabling the exit node?

## Installing Applications

How I choose which method to install an application:

I tend to prefer the author's listed method where I'm hoping for a Snap, then a PPA. I'd prefer using a web app than downloading a tool via the terminal generally.

Downsides of the other ones.
- Flatpak: Weird UX of 2 different app managers
- AppImage: Annoying to setup the `.desktop` service (no GUI) and sometimes broken icons
- .deb: No auto updates

## Shortcuts

- Win + E: Open file explorer

## Aliases

```bash
alias updateall='apt-get update && sudo apt-get upgrade && sudo apt-get dist-upgrade'

# Open the file explorer inside this directory
alias openhere='nautilus .'

alias onedrivelogs='journalctl --user-unit=onedrive -f'
alias cputemps="paste <(cat /sys/class/thermal/thermal_zone*/type) <(cat /sys/class/thermal/thermal_zone*/temp) | column -s $'\t' -t | sed 's/\(.\)..$/.\1°C/'"
alias diskspace="du -xhd1 /home/$USERNAME | sort -hr"
```

