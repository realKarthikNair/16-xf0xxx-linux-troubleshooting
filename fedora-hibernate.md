`/etc/UPower/UPower.conf`

```
CriticalPowerAction=Hibernate
```

```bash
karthik@fedora:~$ cat /usr/lib/systemd/system-sleep/nvidia 
#!/bin/bash

case $1/$2 in
  pre/*)
    # echo "Going to $2..."
    /usr/bin/echo "0" > /sys/class/vtconsole/vtcon0/bind
    /usr/sbin/rmmod nouveau
    ;;
  post/*)
    # echo "Waking up from $2..."
    /usr/sbin/modprobe nouveau
    /usr/bin/echo "1" > /sys/class/vtconsole/vtcon0/bind
    ;;
esac
```
Use https://github.com/DavidS95/Smokeless_UMAF and set Modern Standby Type to `<Modern Standby + s0i2+ s0i3>`

