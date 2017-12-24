# PlayOnLinux Ubuntu 17 correct instalation
## Install wine
Before install PlayOnLinux, you must install WINE

```bash
sudo dpkg --add-architecture i386 
wget -nc https://dl.winehq.org/wine-builds/Release.key
sudo apt-key add Release.key
sudo apt-add-repository https://dl.winehq.org/wine-builds/ubuntu/
sudo apt-get update
sudo apt-get install --install-recommends winehq-stable
```

## Install xTerm
PlayOnLinux will need xterm to run correctly. So, you must install it as well.
```bash
sudo apt-get install xterm
```

## PlayOnLinux
For ubuntu distro, you can download deb package and install easly with `gnome-software` or some similar application. You can check mor infos [here](https://www.playonlinux.com/en/download.html)
