Making linux related notes and troubleshooting for HP Omen 16 R7 7840HS RTX 4060 (16-xf0xxx) 

# What works and what doesn't

**Based on Pop!_OS 22.04 and Fedora Workstation 39**  

*Wherever I haven't mentioned "Windows", the issue affects Linux only.*

| Component | Works? | Notes |
| --------- | ------ | ----- |
| Display | :heavy_check_mark: |  - The latest kernel as of writing this is 6.5.7 and it only supports 165Hz and 60Hz. For more options [60, 90, 120, 144, 165]Hz you need to use the 6.4.6-76060406-generic kernel. Reasons behind this regression is unknown. Kernels older than 6.4.6-76060406-generic also gives only 165Hz and 60Hz <br><br> - HDR doesn't work since Linux doesn't support HDR yet. <br><br> - Displays colors by default are good enough. For even better color repro, use Adobe RGB color profile. | 
| Keyboard | :heavy_check_mark: | - You can't control the RGB settings of keyboard on this model from Linux yet. [hp-omen-linux-module](https://github.com/pelrun/hp-omen-linux-module) doesn't work either. However, if you're on dual boot, RGB settings changed from Windows will persist on Linux. <br><br> - You can't control the brightness of the keyboard from Linux either <br><br> - Surprisingly, the calculator key does launch the calculator app on Gnome | 
| CPU | :heavy_check_mark: <br><br> (Please read the notes on this one) |  - AMD-pstate works from kernel 6.5.x | 
| GPU (RTX 4060) | :heavy_check_mark: | - Use proprietary drivers <br><br> -To enable Dynamic Boost (thus changing max TGP from 80W to 150W) follow [this](https://github.com/realKarthikNair/16-xf0xxx-linux-troubleshooting/blob/main/enable-max-TGP.md) |
| Battery | :heavy_check_mark: |  - Battery life varies from 2-8 hours depending on the workload. <br><br> -Fedora 39 provides better battery life than Pop!_OS 22.04 <br><br> - The battery life is similar, if not better than Windows <br><br> - Battery charges upto 84.66 Wh while the design capacity is 83.Wh. On Windows, the capacity is 81.0 Wh. | 
| Speaker |  |  - On Pop!_OS, speakers are buggy, no matter the kernel <br><br> - Speakers work fine on Fedora 39 |
| Headphone jack |  | - Headphone jack is buggy on Pop!_OS <br><br> - Works as expected on Fedora 39 |
| Microphone | :heavy_check_mark: |  - Microphone works as expected. |
| Webcam | :heavy_check_mark: |  - Webcam works as expected. |
| Fans | :heavy_check_mark: |  - Fans seems to work fine (it does work when temps are above 40-50 degree celcius) though lm-sensors doesn't show the fan speed. <br><br> - I will update this section later. <br><br> - You can't manually control fans of this machine on Linux yet |
| Touchpad | :heavy_check_mark: |  - Touchpad works as expected. <br><br> - multi touch gestures works too. |
| Fingerprint reader |  |  - My model doesn't have a fingerprint reader. Someone else will have to test this. |
| USB ports | :heavy_check_mark: <br><br> | - All USB ports work fine <br><br> - I am yet to test their data transfer speeds |
| Bluetooth | :heavy_check_mark: | | 
| WiFi | :heavy_check_mark: | - HP has put a MediaTek wifi card in this laptop. It works fine most of the time but **does glitch sometimes in both Linux and Windows | 
| Suspend/sleep | :heavy_check_mark: | - If you face random logouts after waking up from suspend, follow [this](https://github.com/realKarthikNair/16-xf0xxx-linux-troubleshooting/blob/main/fix_suspend.md) <br><br> - Suspend doesn't work if sleep state is set to S3 (deep) | 
| Hibernation |  | - Couldn't figure out a way to make it work on Pop!_OS/Ubuntu <br><br> - ~Works on Fedora with some workarounds~ |
