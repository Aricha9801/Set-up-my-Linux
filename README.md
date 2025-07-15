# Set-up-my-Linux
As a beginner of Linux, this guide shows how did I set up my Linux system (Ubuntu 24.04) step by step.

> Me: GIS developer, Python, PostgreSQL and front-end developing.<br>
> Working institute: ISRIC<br>
> Device: ThinkPad-T14-Gen-4, previous system: Windows 11<br>

## Install Ubuntu
I chose to wipe up my windows system. Can also chose to create a dual boot to have Windows and Ubuntu.
- Dual boot: First partition the hard drive. See guides [How to Set Up a Dual Boot with Ubuntu and Windows](https://gcore.com/learning/dual-boot-ubuntu-windows-setup).
- Ubuntu only: First backup your files.

For the installation, check the guide [Ubuntu installation tutorial](https://ubuntu.com/tutorials/install-ubuntu-desktop#1-overview)

It is recommended to use LTS.

For WUR environment, when it comes to problem about Secure Boot Violation, got to ServiceDesk for help.

## Shortcuts
Shortcuts for terminals can be found and edited at Edit -> preferences -> Shortcuts
| Shortcut    | Use |
| -------- | ------- |
| Ctrl + Alt + T  | open the terminal   |
| Super (Win) | show all activities    |
| Ctrl + L    |  clear the terminal screen   |


## Terminal commands


## First setup
Update:
```shell
sudo apt update && sudo apt upgrade -y
```

## Installations

### Install Microsoft Teams
Make sure you did apt update and apt upgrade

```shell
sudo apt install snapd
sudo snap install teams-for-linux
Teams-for-linux –-version
teams-for-linux
```
### Install VScode

Download the .deb [Download Visual Studio Code](https://code.visualstudio.com/Download)
```shell
sudo dpkg -i ~/Downloads/code_1.XXX.deb
code
```
If you found apps like Teams and VScode are blurry, that's because [Blurry VsCode on wayland fractional scaling ](https://www.reddit.com/r/Fedora/comments/wpkws3/blurry_vscode_on_wayland_fractional_scaling/ikhc12o/?utm_source=share&utm_medium=mweb3x&utm_name=mweb3xcss&utm_term=1&utm_content=share_button). Setting scales to 100% can solve it. Other solutions can be found from the link.

### Install and setup Git

```shell
sudo apt install git-all
git --version
```
```shell
git config --global user.name "Your Name"
git config --global user.email "youremail@domain.com"
```


