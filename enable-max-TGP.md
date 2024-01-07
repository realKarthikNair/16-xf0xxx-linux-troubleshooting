# Enabling NVIDIA Dynamic Boost

By default, the maximum TGP on this machine is the same as the default TGP (which 80W)
To unlock higher TGP (upto 140W), run these commands 

```bash
sudo cp  /usr/share/doc/NVIDIA_GLX-1.0/nvidia-dbus.conf /etc/dbus-1/system.d/
systemctl enable nvidia-powerd.service
systemctl start nvidia-powerd.service
```

source : https://download.nvidia.com/XFree86/Linux-x86_64/545.29.02/README/dynamicboost.html

**Please note that on battery, max TGP is capped at 45W**

You can always check TGP limits using ```nvidia-smi```
