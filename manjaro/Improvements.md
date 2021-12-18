# Improvements

1. Disable Compositor

   ```
   xfwm4-tweaks-settings
   ```

   Window Manager Tweak > Compositor > Disable

2. 4k resolution with 60hz

   Add following line to /boot/config.txt
   ```
   hdmi_enable_4kp60=1
   ```

   Reboot and then open display settings
   ```
   xfce4-display-settings
   ```

   Change Refresh rate to 60.0 hz

3. Increase DPI

   ```
   xfce4-appearance-settings
   ```

   Appearance > Fonts > DPI = 125

4. Install Chromium

   ```
   sudo pacman -Sy chromium
   ```

   Chromium > Settings > Appearance > Page zoom = 110%

5. Screenlock Fix - Install screensaver
   ```
   sudo pacman -Sy xfce4-screensaver
   reboot
   ```
