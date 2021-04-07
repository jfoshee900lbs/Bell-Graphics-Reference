# Tech Guidelines

## Table of Contents

- [Tech Guidelines](#tech-guidelines)
  - [Table of Contents](#table-of-contents)
  - [1. Introduction](#1-introduction)
    - [1.1. TeamViewer](#11-teamviewer)
      - [1.1.1. Installation](#111-installation)
      - [1.1.2. Settings](#112-settings)
      - [1.1.3. Headless PCs and TeamViewer](#113-headless-pcs-and-teamviewer)
    - [1.2. Important PC Optimizations](#12-important-pc-optimizations)
      - [1.2.1. General Windows Settings](#121-general-windows-settings)
      - [1.2.2. Initial Windows Updates](#122-initial-windows-updates)
      - [1.2.3. Graphics Processing Unit](#123-graphics-processing-unit)
    - [1.3. Nvidia Control Panel](#13-nvidia-control-panel)
        - [1.3.1. Nvidia Geforce Experience](#131-nvidia-geforce-experience)
        - [1.3.2. Nvidia Surround and Spanning Displays Information](#132-nvidia-surround-and-spanning-displays-information)
          - [1.3.2.1 Disabling Secondary GPU](#1321-disabling-secondary-gpu)
        - [1.3.3. Nvidia Surround Setup](#133-nvidia-surround-setup)
          - [1.3.3.1 Proper Resolution and Refresh Rate for the Surround Display](#1331-proper-resolution-and-refresh-rate-for-the-surround-display)
          - [1.3.3.2 Adding Secondary Displays](#1332-adding-secondary-displays)
        - [1.3.4. Audio Setup](#134-audio-setup)
          - [1.3.4.1 Multi-channel Audio and Exclusive Mode](#1341-multi-channel-audio-and-exclusive-mode)

## 1. Introduction

### 1.1. TeamViewer

Most every computer that ends up installed on site for our clients are assigned to the company's TeamViewer account for remote access for maintenance, updates, and troubleshooting. There are certainly exceptions to this rule but wherever possible, any outgoing hardware should be remote access capable for 900lbs.

#### 1.1.1. Installation

Head to [the TeamViewer website](https://www.teamviewer.com/en-us/download/windows) and download the latest version on the client PC. Install the application as normal and make sure to select "for organizational use" when the installer asks.

![teamviewer website](assets/images/tech-guidelines/1.1.1_teamviewer_website.png)

#### 1.1.2. Settings

Open the TeamViewer application. On the main screen make sure to check the box for `Start TeamViewer with Windows` and `Grant Easy Access`. Once the box is checked for easy access a dialog will appear for login. The email used for all PCs, including both installation PCs for clients as well as internal PCs for users/company use, is `admin@900lbs.com`. Get in contact with either the Lead Developer or the Technical Manager for the password.

![teamviewer easy access needed](assets/images/tech-guidelines/1.1.2_teamviewer_easy_access_needed.png)

After the password has been accepted TeamViewer requires approval of the new device via email. At this point, either the Lead Developer or the Technical Manager will approve the new device. Login again on TeamViewer for easy access to be granted. 

![teamviewer second sign in](assets/images/tech-guidelines/1.1.2_second_sign_in.png)

After the second sign in the dialog will read `Easy access for 900lbs Admin is granted`

![teamviewer easy access granted](assets/images/tech-guidelines/1.1.2_teamviewer_easy_access_granted.png)

Next, at the top of the TeamViewer window click `Extras` then `Options`

![extras options](assets/images/tech-guidelines/1.1.2_extras_options.png)

In the `General` tab give the device a proper name that clearly identifies the client, and installation in the display name. Examples of this can be `VC-Spare`, `Bell - D.C.`, `Bell - MTC`, etc. 

![teamviewer naming](assets/images/tech-guidelines/1.1.2_teamviewer_naming.png)

Next, go to the `Security` tab, and under `Random password (for spontaneous access)`, set the `Password strength` to `Disabled (no random password)`. Change `Windows logon` to `Allowed for all users`

![teamviewer security](assets/images/tech-guidelines/1.1.2_security.png)

Next, in the `Advanced` tab, scroll down to `Personal password` and set both fields to `live2create`.  Scroll further and set `Lock remote computer` to `Never`.

![teamviewer advanced](assets/images/tech-guidelines/1.1.2_advanced.png)

Get with the Lead Developer or the Technical Manager to go into the backend of our TeamViewer account to assign the same PC name and password. They must as well sort the new computer into a proper client group, and make sure the needed user accounts have proper access to that client group. This is all handled in the Admin TeamViewer Management Console and will not be explained here.

Make sure to test remote connection capability from another machine before deploying the computer to any installation.

#### 1.1.3. Headless PCs and TeamViewer

While generally very rare, there are some calls for a headless PC to be installed at various sites. In this instance a headless PC is any PC that is not actively connected to any display. Examples include the NUC in our office that runs the wiki, and another NUC in Allentown for Mack Truck. They may be used for an easy access point to maintain other systems on the same network but special considerations must be made for this. TeamViewer as an application works by capturing the output from the GPU of a PC and streaming it over the network to a user. If a PC does not have anything outputting from the GPU when remoted into, a black screen will be displayed. This can be worked around by going to the top bar in the TeamViewer window, selecting `View` and toggle `Hide Wallpaper` on and off a couple times. Generally this will allow viewing the Windows desktop, but in a very limited capacity. The resolution will be very low, without allowing adjustments, and things like `Windows Settings` panes will not properly scroll in this headless state.

![hide wallpaper](assets/images/tech-guidelines/1.1.3_view_hide_wallpaper.png)

The true fix for this is to not ship out a completely headless PC. We can fake a display with cheap "HDMI Dummy Plugs" from Amazon. These are cheap circuit devices that essentially feed EDID values to the GPU, tricking it into believing there is a display attached. With this fake display attached, full functionality of the device will be available, and no tricks will be needed to operate the device.

![hdmi dummy](assets/images/tech-guidelines/1.1.2_hdmi_dummy.png)

### 1.2. Important PC Optimizations

#### 1.2.1. General Windows Settings

For most installations on a new PC we assume turning on and off the machine will be handled manually by the user. For this, we want to open the Windows settings and head to `System`, then `Power & Sleep`. Unless otherwise noted for a particular install, set both `Screen` and `Sleep` to `Never`.

![power sleep](assets/images/tech-guidelines/1.2.1_power_sleep.png)

Next head to the `Display` tab on the left. Scroll down to `Graphics Settings` and make sure `Hardware-accelerated GPU scheduling` is set to `On`. This setting will require the PC to be rebooted to enable.

![graphics settings](assets/images/tech-guidelines/1.2.1_graphic_settings.png)

![gpu scheduling](assets/images/tech-guidelines/1.2.1_gpu_scheduling.png)

#### 1.2.2. Initial Windows Updates

Windows updates are currently a fact of life for every PC we have deployed. If setting up a new PC to be deployed, make sure Windows Update has been ran a few times after a couple of restarts to get as much as possible installed on the system before it is sent out for deployment.

![windows update](assets/images/tech-guidelines/1.2.2_windows_update.png)

Another key thing to make sure system operation is stable, is to download manufacturer drivers for different aspects of the systems that have tangible uses for the deployed computer. For example, the motherboard could have a bios update, tuned network or wireless communication drivers, etc, that all have a benefit on the computer. However something like Asus's `Armory Crate`, an application that provides an easy UI for overclocking the system, is almost never needed on a deployed PC. Use best judgement on what drivers should be installed per system.

#### 1.2.3. Graphics Processing Unit

Windows update usually will automatically install some version of GPU drivers to the system to at least get the GPU functioning mostly as intended, but do not stop there. Head over to [Nvidia's Website](https://www.nvidia.com/Download/index.aspx) and search for the Graphics card that the drivers are needed for. Always choose the 64 bit install, as well as the WHQL version if available. If the WHQL version is selected, make sure the WHQL setting in the bios is set to `Enabled`. Upon installation of the driver and a reboot of the PC, `Nvidia Control Panel` should be accessible via a right click of the desktop. As well, `Nvidia Geforce Experience` should also be installed.

![graphics processing unit 1](assets/images/tech-guidelines/1.2.3_graphics_processing_unit.png)

![graphics processing unit 2](assets/images/tech-guidelines/1.2.3_graphics_processing_unit_2.png)

![graphics processing unit 4](assets/images/tech-guidelines/1.2.3_graphics_processing_unit_4.png)

![graphics processing unit 5](assets/images/tech-guidelines/1.2.3_graphics_processing_unit_5.png)

![graphics processing unit 6](assets/images/tech-guidelines/1.2.3_graphics_processing_unit_6.png)

![graphics processing unit 7](assets/images/tech-guidelines/1.2.3_graphics_processing_unit_7.png)

![graphics processing unit 8](assets/images/tech-guidelines/1.2.3_graphics_processing_unit_8.png)

![graphics processing unit 3](assets/images/tech-guidelines/1.2.3_graphics_processing_unit_3.png)

### 1.3. Nvidia Control Panel

Right click the desktop and click `Nvidia Control Panel`. Click the `Manage 3D settings` tab on the left. In the `Global Settings` tab scroll down to `Power Management Mode` and change the value from `Optimal Power` to `Prefer Maximum Performance`. This setting will need to be changed after every GPU driver upgrade.

![nvidia control panel power mode](assets/images/tech-guidelines/1.2.4_nvidia_control_panel_power_mode.png)

##### 1.3.1. Nvidia Geforce Experience

Open the `Nvidia Geforce Experience` app. A login prompt will be displayed. Sign in via the email text fields, and not the Google connected account button. Login is `Admin@900lbs.com`. Password is `Live2Create!`. 

![geforce experience login](assets/images/tech-guidelines/1.2.4.1_geforce_experience_login.png)

Once logged in, click the `Drivers` tab Check for updates and download the latest official driver. Once it downloads, choose `Express Installation`. Reboot the PC after installing the latest GPU drivers.

![geforce_experience_check_driver_2](assets/images/tech-guidelines/1.2.4.1_geforce_experience_check_driver_2.png)

![geforce_experience_check_driver](assets/images/tech-guidelines/1.2.4.1_geforce_experience_check_driver.png)

##### 1.3.2. Nvidia Surround and Spanning Displays Information

A lot of the PC installations we have created use Nvidia Spanning capabilities to treat two displays as a single display. This is a software controlled function that takes place within the Nvidia Control Panel, but before we get to spanning displays there are some considerations that must be addressed.

The displays that are being spanned must both be connected to the same graphics card when used on a multi-gpu setup. Additional secondary displays that are not spanned should be plugged in to the secondary graphics card. There are a lot of finicky things that can cause issues as well that cannot all possibly be covered in detail. Both displays being spanned should be connected to the same connection type on the same GPU. Adapters can be utilized to convert a signal from the display to the GPU's ports, but the spanned displays must be connected to the same type of port on the same GPU. Active displayport to HDMI adapters can be used to convert two displayport sockets, to two HDMI sockets.

![active_displayport_adapter](assets/images/tech-guidelines/1.3.2_active_displayport_adapter.png)

Do NOT use an SLI bridge. We have found over time that small changes have been made to SLI support, rendering pre-existing installs impossible to create if an SLI bridge is utilized. An SLI bridge combines the cards to make the Windows OS see it functionally as a single card and a single card that is using display spanning is only allowed to have a single additional display attached to it, even with six or more free ports across both installed cards.

For an example install with an Ideum table, two 4K screens, and 3 1080p secondary screens, both table displays are plugged into the top card to be spanned and after spanning is accomplished, the rest of the displays are plugged in to the bottom card.

###### 1.3.2.1 Disabling Secondary GPU

There are small annoyances that can pop up as well when spanning displays. For example, Nvidia's software will not allow for spanning displays properly when two cards are detected and no SLI bridge installed. Again, don't install a SLI bridge.

![sli_unsupported](assets/images/tech-guidelines/1.2.4.2_sli_unsupported.png)

To get around this limitation to start spanning without disassembling the PC, head to the Windows `Device Manager` and click `Display Adapters`. Right click one and hit disable. As a warning, there is a 50/50 chance the second card meant for the secondary displays will be disabled.

![disable_gpu](assets/images/tech-guidelines/1.3.2_disable_gpu.png)

If one card was disabled and the screens go black and do not come back, the wrong card was disabled. To fix this, move a primary display cable from the top card, to the bottom card. Enable the disabled graphics card, disable the other one, and move the primary display cable back to the primary graphics card.

Now, only one graphics card should be enabled with the desired spanning displays plugged into it.

![surround](assets/images/tech-guidelines/1.3.3_3.jpg)

Now, displays should be spannable.

##### 1.3.3. Nvidia Surround Setup

The first thing to note is there are some apps that will not allow the required spanning tasks to be performed if they are open. This includes TeamViewer, so currently as it stands, we cannot remotely configure a surround setup on any installation PC. These steps can be used as a guide to talk through anyone on site to reduce team member travel.

Right click the desktop and click `Nvidia Control Panel`. Head to `Configure Surround, PhysX`. Check the box for `Span Displays with Surround` then click `Configure...` 

![surround1](assets/images/tech-guidelines/1.3.3_1.png)

A big bold number should appear on the active displays. These numbers correspond to the topology of the displays. If they are not, check the box next to the desired displays in the `Displays` window. Next, drag the windows in the preview pane to match the correct topology to the numbers that are displaying on the screen. Do not worry about changing the resolution or refresh rate that the dropdown in the middle depicts yet.  We have not used any bezel correction on any installations at the time of writing this. Click `Enable Surround`.

![surround2](assets/images/tech-guidelines/1.3.3_2.png)

It's at this point the screens will flash, lose signal, sync back together, and repeat that process. The Nvidia Control Panel windows will become unresponsive. It appears to take between 30 seconds to a minute for everything to sync up. Once the Nvidia Control Panel window is responsive again surround spanning is complete. Do not change the resolution or refresh rate in this window.

###### 1.3.3.1 Proper Resolution and Refresh Rate for the Surround Display

Right click the desktop and click `Display settings`. At this point the only options available are for a single display. The two displays are acting as one. Windows can no longer change their settings independently. Use this window to make sure the resolution is correct. Generally two 1080p displays are 3840x1080, and two 4K displays are 7680x2160. 

![surround4](assets/images/tech-guidelines/1.3.3_4.png)

Next scroll down to `Advanced display settings` and ensure the proper refresh rate is being output. 

![surround5](assets/images/tech-guidelines/1.3.3_5.png)
![surround6](assets/images/tech-guidelines/1.3.3_6.png)
![surround7](assets/images/tech-guidelines/1.3.3_7.png)


Something to watch out for is making sure 4K displays are reporting at `60hz` and not `30hz`. 4K30hz is a limitation of older HDMI specification and may need to be changed to Displayport connections to get the higher bandwidth.

###### 1.3.3.2 Adding Secondary Displays

At this point plug in the secondary displays / re-enable the secondary graphics card again in `Device Manager`. 

![surround8](assets/images/tech-guidelines/1.3.3_8.jpg)
![surround9](assets/images/tech-guidelines/1.3.3_9.png)

The secondary displays should pop up but if not, right click the desktop and click `Nvidia Control Panel` then click `Set Up Multiple Displays` in the left pane. Make sure all of the desired displays have their checkboxes enabled. At this point, either go back to the Windows `Display Settings` or click `Change Resolution` in the left pane of the Nvidia Control Panel. Set the secondary displays to the desired resolution and refresh rate as we did for the primary display. One thing to look out for is some displays may default to a different aspect ratio, such as 1920x1200 or 4096x2160. Make sure the correct target resolution expected for the build is used.
Also, use this time to arrange the displays in order for the build. The order may need to be further tweaked after checking the build, but this is the area to change them.

![surround10](assets/images/tech-guidelines/1.3.3_10.png)
![surround11](assets/images/tech-guidelines/1.3.3_11.png)

##### 1.3.4. Audio Setup

Next, we look at the sound output to make sure it is properly set. Right click the sound icon in the taskbar and click `Open Sound settings`.

![sound_icon](assets/images/tech-guidelines/1.3.3_sound_icon.png)
![surround12](assets/images/tech-guidelines/1.3.3_12.png)

Next, in the right side of the settings pane click `Sound Control Panel`.

![surround13](assets/images/tech-guidelines/1.3.3_13.png)

The output device is different on every installation and will require some testing to ensure we are outputting to the proper device. Here in this window right click each device and hit `Test` to hear where the audio is coming from. Use process of elimination to `Disable` the devices that should not be outputting audio to leave only the proper output device accessible.

![surround14](assets/images/tech-guidelines/1.3.3_14.png)

##### 1.3.4.1 Multi-channel Audio and Exclusive Mode

Once we have the proper sound device identified, right click it and choose `Properties`

![surround15](assets/images/tech-guidelines/1.3.3_15.png)

Head to `Advanced` and make sure the audio output matches the speaker installation required. For this example we are using optical audio over a Toslink cable. 

![surround16](assets/images/tech-guidelines/1.3.3_16.png)

As well, in the `Advanced` tab make sure to uncheck both boxes for `Exclusive Mode`

![surround17](assets/images/tech-guidelines/1.3.3_17.png)

If 5.1 is not listed here close the `Properties` window, right click the audio device, and choose `Configure Speakers`. This screen will also allow to test each channel individually to ensure all systems are functioning as intended. Shown below is only reporting Stereo but if 5.1 is supported, it will allow selection here.

![configure_speakers_2](assets/images/tech-guidelines/1.3.3_configure_speakers_2.png)
![configure_speakers](assets/images/tech-guidelines/1.3.3_configure_speakers.png)