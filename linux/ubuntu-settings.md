# ubuntu settings

## базовые утилиты&#x20;

```bash
$ sudo apt-get install git  curl zip gnome-tweak-tool ranger nvim flameshot htop telegram-desktop unzip -y
```



### установка gnome-tweak-tolls

```
sudo apt-get install  
```

### NUM LOCK при старте системы

```
org.gnome.desktop.peripherals.keyboard remember-numlock-state true
```

### тема иконок papirus

```
sudo add-apt-repository ppa:papirus/papirus
sudo apt install papirus-icon-theme
```

В tweak-tools выбрать их!

### установка albert&#x20;

```
echo 'deb http://download.opensuse.org/repositories/home:/manuelschneid3r/xUbuntu_21.04/ /' | sudo tee /etc/apt/sources.list.d/home:manuelschneid3r.list
curl -fsSL https://download.opensuse.org/repositories/home:manuelschneid3r/xUbuntu_21.04/Release.key | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/home_manuelschneid3r.gpg > /dev/null
sudo apt update
sudo apt install albert
```

