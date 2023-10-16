Making linux related notes and troubelshooting for my new HP Omen 16 R7 7840HS RTX 4060 (16-xf0xxx) 

# What works and what doesn't

**Based on Pop!_OS 22.04**

| Component | Works? | Notes |
| --------- | ------ | ----- |
| Display | :heavy_check_mark: |  - The latest kernel as of writing this is 6.5.7 and it only supports 165Hz and 60Hz. For more options [60, 90, 120, 144, 165]Hz you need to use the 6.4.6-76060406-generic kernel. No one including me have no idea about this regression. <br> - HDR doesn't work since Linux doesn't support HDR yet. <br> - Displays colors by default are good enough. For even better colors repro, use Adobe RGB color profile. | 