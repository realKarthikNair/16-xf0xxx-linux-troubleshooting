Making linux related notes and troubleshooting for HP Omen 16 R7 7840HS RTX 4060 (16-xf0xxx) 

# What works and what doesn't

**Based on Pop!_OS 22.04 and Fedora Workstation 39**  

*Wherever I haven't mentioned "Windows", the issue affects Linux only.*

| Component | Works? | Notes |
| --------- | ------ | ----- |
| Display | :heavy_check_mark: |  - VRR works from GNOME 46 (tested on Fedora Workstation 40) <br><br> - HDR doesn't work since Linux doesn't support HDR yet. <br><br> - Displays colors by default are good enough. For even better color repro, use Adobe RGB color profile. | 
| Keyboard | :heavy_check_mark: | - Keyboard backlit can be turned ON and OFF from Linux <br><br> - You can't control the RGB settings of keyboard on this model from Linux yet. [hp-omen-linux-module](https://github.com/pelrun/hp-omen-linux-module) doesn't work either. However, if you're on dual boot, (only static) RGB settings changed from Windows will persist on Linux. <br><br> - You can't control the brightness of the keyboard from Linux either <br><br> - Surprisingly, the calculator key does launch the calculator app on Gnome <br><br> - Orange indicator on mute button doesn't work on Linux but the button itself does the mute/unmute function | 
| CPU | :heavy_check_mark: <br><br> (Please read the notes on this one) |  - AMD-pstate works from kernel 6.5.x <br><br> - Please update the BIOS for improved performance of the 7840HS| 
| HDMI | :heavy_check_mark: | - HDMI works as expected. |
| DisplayPort | :heavy_check_mark: | - DisplayPort works as expected (but only when booted on dGPU) |
| Ethernet RJ45 | :heavy_check_mark: | - Ethernet works as expected. |
| Ryzen AI (AMD XDNA) |  :heavy_check_mark: | - HP has enabled it on BIOS so works on Windows but Linux doesn't have support for Ryzen AI yet :( |  
| GPU (RTX 4060) | :heavy_check_mark: | - Use proprietary drivers <br><br> -To enable Dynamic Boost (thus changing max TGP from 80W to 140W) follow [this](https://github.com/realKarthikNair/16-xf0xxx-linux-troubleshooting/blob/main/enable-max-TGP.md) <br><br> - On Fedora, use negativo17 repo for CUDA and cuDNN; read more [here](https://github.com/realKarthikNair/16-xf0xxx-linux-troubleshooting/blob/main/fedora39-tensorflow-gpu.md) <br><br> -Use [EnvyControl](https://github.com/bayasdev/envycontrol) to switch between GPU modes (integrated, hybrid and nvidia)  
| Battery | :heavy_check_mark: |  - Battery life varies from 2-6 hours on Fedora Linux 40 Workstation Edition depending on the workload. <br><br> - You can't see the battery cycle count on Linux <br><br> - You can't set battery capacity limits on both Linux and Windows <br><br> - The battery life is similar, if not better than Windows <br><br> - Battery charges upto 84.66 Wh while the design capacity is 83.Wh. On Windows, the capacity is 81.0 Wh. | 
| Speaker |  |  - On Pop!_OS, speakers are buggy, no matter the kernel <br><br> - Speakers work fine on Fedora 39/40 but doesn't sound even nearly as good as Windows (Windows have DSP hacks, similar setup can be reproduced on Linux using JamesDSP <br><br> - Also, check [this](/speaker_pins.png) out |
| Headphone jack |  | - Headphone jack is buggy on Pop!_OS <br><br> - Works as expected on Fedora 39/40 |
| Microphone | :heavy_check_mark: |  - Microphone works as expected. |
| Webcam | :heavy_check_mark: |  - Webcam works as expected. |
| Fans | :heavy_check_mark: |  - Fans seems to work fine (it does work when temps are above 40-50 degree celcius) though lm-sensors doesn't show the fan speed. <br><br> - I will update this section later. <br><br> - You can't manually control fans of this machine on Linux yet |
| Touchpad | :heavy_check_mark: |  - Touchpad works as expected. <br><br> - multi touch gestures works too. |
| Fingerprint reader |  |  - My model doesn't have a fingerprint reader. Someone else will have to test this. |
| USB ports | :heavy_check_mark: <br><br> | - All USB ports work fine <br><br> |
| Bluetooth | :heavy_check_mark: | | 
| WiFi | :heavy_check_mark: | - HP has put a MediaTek wifi card in this laptop. It works fine most of the time but does glitch sometimes in ~both Linux and~ Windows <br><br> - Use `sudo iw wlo1 set power_save off` to disable power saving mode on the WiFi card  | 
| Suspend/sleep | :heavy_check_mark: | - If you face random logouts after waking up from suspend, follow [this](https://github.com/realKarthikNair/16-xf0xxx-linux-troubleshooting/blob/main/fix_suspend.md) <br><br> - Suspend doesn't work if sleep state is set to S3 (deep) | 
| Hibernation |  | - Always unreliable even when made to work |
