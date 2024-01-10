gratitude for providing an easy to use cuda and cudnn installation : https://negativo17.org/nvidia-driver/

1. Add negativo17/fedora.nvidia and rpmfusion-nonfree-release repos

```bash
sudo dnf config-manager --add-repo=https://negativo17.org/repos/fedora-nvidia.repo
sudo dnf install \
  https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
sudo dnf upgrade
```

2. Remove any existing nvidia thing you have (knowing what you're doing before running this command is a bonus)

```bash
sudo dnf remove *nvidia*
```
3. Install nvidia-driver from rpm-fusion-nonfree
> We are not using negativo17/fedora-nvidia for this since there is a glitch with nvidia-driver on negativo17/nvidia-driver since Jan 2024 on Wayland which makes mouse unusable so we are installing nvidia-driver from rpmfusion-nonfree until its fixed (hopefully)

```bash
sudo dnf install nvidia-driver --disablerepo=fedora-nvidia --enablerepo=rpmfusion-nonfree
```

4. Install cuda drivers and cuda development packages and remove xorg-x11-drv-nvidia-cuda and xorg-x11-drv-nvidia-cuda-libs from rpmfusion-nonfree

```bash
sudo dnf remove xorg-x11-drv-nvidia-cuda
sudo dnf remove xorg-x11-drv-nvidia-cuda-libs
sudo dnf install nvidia-driver-cuda
sudo dnf install cuda-devel
sudo dnf remove xorg-x11-drv-nvidia-cuda
sudo dnf remove xorg-x11-drv-nvidia-cuda-libs
```

5. Install cudnn and cudnn development packages

```bash
sudo dnf install cuda-cudnn.x86_64 cuda-cudnn-devel.x86_64
```

6. If you are on the latest version of Fedora (I am on 39 as of writing this), the default version of Python would be the latest version which won't support tensorflow. So install an older version.

```bash
sudo dnf install python310 
python3.10 -m ensurepip
python3.10 -m pip install tensorrt #tensorrt doesnt exactly work on fedora 39 on latest nvidia drivers even with nvidia's official tensorrt package on their website but its good to have this module (i mean i couldnt make it work atleast)
```

7. ```cd``` to your python project path

```bash
virtualenv -p `which python3.10` .venv 
source .venv/bin/activate
pip uninstall tensorflow[and-cuda]
sudo dnf install mlocate
sudo updatedb
cp $(locate libdevice.10.bc) .
```

Congratulations! You can now use tensorflow with CUDA on Fedora 39! 

Footnotes: 

1. Sometimes Nvidia UVM bugs out so just remove the module right before using anything that uses CUDA or cuDNN.
The kernel will reload it automatically when you run a program that requires it. Sometimes it still fails for no reason. In that case just spam the command a few times on the terminal (I don't know how but it works)
   
```bash
sudo modprobe -r nvidia_uvm #you might need this sometimes to reload
```

2. If you are recieving errors such as `2024-01-10 23:40:45.421281: E external/local_xla/xla/stream_executor/cuda/cuda_dnn.cc:9261] Unable to register cuDNN factory: Attempting to register factory for plugin cuDNN when one has already been registered`, install `tf-nightly[and-cuda]`

```bash
# Assuming you are on a virtual environment
pip uninstall tensorflow[and-cuda]
pip install tf-nightly[and-cuda]
```

3. If you are recieving warnings like ` successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero. See more at https://github.com/torvalds/linux/blob/v6.0/Documentation/ABI/testing/sysfs-bus-pci#L344-L355`, this is caused by a bug that resets `numa_node` to -1 after reboots.

Fix 1 (temporary, needs to be run manually after every reboot, recommended if you are new to linux) 

1. Identify the PCI-ID of your GPU
2. Set 0 to `/sys/bus/pci/devices/<PCI_ID>/numa_node  
  
  For example
  ```bash
  karthik@fedora:~$ lspci -D | grep NVIDIA
  0000:01:00.0 VGA compatible controller: NVIDIA Corporation AD107M [GeForce RTX 4060 Max-Q / Mobile] (rev a1)
  0000:01:00.1 Audio device: NVIDIA Corporation Device 22be (rev a1)
  karthik@fedora:~$ sudo su
  [sudo] password for karthik: 
  root@fedora:/home/karthik# echo 0 | tee -a "/sys/bus/pci/devices/0000:01:00.0/numa_node"
  0
  ```

Fix 2 (same as Fix 1 but permanent) [credit](https://stackoverflow.com/a/70225257)

  ```bash
  # 1) Identify the PCI-ID (with domain) of your GPU
  #    For example: PCI_ID="0000.81:00.0"
  lspci -D | grep NVIDIA
  # 2) Add a crontab for root
  sudo crontab -e
  #    Add the following line
  @reboot (echo 0 | tee -a "/sys/bus/pci/devices/<PCI_ID>/numa_node")
  ```

4. TODO: figure out how to make tensorrt work
