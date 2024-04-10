# Setting Screen Resolution and Rotation on Ubuntu Server for Raspberry Pi

## Introduction
In this tutorial, we will guide you through the process of configuring screen resolution and rotation on Ubuntu Server for Raspberry Pi. We will use the `xrandr` command to set the resolution and create a custom configuration file to adjust the screen rotation.

**Note:** Before proceeding, ensure that you have already installed the XFCE GUI on your Ubuntu Server.

## Step 1: Check Available Resolutions
1. Open a terminal window on your Raspberry Pi.
2. Run the following command to check the available output names and resolutions:
   ```bash
   xrandr
   ```
   Note down the output name and desired resolution for your display.
   
## Step 2: Set Screen Resolution
1. Execute the following command to set the desired resolution:
   ```bash
   xrandr --output <output_name> --mode <resolution>
   ```
   Replace <output_name> with the name of your output and <resolution> with the desired resolution.
   
   **For example:**
   ```bash
   xrandr --output HDMI-1 --mode 1080x1920
   ```
## Step 3: Configure Screen Rotation
1. Create a custom configuration file in the /etc/X11/ directory:
    ```bash
    sudo nano /etc/X11/xorg.conf
    ```
2. Add the following lines to the file to configure screen rotation:
   ```bash
    Section "Device"
        Identifier "Allwinner A10/A13 FBDEV"
        Driver "fbturbo"
        Option "fbdev" "/dev/fb1"
        Option "Rotate" "CW"  # or "CCW" for counter-clockwise rotation
    EndSection
    
    Section "Monitor"
        Identifier "Monitor0"
    EndSection
    
    Section "Screen"
        Identifier "Screen0"
        Device "Allwinner A10/A13 FBDEV"
        Monitor "Monitor0"
        DefaultDepth 24
        SubSection "Display"
            Depth 24
            Modes "1080x1920"  # Adjust resolution here
        EndSubSection
    EndSection

    ```
   **Adjust the resolution in the `Modes` line as needed.**

## Step 4: Apply Changes
1. Save the changes and exit the text editor.
2. Reboot your Raspberry Pi to apply the changes:
   ```bash
   sudo reboot
   ```
   
## Step 5: Check and Adjust Resolution (if needed)
After rebooting, if the screen rotation is correct but the resolution is not as expected, run the following command to adjust the resolution:

  ```bash
  xrandr --output default --mode 1080x1920
  ```

  Or Execute the following command by setting the desired resolution:
  
   ```bash
   xrandr --output <output_name> --mode <resolution>
   ```


## Conclusion
Congratulations! You have successfully configured the screen resolution and rotation on Ubuntu Server for Raspberry Pi. You can now enjoy your preferred display settings.

   

   
