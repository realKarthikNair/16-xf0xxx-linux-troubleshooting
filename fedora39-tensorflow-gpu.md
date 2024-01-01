gratitude for drivers : https://negativo17.org/nvidia-driver/

```
sudo dnf config-manager --add-repo=https://negativo17.org/repos/fedora-nvidia.repo
sudo dnf upgrade
sudo dnf remove *nvidia*
sudo yum -y install nvidia-driver nvidia-driver-cuda cuda-devel
sudo dnf install xorg-x11-drv-nvidia-cuda
sudo dnf install xorg-x11-drv-nvidia-cuda-libs
sudo dnf install cuda-cudnn.x86_64 cuda-cudnn-devel.x86_64
sudo dnf install python310 # as of writing this tf isnt supported on python3.12 on linux
python3.10 -m ensurepip
python3.10 -m pip install tensorrt
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
