# Improvements

1. Disable Compositor

   ```
   xfwm4-tweaks-settings
   ```

   Window Manager Tweak > Compositor > Disable

2. 4k resolution with 60hz

   ```
   xrandr --output HDMI-1 --mode 3840x2160 --rate 60
   ```

3. Increase DPI

   ```
   xfce4-appearance-settings
   ```

   Appearance > Fonts > DPI = 133

4. Install Chromium

   ```
   sudo pacman -Syu chromium
   ```

   Chromium > Settings > Appearance > Page zoom = 110%

5. Screenlock Fix - Install screensaver
   ```
   sudo pacman -Syu xfce4-screensaver
   reboot
   ```
