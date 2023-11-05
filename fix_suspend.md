1. Unmount and remount /boot/efi as rw

  ```bash
  sudo umount $(mount | awk '$3 == "/boot/efi" {print $1}')
  sudo mount -o rw /boot/efi
  ```

2. Uninstall Nvidia drivers

  ```bash
  sudo apt purge ~nnvidia
  sudo apt autoremove
  sudo apt clean
  ```

3. Reinstall Nvidia drivers

  ```bash
  sudo apt update
  sudo apt full-upgrade
  sudo apt install system76-driver-nvidia
  ```
4. If your system crashes while doing step 3 or 4, execute the below after a force reboot (hold the power button) and repeat from step 1

  ```bash
  sudo dpkg --configure -a
  ```
