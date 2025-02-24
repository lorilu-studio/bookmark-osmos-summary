# How to install ADB on Windows, macOS, and Linux
- URL: https://www.xda-developers.com/install-adb-windows-macos-linux/
- Added At: 2025-02-24 00:43:35
- [Link To Text](2025-02-24-how-to-install-adb-on-windows,-macos,-and-linux_raw.md)

## TL;DR
ADB（Android Debug Bridge）是Google提供的调试工具，支持通过USB或无线方式从计算机向Android设备发送命令。设置ADB需要在手机端启用开发者模式和USB调试，电脑端则需下载并配置Android SDK Platform Tools。ADB支持多种高级功能，如无线调试、应用安装、文件传输等，还可用于进入恢复模式、卸载预装应用等操作。通过掌握ADB命令，开发者可以更高效地调试和管理Android设备。

## Summary
1. **ADB简介**：
   - **定义**：Android Debug Bridge (ADB) 是Google为开发者提供的工具，用于调试和测试Android手机上的软件。
   - **功能**：提供对普通用户不可用的高级功能的访问，允许通过USB或无线方式从计算机向Android设备发送命令。
   - **架构**：基于客户端-服务器架构，包含三个组件：
     - **客户端**：连接的PC/Mac/Chromebook。
     - **守护进程**：在Android设备上运行命令的“adbd”。
     - **服务器**：管理客户端和守护进程之间的通信。

2. **ADB设置步骤**：
   - **手机端设置**：
     1. 打开**设置**应用。
     2. 点击**关于手机**选项。
     3. 连续点击**版本号**七次以启用开发者模式。
     4. 返回主设置界面，找到并启用**开发者选项**中的**USB调试**。
   - **电脑端设置**：
     - **Windows**：
       1. 下载并解压Android SDK Platform Tools ZIP文件。
       2. 打开文件资源管理器，导航到解压文件夹。
       3. 右键点击空白处，选择**在终端中打开**。
       4. 连接手机并输入`./adb devices`命令。
     - **macOS**：
       1. 下载并解压Android SDK Platform Tools ZIP文件。
       2. 打开终端，导航到解压文件夹。
       3. 连接手机并输入`./adb devices`命令。
     - **Linux**：
       1. 下载并解压Android SDK Platform Tools ZIP文件。
       2. 打开终端，导航到解压文件夹。
       3. 连接手机并输入`./adb devices`命令。

3. **ADB路径环境变量设置**：
   - **Windows**：
     1. 右键点击**开始**按钮，选择**系统**。
     2. 点击**高级系统设置**，然后点击**环境变量**。
     3. 在**系统变量**中找到**Path**，双击并添加ADB文件夹路径。
   - **macOS**：
     1. 打开终端，导航到主目录。
     2. 创建或编辑`.bash_profile`或`.zshrc`文件，添加ADB路径。
     3. 保存文件并重新加载shell设置。
   - **Linux**：
     1. 打开终端，导航到主目录。
     2. 编辑`.bashrc`文件，添加ADB路径。
     3. 保存文件并重新加载shell设置。

4. **ADB高级用法**：
   - **WSL和ChromeOS**：
     - **WSL**：通过`usbipd-win`项目实现USB设备访问。
     - **ChromeOS**：启用Linux开发环境后，按照Linux步骤设置ADB。
   - **浏览器ADB**：使用WebUSB API通过浏览器控制Android设备，如Tango项目。
   - **Wi-Fi ADB**：
     1. 确保PC和手机连接同一Wi-Fi网络。
     2. 在手机上启用**无线调试**并配对设备。
     3. 在PC上使用`adb pair`和`adb connect`命令连接设备。

5. **ADB命令示例**：
   - 列出连接的设备：`adb devices`
   - 杀死ADB服务器：`adb kill-server`
   - 安装应用：`adb install <path_to_APK>`
   - 端口转发：`adb forward tcp:6100 tcp:7100`
   - 从设备复制文件：`adb pull <remote_path> <local_path>`
   - 向设备复制文件：`adb push <local_path> <remote_path>`
   - 启动ADB Shell：`adb shell`

6. **ADB的其他用途**：
   - **进入恢复模式**：通过ADB命令或按钮组合进入恢复模式。
   - **卸载预装应用**：使用ADB命令卸载运营商或OEM预装应用。
   - **无PC操作**：使用LADB应用在手机上运行ADB命令。
   - **Android TV应用侧载**：通过ADB或APK安装方法侧载应用到Android TV。
   - **PC控制手机**：使用scrcpy工具在PC上显示和控制Android手机屏幕。
   - **ADB技巧**：掌握ADB命令的高级用法，提升使用效率。
