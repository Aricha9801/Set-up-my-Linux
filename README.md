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

### Fundementals about installation
Here are some commen ways to install software in Ubuntu:
1. The most commen way is to use **APT**. Run `apt install program-name`. It can be applied to most standard software. Make sure to run `apt update` first to refresh the software list. And run `apt upgrade` from time to time to upgrade the software. 
    - Sometimes, when the software is not in Ubuntu's default repo, or you want the latest version of a software, or you want to install multiple versions of a software, you can **add repository** of that software. After adding that, make sure to run `apt update` before installing it.
2. If you just want a specific version, or the software is not in Ubuntu default repo but provides the .deb file, you can download the **.deb** file and install it by `apt install path` or `dpkg -i path`. By `apt install` it install dependencies automatically, while `dpkg` does not install dependencies.
3. Sometimes we can use package manager like **Snap** to easily install softwares. But it is not recommended.

### WUR vpn: FortiClient
[FortiClient 7.4 ](https://www.fortinet.com/support/product-downloads/linux) does not support Ubuntu 24.04. I tried [this solution](https://www.reddit.com/r/fortinet/comments/1dzp2rn/forticlient_vpn_support_for_ubuntu_2404_lts/) and it works.
```shell
# Download libappindicator1
wget http://mirrors.kernel.org/ubuntu/pool/universe/liba/libappindicator/libappindicator1_12.10.1+20.10.20200706.1-0ubuntu1_amd64.deb 
# Download dependency required by libappindicator1
wget http://mirrors.kernel.org/ubuntu/pool/universe/libd/libdbusmenu/libdbusmenu-gtk4_16.04.1+18.10.20180917-0ubuntu8_amd64.deb
# Install both packages
sudo apt install  ./libappindicator1_12.10.1+20.10.20200706.1-0ubuntu1_amd64.deb ./libdbusmenu-gtk4_16.04.1+18.10.20180917-0ubuntu8_amd64.deb 
# Install forticlient downloaded from https://www.fortinet.com/support/product-downloads
sudo apt install ./forticlient_vpn_7.4.0.1636_amd64.deb
```
When downloading forticlient .deb, go to [Product Downloads and Free Trials](https://www.fortinet.com/support/product-downloads), scroll down to **FortiClient VPN-only**, choose **DOWNLOAD VPN for Linux .deb**.

After the installation, config the VPN.

### Install Microsoft Teams and Zoom
Make sure you did `apt update` and `apt upgrade`.

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
If you found apps like Teams and VScode are blurry, that's because [Blurry VsCode on wayland fractional scaling](https://www.reddit.com/r/Fedora/comments/wpkws3/blurry_vscode_on_wayland_fractional_scaling/ikhc12o/?utm_source=share&utm_medium=mweb3x&utm_name=mweb3xcss&utm_term=1&utm_content=share_button). Setting scales to 100% can solve it. Other solutions can be found from the link.


### Install and setup Git

```shell
sudo apt install git-all
git --version
```
```shell
git config --global user.name "Your Name"
git config --global user.email "youremail@domain.com"
```
To connect to WUR gitlab, either create an access token or set up ssh key.

To set up ssh key for WUR gitlab, see guide [SSH keys for GitLab](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://www.wur.nl/en/show/ssh-keys-for-wur-gitlab.htm&ved=2ahUKEwis6dHvzb6OAxXp0wIHHaAMBh0QFnoECBsQAQ&usg=AOvVaw1NmhXZjnZ5JJbnMxwzdTMS)

```shell
ssh-keygen -t ed25519 -C youremail@wur.nl
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
sudo apt update
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
sudo apt install curl
```
```shell
sudo apt install postgresql-17
sudo systemctl start postgresql
sudo systemctl enable postgresql
```
Then config the postgres following the guide.

Install PostGIS:
```shell
sudo apt install postgresql-17-postgis-3
```

Install pgadmin:
guide at [pgAdmin 4 (APT)](https://www.pgadmin.org/download/pgadmin-4-apt/)
```shell
curl -fsS https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo gpg --dearmor -o /usr/share/keyrings/packages-pgadmin-org.gpg
sudo sh -c 'echo "deb [signed-by=/usr/share/keyrings/packages-pgadmin-org.gpg] https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list && apt update'
sudo apt install pgadmin4
```

### Install NodeJS and npm
nodejs LTS install guide [Download Node.js](https://nodejs.org/en/download)

### Install Java and Solr
Java installation guide [How to Install Java with Apt on Ubuntu (JRE & JDK)](https://www.digitalocean.com/community/tutorials/how-to-install-java-with-apt-on-ubuntu-22-04).

Solr installation guide [Apache Solr Reference Guide](https://solr.apache.org/guide/solr/latest/getting-started/solr-tutorial.html)

To Use Solr easily, download the binary relase to your home directory, unpack:
```shell
tar -xzf solr-9.8.1.tgz
cd solr-9.8.1
```
Then you can start solr:
```shell
bin/solr start -c
```

To install solr as a service:
```shell
sudo bash solr-version/bin/install_solr_service.sh version.tgz
```
Then you can start solr by:
```shell
sudo service solr start
```

### Install QGIS
guides at [QGIS Installers](https://qgis.org/resources/installation-guide/#debian--ubuntu), make sure to change the codename when add the repo, for example, for Ubuntu 24.04 it is `noble`.






