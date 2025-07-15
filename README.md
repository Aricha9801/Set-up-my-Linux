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
Check tutorial [The Linux command line for beginners](https://ubuntu.com/tutorials/command-line-for-beginners#1-overview)

## First setup
Update:
```shell
sudo apt update && sudo apt upgrade -y
```

## Installations

For the daily work operations, most apps are available as webpages, including Outlook, Office, and Teams.

Choose a browser you like, by default it has Firefox, otherwise install other browsers and import your bookmark.

### WUR vpn: FortiClient
install guide [FortiClient 7.4 ](https://www.fortinet.com/support/product-downloads/linux)
No support for Ubuntu 24.04, do it later.


### Install Microsoft Teams and Zoom
Make sure you did apt update and apt upgrade

```shell
sudo apt install snapd
sudo snap install teams-for-linux
Teams-for-linux –-version
teams-for-linux
```

```shell
sudo snap install zoom-client
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
To connect to WUR gitlab, either create a access token or set up ssh key.

To set up ssh key for WUR gitlab, see guide [SSH keys for GitLab](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://www.wur.nl/en/show/ssh-keys-for-wur-gitlab.htm&ved=2ahUKEwis6dHvzb6OAxXp0wIHHaAMBh0QFnoECBsQAQ&usg=AOvVaw1NmhXZjnZ5JJbnMxwzdTMS)

```shell
ssh-keygen -t ed25519 -C pietje.puk@wur.nl
```
Then paste the xxx.pub, in Gitlab add the ssh key.

Now try clone a repo and push a commit.

Then add the same ssh key to Github and test it.

Optional: install a Git GUI tool, such as GitKraken:

Install the .deb at [GitKraken Desktop Download](https://www.gitkraken.com/download/linux-deb)

```shell
sudo dpkg -i ~/Downloads/gitkraken-amd64.deb
```

### Install Python
Ubuntu has python 3.12. Can verify it by:
```shell
python3 --version
```
install pip and venv:
```shell
sudo apt-get update
sudo apt install python3-pip -y
sudo apt install python3-venv -y
```
### Install PostgreSQL
It is recommended to add the Postgres repo.
PostgreSQL 17 installation guide [PostgreSQL 17 Installation on Ubuntu 24.04](https://dev.to/johndotowl/postgresql-17-installation-on-ubuntu-2404-5bfi)
```shell
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
curl -fsSL https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/postgresql.gpg
sudo apt update
```
If curl not installed make sure to install it:
```shell
sudo apt-get install curl
```
```shell
sudo apt install postgresql-17
sudo systemctl start postgresql
sudo systemctl enable postgresql
```
Then config the postgres following the guide.

Install pgadmin:
guide at [pgAdmin 4 (APT)](https://www.pgadmin.org/download/pgadmin-4-apt/)
```shell
curl -fsS https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo gpg --dearmor -o /usr/share/keyrings/packages-pgadmin-org.gpg
sudo sh -c 'echo "deb [signed-by=/usr/share/keyrings/packages-pgadmin-org.gpg] https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list && apt update'
sudo apt install pgadmin4
```
Install PostGIS:
```shell
sudo apt install postgresql-17-postgis-3
```

### Install node and npm
nodejs LTS install guide [Download Node.js](https://nodejs.org/en/download)






