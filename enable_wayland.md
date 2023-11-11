Index

[On Fedora](#enable-wayland-on-fedora-workstation-gnome)  
[On Pop!_OS](#enable-wayland-on-pop_os-2204)

### Enable wayland on Fedora Workstation (gnome)

If wayland isn't working already (which should be in most of the cases) follow these

1. 

```bash
mkdir -p /home/$USER/backup/usr/lib/udev/rules.d/
sudo mv /usr/lib/udev/rules.d/61-gdm.rules /home/$USER/backup/usr/lib/udev/rules.d/
```

2. Reboot.

3. You should have the Wayland option in GDM password window's bottom right corner clog button. 

### Enable wayland on Pop!_OS 22.04

**Wayland works out of the box on Fedora 38+**

> ⚠️ It works for me but if something breaks for you, I won't be able to help. So please don't make these changes if you're pretty new to Linux and/or can't troubleshoot issues that may arise.... 

1. In `/etc/gdm3/custom.conf`, comment out the below line 

    ```
    WaylandEnable=false
    ```
    
    to this 

    ```
    # WaylandEnable=false
    ```

2. in `/boot/efi/loader/entries/Pop_OS-current.conf`, comment out below line

    ```
    RUN+="/usr/libexec/gdm-runtime-config set daemon WaylandEnable false"
    ```

    to this 

    ```
    # RUN+="/usr/libexec/gdm-runtime-config set daemon WaylandEnable false"
    ```

3. Enable DRM for NVIDIA driver: Add `nvidia-drm.modeset=1` to `/boot/efi/loader/entries/Pop_OS-current.conf`
4. Reboot and choose Wayland in after clicking on the clog icon on GDM login screen (bottom right)
