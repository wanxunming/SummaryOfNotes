####  Android 真机上进行 React Native 的断点调试：

1. **开启开发者模式：**
   
   - 打开你的 Android 设备的设置。
   - 寻找 "关于手机" 或 "关于设备" 选项，通常在设置的底部。
- 在 "关于手机" 中，寻找 "版本号" 或 "构建号"，然后连续点击多次（通常是7次）以激活开发者选项。
   
2. **启用 USB 调试：**
   
- 在开发者选项中，找到并打开 "USB 调试" 选项。
   
3. **连接设备：**
   
- 使用 USB 数据线将 Android 设备连接到你的计算机。
   
4. **授权计算机：**
   
- 首次连接设备时，可能会显示一个授权对话框，请点击 "允许" 以授权计算机访问设备。
   
5. **启动应用程序：**
   - 在终端中导航到 React Native 项目的根目录。
   - 运行以下命令以在连接的 Android 设备上启动应用程序：
     ```
     npx react-native run-android
     ```

6. **在 VSCode 中启动调试：**
   - 打开 VSCode，并确保已安装 "React Native Tools" 插件。
   - 在左侧导航栏中点击调试图标（虫子图标）以打开调试视图。
   - 点击上方的齿轮图标，选择 "Add Configuration"。
   - 选择 "React Native" 配置。

7. **配置调试器：**
   - 在生成的 `launch.json` 文件中，确保以下设置正确：
     ```json
     "name": "Debug Android",
     "request": "attach",
     "type": "reactnative",
     "target": "android"
     ```

8. **开始调试：**
   
- 点击调试视图中的绿色播放按钮来开始调试会话。
   
9. **触发断点：**
   
- 在你设置断点的代码路径中触发相应的操作，使断点被触发。
   
10. **查看调试信息：**
    
    - 当断点被触发时，VSCode 应该会捕获断点并在调试器中显示变量的值和执行流程。

确保 Android 设备通过 USB 连接到计算机，并已经按照上述步骤开启了开发者模式和启动了 USB 调试。如果在任何步骤中遇到问题，检查设备是否正确连接并且 USB 调试已经启用。（使用 `adb devices`）

##### 识别和连接到已启用 USB 调试的 Android 设备

1. **确保 ADB 已安装：**
   - 在终端中输入 `adb version`，如果出现 ADB 版本信息，则表示 ADB 已经正确安装。

2. **连接 Android 设备：**
   - 使用 USB 数据线将 Android 设备连接到计算机。

3. **运行 `adb devices`：**
   - 在终端中输入 `adb devices` 命令，然后按回车键。
   - 如果一切正常，你应该能够看到连接的 Android 设备的序列号以及其状态为 "device"。

示例输出：

```
List of devices attached
emulator-5554   device
1234abcd        device
```

- `emulator-5554` 或其他类似的标识是模拟器的设备标识。
- `1234abcd` 是真实 Android 设备的序列号。

如果在运行 `adb devices` 命令后未看到设备列表或状态为 "unauthorized"，请确保已启用开发者模式和 USB 调试，并在设备上确认允许计算机的授权。有时可能需要重新插拔 USB 数据线或重新启动设备以使其正常连接。





####  iOS 真机上进行 React Native 应用程序调试

在 iOS 端进行真机调试 React Native 应用程序涉及使用 Xcode 和 VSCode（或其他编辑器）以及一些必要的配置。

1. **安装 Xcode：**
   
- 如果尚未安装 Xcode，请从 Mac App Store 下载并安装 Xcode。
   
2. **连接 iOS 设备：**
   
- 使用 USB 数据线将 iOS 设备连接到计算机。
   
3. **启动应用程序：**
   - 在终端中导航到你的 React Native 项目的根目录。
   - 运行以下命令来启动应用程序在连接的 iOS 设备上：
     ```
     npx react-native run-ios --device "Your Device Name"
     ```
   - 替换 `"Your Device Name"` 为你连接的 iOS 设备的名称。

4. **在 Xcode 中打开项目：**
   - 打开 Xcode。
   - 在 Xcode 中，点击 "Open another project..." 并导航到你的 React Native 项目文件夹。
   - 在项目文件夹中，选择 `.xcworkspace` 文件以打开项目。

5. **选择设备和启动应用程序：**
   - 在 Xcode 的左上角，选择你的 iOS 设备作为目标设备。
   - 点击上方的播放按钮以启动应用程序在 iOS 设备上。

6. **在 Xcode 中设置断点：**
   
- 在你想要设置断点的代码行上，点击行号旁边来设置断点。
   
7. **在 VSCode 中启动调试：**
   - 打开 VSCode，并确保已安装 "React Native Tools" 插件。
   - 在左侧导航栏中点击调试图标（虫子图标）以打开调试视图。
   - 点击上方的齿轮图标，选择 "Add Configuration"。
   - 选择 "React Native" 配置。

8. **配置调试器：**
   - 在生成的 `launch.json` 文件中，确保以下设置正确：
     ```json
     "name": "Debug iOS",
     "request": "attach",
     "type": "reactnative",
     "target": "ios"
     ```

9. **开始调试：**
   
- 点击调试视图中的绿色播放按钮来开始调试会话。
   
10. **触发断点：**
    
- 在你设置断点的代码路径中触发相应的操作，使断点被触发。
    
11. **查看调试信息：**
    
    - 当断点被触发时，VSCode 应该会捕获断点并在调试器中显示变量的值和执行流程。

确保 iOS 设备通过 USB 连接到计算机，并已启用开发者模式。如果在任何步骤中遇到问题，可以检查 Xcode 的设备选择和 VSCode 的调试器输出以获取更多信息。注意，iOS 真机调试通常需要一些与 Xcode 和开发者证书相关的配置。



当涉及到在 iOS 真机上进行 React Native 应用程序调试时，需要一些与 Xcode 和开发者证书相关的配置。以下是关于 Xcode 和开发者证书配置的学习笔记：

##### Xcode 和开发者证书配置（用于 iOS 真机调试）

2. **开启 Apple Developer 账号：**
   - 注册或登录 [Apple Developer](https://developer.apple.com/)，确保你有一个有效的 Apple Developer 账号。

3. **在 Xcode 中设置 Team：**
   - 打开 Xcode。
   - 在 Xcode 的顶部菜单中，选择 "Xcode" > "Preferences"。
   - 在弹出的窗口中，点击 "Accounts"。
   - 添加你的 Apple Developer 账号（如果还没有添加）。
   - 选择你的账号，并在 "Team" 下拉菜单中选择你的开发团队。

4. **在 Apple Developer 上创建 App ID：**
   - 登录 Apple Developer。
   - 导航到 "Certificates, Identifiers & Profiles"。
   - 创建一个新的 App ID，确保 Bundle Identifier 与你的 React Native 项目一致。

5. **创建 Development 证书：**
   - 在 "Certificates, Identifiers & Profiles" 中，导航到 "Certificates"。
   - 创建一个 "iOS Development" 证书。
   - 将证书下载到计算机。

6. **将设备添加到开发者账号：**
   - 在 "Devices" 中添加你要用于测试的 iOS 设备的 UDID。

7. **配置 Xcode 项目：**
   - 在 Xcode 中，打开你的项目。
   - 在 "General" 标签下，确保正确选择了 Team。


