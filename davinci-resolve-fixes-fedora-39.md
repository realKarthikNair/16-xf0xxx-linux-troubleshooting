Assuming you already have the latest NVIDIA drivers and CUDA installed (you can follow the drivers and cuda part from [here](https://github.com/realKarthikNair/16-xf0xxx-linux-troubleshooting/blob/main/fedora39-tensorflow-gpu.md) if you haven't),

```bash
sudo dnf install libxcrypt-compat
cd /opt/resolve/libs/
mkdir disabled && mv libglib* libgio* libgmodule* disabled
```
