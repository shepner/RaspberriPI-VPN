# installation instructions

## initial setup

make sure everything is wired up as outlined in the hardware section

Flash a micro SD with [RASPBIAN STRETCH LITE](https://www.raspberrypi.org/downloads/raspbian/) using [Etcher](https://etcher.io/)

Attach an HDMI monitor.  Attach a keyboard to the USB port.  Attach power to the PWR port (its the one closer to the end of the board)

Default login U/P:  pi/raspberry

---

`sudo raspi-config`

1) network options>hostname: PiVPN
2) network options>Wi-Fi:
    US
    ssid
    password
3) localization options: select "en_US.UTF-8 UTF-8" as the default
4) interfacing options:  ssh

---

set root's password (this must be done from the console)
``` shell
sudo passwd root
logout
```

login as root

``` shell
usermod -l newusername pi
usermod -m -d /home/newusername newusername
passwd newusername
logout
```

login as newusername

``` shell
#test sudo access
sudo apt-get update

#disable root access
sudo passwd -l root 
```

---

Now `sudo reboot` and make sure it connects to WiFi.  You make want to login to the console and run `ifconfig -a` to find out what IP address was assigned

You *should* be done with the keyboard and monitor at this point.  Make sure you can login (ie `ssh pi@<ip address>`) before disconnect them.

## update

``` shell
cat > update.sh << `filecontents`
#!/bin/sh

sudo apt-get update && sudo apt-get -y upgrade && sudo apt-get -y dist-upgrade && sudo apt -y autoremove
filecontents

chmod 755 update.sh
```




## install [PiVPN](http://www.pivpn.io/)

``` shell
curl -L https://install.pivpn.io | bash
```



