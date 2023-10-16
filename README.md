Making linux related notes and troubelshooting for my new HP Omen 16 R7 7840HS RTX 4060 (16-xf0xxx) 

# What works and what doesn't

**Based on Pop!_OS 22.04**

| Component | Works? | Notes |
| --------- | ------ | ----- |
| Display | :heavy_check_mark: |  - The latest kernel as of writing this is 6.5.7 and it only supports 165Hz and 60Hz. For more options [60, 90, 120, 144, 165]Hz you need to use the 6.4.6-76060406-generic kernel. No one including me have no idea about this regression. Kernels older than 6.4.6-76060406-generic also gives only 165Hz and 60Hz <br><br> - HDR doesn't work since Linux doesn't support HDR yet. <br><br> - Displays colors by default are good enough. For even better color repro, use Adobe RGB color profile. | 
| Keyboard | :heavy_check_mark: | - You can't control the RGB settings of keyboard on this model from Linux yet. [hp-omen-linux-module](https://github.com/pelrun/hp-omen-linux-module) doesn't work either. However, if you're on dual boot, RGB settings changed from Windows will persist on Linux. <br><br> - You can't control the brightness of the keyboard from Linux either <br><br> - Surprisingly, the calculator key does launch the calculator app on Gnome | 
| CPU | :heavy_check_mark: <br><br> (Do read the notes on this one too) |  - AMD-pstate works from kernel 6.5.x <br><br> - **The CPU frequency never peaks above 4.1GHz** but that's something HP has messed up on a firmware level since it can be reproduced in Windows too. **The CPU is capable of going upto 5.1GHz.** That said, performance is on par with other laptops with the same CPU so I didn't bother. | 
| GPU (RTX 4060) | :heavy_check_mark: | - Seems to be fine but I don't game so I can't comment much now | 
| Battery | :heavy_check_mark: |  - Battery life varies from 2-8 hours depending on the workload. <br><br> - The battery life is similar, if not better than Windows <br><br> - Battery charges upto 84.66 Wh while the design capacity is 83.Wh. On Windows, the capacity is 81.0 Wh. | 
| Speaker |  |  - Speaker is buggy. But whenenevr it works, it sounds good. I will update this section later. |
| Headphone jack |  | - Headphone jack is buggy. I will update this section later. |
| Microphone | :heavy_check_mark: |  - Microphone works as expected. |
| Webcam | :heavy_check_mark: |  - Webcam works as expected. |