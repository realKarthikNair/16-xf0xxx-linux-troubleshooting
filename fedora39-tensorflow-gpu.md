gratitude for providing an easy to use cuda and cudnn installation : https://negativo17.org/nvidia-driver/

```
sudo dnf config-manager --add-repo=https://negativo17.org/repos/fedora-nvidia.repo
sudo dnf install \
  https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
sudo dnf upgrade
sudo dnf remove *nvidia*
sudo dnf install nvidia-driver --disablerepo=fedora-nvidia --enablerepo=rpmfusion-nonfree #there is a glitch with nvidia-driver on negativo17/nvidia-driver since Jan 2024 on Wayland which makes mouse unusable so we are installing nvidia-driver from rpmfusion-nonfree until its fixed (hopefully) 
sudo dnf install nvidia-driver-cuda
sudo dnf install cuda-devel
sudo dnf remove xorg-x11-drv-nvidia-cuda
sudo dnf remove xorg-x11-drv-nvidia-cuda-libs
sudo dnf install cuda-cudnn.x86_64 cuda-cudnn-devel.x86_64
sudo dnf install python310 # as of writing this tf isnt supported on python3.12 on linux
python3.10 -m ensurepip
python3.10 -m pip install tensorrt #tensorrt doesnt exactly work on fedora 39 on latest nvidia drivers even with nvidia's official tensorrt package on their website but its good to have this module (i mean i couldnt make it work atleast)
# cd your python project path
virtualenv -p `which python3.10` .venv 
source .venv/bin/activate
pip install tensorflow
sudo dnf install mlocate
sudo updatedb
cp $(locate libdevice.10.bc) .
```

```bash
sudo modprobe -r nvidia_uvm #you might need this sometimes to reload
```

TODO: figure out how to make tensorrt work
