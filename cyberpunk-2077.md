#### Here is how you can run Cyberpunk 2077 on this laptop on Linux (Pop!_OS 22.02)

*I expect the reader to have basic familiarity using [Bottles](https://usebottles.com/)*

1. Get Bottles from Pop!_Shop or simply enter this on the terminal
   ```bash
   flatpak install flathub com.usebottles.bottles
   ```

2. Get the necessary game files (how you manage to get them is upto you).
3. Grant necessary permissions for Bottles
   
     a. install Flatseal
   
       flatpak install flathub com.github.tchx84.Flatseal
   
   
     b. 

      ![image](https://github.com/realKarthikNair/16-xf0xxx-linux-troubleshooting/assets/78267371/7ae40446-5f41-4c03-bb8d-199a9e1f344f)
      ![image](https://github.com/realKarthikNair/16-xf0xxx-linux-troubleshooting/assets/78267371/21188944-2cb5-4fcb-83a5-da5c57d5c99e)

      Replace the username in the path in below screenshot with your username

      ![image](https://github.com/realKarthikNair/16-xf0xxx-linux-troubleshooting/assets/78267371/43d942c9-4de7-4f0d-9fbb-5300ba9cd933)
      ![image](https://github.com/realKarthikNair/16-xf0xxx-linux-troubleshooting/assets/78267371/0d25efaa-55da-4b0b-82a7-12e0aa8068f5)

4. Run this on Terminal

```bash
flatpak override com.usebottles.bottles --user --filesystem=xdg-data/applications
```

5. This dependency is required for Cyberpunk 2077

   ![image](https://github.com/realKarthikNair/16-xf0xxx-linux-troubleshooting/assets/78267371/bd4a4c88-b14f-4013-b8c8-f2a5debb10c6)

   Install vkBasalt for Post Processing effects

   ```bash
   flatpak install org.freedesktop.Platform.VulkanLayer.vkBasalt/x86_64/22.08
   ```


6. Now before launching the game, make these changes in Cyberpunk 2077 Bottles settings for good results

![image](https://github.com/realKarthikNair/16-xf0xxx-linux-troubleshooting/assets/78267371/a0ea0225-04fb-4dcd-ae97-9df5c95e1bc2)
![image](https://github.com/realKarthikNair/16-xf0xxx-linux-troubleshooting/assets/78267371/f7ab6927-e06b-49e8-a099-a3fe801c3dd9)


7. For Ray Tracing and DLSS

![image](https://github.com/realKarthikNair/16-xf0xxx-linux-troubleshooting/assets/78267371/3ddf4b15-d46e-43f4-a3b6-90c95affd76b)

8. If the keyboard is detected as a controller, follow this 

Backup the original Cyberpunk2077.exe file and then run this 

   ```bash
   echo '2C45C6: EB' | xxd -r - Cyberpunk2077.exe
   ```

9. To solve touchpad gestures crashing the session on Wayland

   ```bash
   xinput list --name-only | grep ^xwayland-pointer-gestures | xargs -n1 xinput disable
   ```
