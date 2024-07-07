### AMD Vari Bright simply SUCKS!

#### This writeup focusses on my rant over its implementation on Linux and how to disable it
#### Click [here](#lets-fix-it-by-disabling-it) to skip to the disabling part!

It sucked on Windows and as of writing this (2024-07-07T22:45:20+00:00), it's available on Linux too now. And it continues to suck.   

**AND THE WORST PART? IT IS ENABLED BY DEFAULT ON LATEST KERNELS, TRIGGERED BY POWER-PROFILES-DAEMON, AND THERE IS NO FUCKING GUI (YET) TO DISABLE IT.** (On Windows, you atleast have a GUI to disable it)    

These are the kind of stupid decisions that keep normal people away from Linux! 

![image](https://github.com/realKarthikNair/16-xf0xxx-linux-troubleshooting/assets/78267371/bdae58d2-5e72-447e-b20e-6907c596305f)

What they don't tell you is that it not only just lowers the brightness, but also **fucks up color accuracy, contrast**, etc (I try not to use the F word on GitHub, but this one deserves it)

It gets worse : `power-profiles-daemon` can change its state and any other combination other than the `performance` governor (which only has the `performance` EPP) messes with your display color accuracy too, along with the brightness!

A `panel_power_savings` value of `0` indicates no changes to color accuracy and brightness while `4` indicates the worst possible display. 

So `powersave` with `power` EPP is the worst combination (the `Power Saver` mode on Gnome uses this power profile) since it sets a value of `4`.  
To check its value, run

```bash
cat /sys/class/backlight/amdgpu_bl1/device/amdgpu/panel_power_savings
```

`amdgpu_bl1` could be different in your device!

### Let's fix it by DISABLING it!

1. Edit power-profiles-daemon.service

```bash
sudo systemctl edit power-profiles-daemon.service
```

2. Add these lines between the pre existing comments on the file... 

```bash
### Editing /etc/systemd/system/power-profiles-daemon.service.d/override.conf
### Anything between here and the comment below will become the contents of the drop-in f>

[Service]
ExecStart=
ExecStart=/usr/libexec/power-profiles-daemon --block-action=amdgpu_panel_power

### Edits below this comment will be discarded
```

NOTE : The path `/usr/libexec/power-profiles-daemon` might vary across distributions/versions.... This is from my Fedora 40 Workstation installation. Run `systemctl status power-profiles-daemon.service` to see where your binary is!

3. Restart the service

```bash
systemctl restart power-profiles-daemon.service
```

Enjoy!!!


Citations:
- https://discussion.fedoraproject.org/t/update-reduces-color-accuracy-in-favor-of-power-efficiency-amd-gpu/124723
- https://bbs.archlinux.org/viewtopic.php?id=296000
- https://gitlab.freedesktop.org/upower/power-profiles-daemon/-/commit/126f7d3a5411f1643cb58f1791e561b6324be753#8ec9a00bfd09b3190ac6b22251dbb1aa95a0579d
- https://gitlab.freedesktop.org/drm/amd/-/issues/3432
  

