Title: How to install ADB on Windows, macOS, and Linux

URL Source: https://www.xda-developers.com/install-adb-windows-macos-linux/

Published Time: 2021-07-28T02:30:17Z

Markdown Content:
[ADB](https://www.xda-developers.com/tag/adb/)

![Image 1: 4](https://static1.xdaimages.com/wordpress%2Fwp-content%2Fauthors%2F658e4a47c1dad-Skanda_Hazarika_Profile_Picture.jpg?fit=crop&w=90&h=90)

![Image 2: 4](https://static1.xdaimages.com/wordpress%2Fwp-content%2Fauthors%2F6351bd4de2ce7-Pic%201.jpeg?fit=crop&w=90&h=90)

Sign in to your XDA account

### Quick Links

*   [What is the Android Debug Bridge (ADB)?](https://www.xda-developers.com/install-adb-windows-macos-linux/#what-is-the-android-debug-bridge-adb)
    

*   [How to set up ADB on your phone](https://www.xda-developers.com/install-adb-windows-macos-linux/#how-to-set-up-adb-on-your-phone)
    

*   [How to set up ADB on your computer](https://www.xda-developers.com/install-adb-windows-macos-linux/#how-to-set-up-adb-on-your-computer)
    

*   [Add ADB to your Path environment variables](https://www.xda-developers.com/install-adb-windows-macos-linux/#add-adb-to-your-path-environment-variables)
    

*   [WSL, ADB over Wi-Fi, and using your browser](https://www.xda-developers.com/install-adb-windows-macos-linux/#wsl-adb-over-wi-fi-and-using-your-browser)
    

*   [What else can I do with ADB?](https://www.xda-developers.com/install-adb-windows-macos-linux/#what-else-can-i-do-with-adb)
    

Most of the [best phones](https://www.xda-developers.com/best-phones/) on the market run Android, and it's preferred by many for being a more open operating system than Apple's iOS. However, there are many things on Android that are also hidden from the average user. Thankfully, many of these capabilities can be accessed by using the Android Debug Bridge (ADB). If you're wondering how to set it up, we're here to help with that.

    [![Image 3: The Google Pixel 8 Pro in a hand open on the home screen](https://static1.xdaimages.com/wordpress/wp-content/uploads/wm/2023/10/google-pixel-8-pro-3.jpg)](https://www.xda-developers.com/5-features-android-15-wishlist/)Related

##### [These are 5 features I want Android 15 to bring, because Android updates are getting boring](https://www.xda-developers.com/5-features-android-15-wishlist/ "These are 5 features I want Android 15 to bring, because Android updates are getting boring")

Android 15 is a few months out, but there are still some features we could see, especially Pixel-exclusive features.

What is the Android Debug Bridge (ADB)?
---------------------------------------

### And how does it work?

ADB is a tool provided by Google for developers to debug and test their software on Android phones. It provides access to certain features that aren't available to regular users, and since anyone can technically use ADB, you have a way to use these advanced features even if you're not a developer.

The internal structure of ADB is based on the classic client-server architecture. There are three components that make up the entire process.

1.  The client, i.e. the PC/Mac/Chromebook you have connected to your Android device. We are sending commands to our device from the computer through the USB cable or wirelessly.
2.  A daemon (known as "adbd") that runs commands on an Android phone. The daemon runs as a background process on each device.
3.  A server that manages communication between the client and the daemon. The server runs as a background process on the computer.

Because there are three pieces that make up ADB (the client, the daemon, and the server), certain pieces need to be up and running in the first place. If you have freshly booted the computer (and you don’t have it set up to start the daemon on boot), then you will need it to be running before any communication can be sent to the target Android device.

How to set up ADB on your phone
-------------------------------

### Preparing to communicate with your computer

Setting up ADB requires some preparation on both the Android phone and the PC you want to use. For starters, follow these steps on your phone:

1.  Launch the **Settings** application on your phone.
2.  Tap the **About phone** option generally near the bottom of the list.
    
    Depending on the OEM skin, the **About phone** page may be called something else or buried somewhere else in the **Settings** app on your device.
    
3.  Then tap the **Build number** option seven times to enable Developer Mode. You will see a toast message when it is done.
4.  Now go back to the main Settings screen, and you should see a new **Developer options** menu you can access.
    
    On Google Pixel phones and some other devices, you might need to navigate to **Settings** \> **System** to find the **Developer options** menu.
    
5.  Go in there and enable the **USB debugging** option.

For now, you're done with the process on the phone. Next up, you will need to scroll below and follow the rest of the instructions for your particular operating system.

How to set up ADB on your computer
----------------------------------

### How to set up ADB on Microsoft Windows

1.  Download the [Android SDK Platform Tools ZIP file for Windows](https://dl.google.com/android/repository/platform-tools-latest-windows.zip)**.**
2.  Extract the contents of this ZIP file into an easily accessible folder (such as C:\\platform-tools).
3.  Open **File Explorer** and browse to where you extracted the contents of this ZIP file.
4.  Right-click an empty area of the File Explorer window and choose **Open in Terminal**. If you have an older version of Windows without Windows Terminal, you need to hold **Shift** on the keyboard while right-clicking, then choose **Open PowerShell window here**.
    
        ![Image 4: Screenshot of File Explorer with the option to open in Terminal highlighted](https://static1.xdaimages.com/wordpress/wp-content/uploads/wm/2024/04/file-explorer-open-in-terminal.png)
    
5.  Connect your smartphone or tablet to your computer with a USB cable. Change the USB mode to “file transfer (MTP)” mode. Some OEMs may or may not require this, but it's best to just leave it in this mode for general compatibility.
6.  In the PowerShell/Terminal window, enter the following command to launch the ADB daemon.
    
    ./adb devices
    
7.  On your phone's screen, you should see a prompt to allow or deny USB Debugging access. Tap **Allow**.
    
        ![Image 5: Allow USB debugging from a PC on a Google Pixel phone](https://static1.xdaimages.com/wordpress/wp-content/uploads/wm/2023/05/allow-usb-debugging-from-a-pc-on-a-google-pixel-phone.png)
    
8.  Finally, re-enter the command from step 6. If everything was successful, you should now see your device's serial number in the command prompt/Terminal window.
    
        ![Image 6: adb devices under Windows Terminal](https://static1.xdaimages.com/wordpress/wp-content/uploads/wm/2023/05/adb-devices-under-windows-terminal.png)
    

You can now run any ADB command on your device! As a side note, you can also isntall adb using a package manager like [winget](https://www.xda-developers.com/how-use-winget-windows-11/), which makes it easier to keep adb updated.

### How to set up ADB on macOS

1.  Download the [Android SDK Platform Tools ZIP file for macOS](https://dl.google.com/android/repository/platform-tools-latest-darwin.zip).
2.  Extract the ZIP to an easily accessible location (like the Desktop, for example).
3.  Open **Terminal**.
4.  To browse to the folder you extracted ADB into, enter the following command, where **path/to/extracted/folder** represents the folder where you extracted the ZIP file to.:
    
    cd /path/to/extracted/folder/
    
    For example, if you extracted them to your desktop, the command would look like this:
    
    cd /Users/XDA/Desktop/platform-tools/
    
5.  Connect your device to your Mac with a compatible USB cable. Change the USB connection mode to “file transfer (MTP)” mode. This is not always required for every device, but it's best to just leave it in this mode, so you don't run into any issues.
6.  Once the Terminal is in the same folder your ADB tools are in, you can execute the following command to launch the ADB daemon:
    
    ./adb devices
    
7.  On your phone, you'll see an **Allow USB debugging** prompt. Allow the connection.
    
        ![Image 7: Allow USB debugging from a PC on a Google Pixel phone](https://static1.xdaimages.com/wordpress/wp-content/uploads/wm/2023/05/allow-usb-debugging-from-a-pc-on-a-google-pixel-phone.png)
    
8.  Finally, re-enter the command from step 7. If everything was successful, you should now see your device's serial number in macOS's Terminal window.
    
        ![Image 8: adb devices under macOS Terminal](https://static1.xdaimages.com/wordpress/wp-content/uploads/wm/2023/05/adb-devices-under-macos-terminal.png)
    

Congratulations! You can now run any ADB command on your device!

While the guide above will certainly work, veteran macOS users can also opt to install ADB on their Macs using an unofficial package manager such as [Homebrew](https://formulae.brew.sh/cask/android-platform-tools) or [MacPorts](https://ports.macports.org/port/android-platform-tools/summary). That way, you don't have to manually update the binaries.

### How to set up ADB on Linux

1.  Download the [Android SDK Platform Tools ZIP file for Linux](https://dl.google.com/android/repository/platform-tools-latest-linux.zip).
2.  Extract the ZIP to an easily accessible location (like the Desktop, for example).
3.  Open a **Terminal** window.
4.  Browse to the extracted folder using the following command, replacing **path/to/extracted/folder** with the folder where you extracted the ZIP file to:
    
    cd /path/to/extracted/folder/
    
    For example:
    
    cd /home/XDA/Desktop/platform-tools/
    
5.  Connect your device to your Linux machine with your USB cable. Change the connection mode to **file transfer (MTP)** mode. This is not always necessary for every device, but it's recommended, so you don't run into any issues.
6.  Once the Terminal is in the same folder your ADB tools are in, you can execute the following command to launch the ADB daemon:
    
    ./adb devices
    
7.  Back on your Android device, you'll see a prompt asking you to allow USB debugging. Go ahead and grant it.
    
        ![Image 9: Allow USB debugging from a PC on a Google Pixel phone](https://static1.xdaimages.com/wordpress/wp-content/uploads/wm/2023/05/allow-usb-debugging-from-a-pc-on-a-google-pixel-phone.png)
    
8.  Finally, re-enter the command from step 8. If everything was successful, you should now see your device's serial number in the Terminal window output.
    
        ![Image 10: adb devices under Ubuntu Linux Terminal](https://static1.xdaimages.com/wordpress/wp-content/uploads/wm/2023/05/adb-devices-under-ubuntu-linux-terminal.png)
    

Congrats! You can now run any ADB command on your device!

Linux users should know that there is an easier way to install ADB on their computers. The guide above will certainly work for you, but those who own a mainstream Debian/Ubuntu or Fedora/SUSE-based distro of Linux can skip steps 1 and 2 of the guide above and use one of the following commands:

*   Debian/Ubuntu-based Linux users can type the following command to install ADB:
    
    sudo apt-get install android-sdk-platform-tools
    
*   Fedora/SUSE-based Linux users can type the following command to install ADB:
    
    sudo dnf install android-tools
    

However, it is always better to opt for the latest binary from the Android SDK Platform Tools release since the distro-specific packages often contain outdated builds.

Add ADB to your Path environment variables
------------------------------------------

You can use ADB just fine through the steps above, but if you're doing this frequently, adding ADB to the PATH environment variable is a huge time saver. All major operating systems have a PATH variable, and it allows you to specify the location of important programs that are also trusted by the user, so the computer can automatically access it without ahving to open the program's location first. For instance, you can type "calc" in the Run prompt of Windows to launch calculator, but not "chrome" to start Google Chrome - simply because the location of the latter isn't included in the PATH variable.

Adding ADB to the PATH environment variable allows you to run ADB by running the terminal normally, and it also makes it so you don't need to precede ADB commands with **./** . Here's how to do it.

### Windows

1.  Right-click on the **Start** button (or use the **Windows + X** keyboard shortcut) and select the **System** option. You will be greeted with a screen showing some system information.
    
        ![Image 11: Screenshot of the Quick Link menu in Windows 11 with the System option highlighted](https://static1.xdaimages.com/wordpress/wp-content/uploads/wm/2024/01/path-environment-variables-1.png)
    
2.  Select **Advanced system settings** from the **Related links** section under **Device specifications**.
    
        ![Image 12: Screenshot of the About page in the Windows 11 Settings app with the advanced system settings button highlighted](https://static1.xdaimages.com/wordpress/wp-content/uploads/wm/2024/01/path-environment-variables-2.png)
    
3.  Click on the **Environment Variables** button.
    
        ![Image 13: Screenshot of the System Properties dialog with the environment variables button highlighted](https://static1.xdaimages.com/wordpress/wp-content/uploads/wm/2024/01/path-environment-variables-3.png)
    
4.  Look for the variable named **Path** under **System variables** and double-click it.
    
        ![Image 14: Screenshot of environment variables in Windows 11 with the Path variable highlighted](https://static1.xdaimages.com/wordpress/wp-content/uploads/wm/2024/01/path-environment-variables-4.png)
    
5.  Click **New**, then **Browse** and navigate to the folder where you extracted the ADB files (e.g. C:\\platform-tools).
    
        ![Image 15: Screenshot of the environment vcariable editor with the new and browse buttons highlighted](https://static1.xdaimages.com/wordpress/wp-content/uploads/wm/2024/01/path-environment-variables-5.png)
    
6.  When you see the folder location is properly listed, click the **OK** button out of all the Windows you have opened to confirm.
7.  Sometimes, the graphical shell needs a restart to make the changes take effect. You can simply sign out and sign in again or reboot your PC to force Windows to use the updated PATH settings.

Now start a new terminal or command prompt instance and type **adb** to verify the location has been added.

In case you use a package manager like Chocolatey to install ADB, it should take care of the PATH variable editing portion as well. As a result, you can skip the above process.

### macOS

You can use the following steps to set up the PATH environment variable in macOS, but if you installed ADB using a package manager like Homebrew, this is unnecessary. Here's how it works:

1.  Note down the location where you extracted the ADB tools.
2.  Open the **Terminal app** and make sure to be in the Home directory.
    
    cd ~
    
3.  In case you're running any macOS version older than Catalina, the default shell should be Bash. For macOS Catalina and newer, the default changed to the Z shell (Zsh). Hence, you need to determine the current shell before changing the PATH variable. Type the following command and press **Enter** to see the shell your Mac is using:
    
    echo $0
    
4.  Depending on the output, create a shell configuration file. For Bash:
    
    touch .bash\_profile
    
    For Zsh:
    
    touch .zshrc
    
    People who are already using custom shell configurations can skip this step.
5.  Open the shell configuration file with **TextEdit**: For Bash:
    
    open -e .bash\_profile
    
    For Zsh:
    
    open -e .zshrc
    
    If you prefer to use nano/pico/vi or any other CLI text editor, you can instead.
6.  Adjust the location according to the first step in the following command and add it to the shell configuration file you just opened:
    
    export PATH=$PATH:/path/to/extracted/folder/
    
    For example:
    
    export PATH=$PATH:/Users/XDA/Desktop/platform-tools/
    
7.  Save the file and close the TextEdit app. Next, go back to the **Terminal app** and reload your shell settings. For Bash:
    
    source .bash\_profile
    
    For Zsh:
    
    source .zshrc
    
8.  You're done. Optionally, verify the PATH variable assertions using the following command:
    
    echo $PATH
    

To test if the process was successful, start a new Terminal instance and type **adb**. You can also install adb with Homebrew, which will automatically add it to your PATH!

### Linux

1.  Note down the location where you extracted the ADB tools.
2.  Open the **Terminal app** and make sure to be in the Home directory.
    
    cd ~
    
3.  Due to the fact that most common Linux distributions ship with Bash as their default shell, the next steps will be Bash-specific. You can, of course, consult the documentation of your preferred shell and modify the commands to suit your needs.
4.  Open the shell configuration file with a text editor:
    
    sudo nano .bashrc
    
    You can also use other editors like vi or gedit.
5.  Add the following line to the end of the .bashrc file. Remember to adjust the location according to the first step beforehand.
    
    export PATH=$PATH:/path/to/extracted/folder/
    
    For example:
    
    export PATH=$PATH:/home/xda/platform-tools/
    
    Be careful editing this file; do not add anything else or change anything else.
    
6.  Save the file. Next, go back to the **Terminal app** and reload your shell settings:
    
    source ~/.bashrc
    
7.  Optionally, verify the PATH variable assertions using the following command:
    
    echo $PATH  
    

Now you can call ADB from anywhere under Linux. To check if it's working, spawn a new Terminal window and type **adb**.

It is worth mentioning that you don't need to perform these steps if you prefer to install (and update) ADB using the distro-specific packages.

WSL, ADB over Wi-Fi, and using your browser
-------------------------------------------

### How to set up ADB on Windows Subsystem for Linux and ChromeOS

[Windows Subsystem for Linux (WSL)](https://www.xda-developers.com/how-to-install-wsl-2-windows/) offers Windows users a seamless way to run Linux apps. However, the environment has yet to offer full-fledged USB hardware access. As a consequence, ADB under WSL can't access your Android device, even if you install it using the aforementioned way. Nonetheless, there exists an official workaround, which utilizes the open-source [usbipd-win](https://github.com/dorssel/usbipd-win) project. To know more, take a look at our tutorial on [how to set up USB passthrough in WSL](https://www.xda-developers.com/wsl-connect-usb-devices-windows-11/).

For ChromeOS, you need to [turn on the built-in Linux development environment](https://www.xda-developers.com/linux-apps-chrome-os/) first. By default, it offers you a Debian instance. You can then easily set up ADB using the Linux-oriented steps mentioned earlier.

Just to cover all of our bases here, users may need to put a **./** in front of any ADB commands you use in the future, especially when they are using the extracted binaries directly from the Google-provided Platform Tools ZIP. This is something any \*nix user (or Windows user running PowerShell/Terminal) will likely know, but it's important to remember.

### How to set up ADB on your browser

The ADB protocol can be implemented using the WebUSB API in order to [control Android phones directly from web browsers](https://www.xda-developers.com/webadb-run-adb-from-web-browser/). [Tango](https://github.com/yume-chan/ya-webadb/) (formerly known as Yet Another WebADB) is one such project that allows users to perform most of the functionality provided by ADB right from the web browser without installing any binary. All you need is a web browser that supports the WebUSB API (such as Google Chrome, Microsoft Edge, or Firefox) and you are good to go. It's worth noting that some browsers, such as Vivaldi, don't properly display the popup for USB device connections, so they may not work for this.

### How to use ADB over Wi-Fi

Android 11 and higher editions natively support ADB connection over Wi-Fi. This eliminates the need to deal with common USB connection issues and additional steps, such as [Android OEM driver installation](https://www.xda-developers.com/download-android-usb-drivers/) on Windows.

In order to set up wireless debugging, do the following:

1.  Make sure that your PC/Mac and the phone are connected to the same wireless network.
2.  On your phone, go to **Developer options** under **Settings** and enable **Wireless debugging**. On the **Allow wireless debugging on this network?** popup, select **Allow**.
    
        ![Image 16: Android 11 USB debugging and wireless debugging](https://static1.xdaimages.com/wordpress/wp-content/uploads/2021/01/Android-11-USB-debugging-and-wireless-debugging.jpg)
    
3.  Tap on the **Wireless debugging** option and select **Pair device with pairing code**.[](https://www.xda-developers.com/debloat-your-phone-run-adb-shell-commands-no-root-no-pc/)
    
        ![Image 17: Android 11 wireless debugging](https://static1.xdaimages.com/wordpress/wp-content/uploads/2021/01/Android-11-wireless-debugging.jpg)
    
4.  Take note of the pairing code, IP address, and port number displayed on the phone screen.
    
        ![Image 18: Android wireless debugging pair device with pairing code](https://static1.xdaimages.com/wordpress/wp-content/uploads/2021/07/Android-wireless-debugging-pair-device-with-pairing-code.jpg)
    
5.  On your PC/Mac, run the following command:
    
            `adb pair IP_Address:Port`
        
    
    Use the IP address and port number from step 4.
6.  When prompted, enter the pairing code that you received in step 4. A message should indicate that your device has been successfully paired.
7.  Next, run the following command on the PC/Mac's terminal window:
    
            `adb connect IP_Address:Port`
        
    
    Look at the **IP address & Port** section under **Wireless debugging** in step 3 for the IP address and port.
8.  If everything goes right, then you should see a message like the following:
    
            `connected to 192.168.68.100:37173`
        
    
9.  Now you’re ready to type whatever ADB shell command you want.

Examples of ADB commands
------------------------

To check if you have successfully installed ADB, connect your device to your PC/Mac with your USB cable, and run the **adb devices** command as described above. It should display your device listed in the Command Prompt/PowerShell/Terminal window. If you get a different output, we recommend starting over with the steps.

As mentioned above, you can use ADB to do all sorts of things on an Android device. Some of these commands are built directly into the ADB binary and should work on all devices. You can also open up what is referred to as an ADB Shell that will let you run commands directly on the device. The commands which are run directly on the device can vary from device to device (since OEMs can remove access to certain ones, and also modify ADB behavior) and can vary from one version of Android to the next as well.

Below, you’ll find a list of example commands which you can do on your device:

*   Print a list of connected devices:
    
    adb devices
    
*   Kill the ADB server:
    
    adb kill-server
    
*   Install an application:
    
    adb install <path\_to\_the\_APK\_file\>
    
*   Set up port forwarding:
    
    adb forward tcp:6100 tcp:7100
    
*   Copy a file/directory from the device:
    
    adb pull <path\_to\_the\_remote\_object\> <path\_to\_the\_local\_destination\>
    
*   Copy a file/directory to the device:
    
    adb push <path\_to\_the\_local\_object\> <path\_to\_the\_remote\_destination\>
    
*   Initiate an ADB shell:
    
    adb shell
    

What else can I do with ADB?
----------------------------

Below is a list of XDA tutorials for various devices that detail many applications of ADB commands in order to modify hidden settings, customize OEM features or user interfaces, and much more!

    [![Image 19: How to Boot Into Recovery featured image showing phone placed on a table in recovery mode](https://static1.xdaimages.com/wordpress/wp-content/uploads/2021/06/How-to-Boot-Into-Recovery.jpg)](https://www.xda-developers.com/how-to-boot-to-recovery/)Related

##### [How to boot into recovery mode using button combos, ADB, and root apps](https://www.xda-developers.com/how-to-boot-to-recovery/ "How to boot into recovery mode using button combos, ADB, and root apps")

If you have an Android or iOS device and are wondering how to boot into recovery to clear cache or reset your device, this is how to do it!

    [![Image 20: Phone with ](https://static1.xdaimages.com/wordpress/wp-content/uploads/2017/07/How-to-Uninstall-Carrier_OEM-Bloatware-Without-Root-Access.jpg)](https://www.xda-developers.com/uninstall-carrier-oem-bloatware-without-root-access/)Related

##### [How to uninstall carrier/OEM bloatware without root access](https://www.xda-developers.com/uninstall-carrier-oem-bloatware-without-root-access/ "How to uninstall carrier/OEM bloatware without root access")

If you want to get rid of carrier/OEM apps from your phone, here's how you can uninstall bloatware from your device without root access!

    [![Image 21: LADB debloat your phone without root or PC](https://static1.xdaimages.com/wordpress/wp-content/uploads/2021/01/LADB-Featured-Image.jpg)](https://www.xda-developers.com/debloat-your-phone-run-adb-shell-commands-no-root-no-pc/)Related

##### [How to debloat your phone (and more) without connecting to a PC](https://www.xda-developers.com/debloat-your-phone-run-adb-shell-commands-no-root-no-pc/ "How to debloat your phone (and more) without connecting to a PC")

LADB is an app that lets you run ADB shell commands from your phone, no root and no PC needed! Use it to debloat your phone and more!

    [![Image 22: Sideload apps on Android TV](https://static1.xdaimages.com/wordpress/wp-content/uploads/2021/10/How-to-Sideload-Apps-on-Android-TV.jpg)](https://www.xda-developers.com/how-to-sideload-apps-android-tv/)Related

##### [How to sideload apps on Android TV: APK Install and ADB Sideload methods explained in easy-to-follow steps!](https://www.xda-developers.com/how-to-sideload-apps-android-tv/ "How to sideload apps on Android TV: APK Install and ADB Sideload methods explained in easy-to-follow steps!")

Not sure how to sideload apps on Android TV? We explain two easy ways to sideload APKs or Android app bundles on Android TV devices.

    [![Image 23: scrcpy](https://static1.xdaimages.com/wordpress/wp-content/uploads/2018/03/scrcpy.jpg)](https://www.xda-developers.com/scrcpy-control-android-on-pc/)Related

##### [Control your Android Smartphone from your PC for free with scrcpy](https://www.xda-developers.com/scrcpy-control-android-on-pc/ "Control your Android Smartphone from your PC for free with scrcpy")

A new tool called "scrcpy" allows you to display your phone screen on your computer with just a USB connection and ADB. No root required.

    [![Image 24: ADB Tips and Tricks](https://static1.xdaimages.com/wordpress/wp-content/uploads/2021/07/ADB-Tips-and-Tricks-option-2.jpg)](https://www.xda-developers.com/adb-tips-tricks/)Related

##### [ADB tips and tricks: Commands that every power user should know about](https://www.xda-developers.com/adb-tips-tricks/ "ADB tips and tricks: Commands that every power user should know about")

There's a lot to the Android Debug Bridge that you may not know about. Click here for some useful tips and tricks for using ADB!
