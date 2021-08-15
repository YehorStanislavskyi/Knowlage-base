# ubuntu settings

## NUM LOCK при старте системы 

```text
sudo apt-get update
sudo apt-get -y install numlockx
sudo sed -i 's|^exit 0.*$|# Numlock enable\n[ -x /usr/bin/numlockx ] \&\& numlockx on\n\nexit 0|' /etc/init.d/rc.local
```

