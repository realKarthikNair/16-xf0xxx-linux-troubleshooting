```
sudo dnf config-manager --add-repo=https://negativo17.org/repos/fedora-nvidia.repo
sudo dnf upgrade
sudo dnf remove *nvidia*
sudo yum -y install nvidia-driver nvidia-driver-cuda cuda-devel
sudo dnf install xorg-x11-drv-nvidia-cuda
sudo dnf install xorg-x11-drv-nvidia-cuda-libs
sudo dnf install cuda-cudnn.x86_64 cuda-cudnn-devel.x86_64
# cd your python project path
virtualenv -p `which python3.10` .venv # as of writing this tf isnt supported on python3.12 on linux
source .venv/bin/activate
pip install tensorflow
sudo dnf install mlocate
cp $(locate libdevice.10.bc) .
```
