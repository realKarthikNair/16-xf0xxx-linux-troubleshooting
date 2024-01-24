```bash
sudo grubby --args="amdgpu.sg_display=0" --update-kernel=ALL
```
(tested on Fedora 39)

https://gitlab.freedesktop.org/drm/amd/-/issues/2354  
https://patchwork.freedesktop.org/patch/519023/  
https://www.phoronix.com/news/AMD-Scatter-Gather-Re-Enabled
