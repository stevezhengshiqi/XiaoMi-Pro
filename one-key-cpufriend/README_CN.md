# 调整 macOS CPU性能

[English](README.md) | 中文

## 简介

[我](https://github.com/stevezhengshiqi)还是个bash语言新手，欢迎大佬们帮助我改善脚本。

<b>这个脚本只支持8代U (KBL-R, CNL, CFL...)</b>。

这个脚本能修改低频率模式和性能模式，然后用[ResourceConverter.sh](https://github.com/acidanthera/CPUFriend/tree/master/ResourceConverter) 来生成定制的 `CPUFriendDataProvider.kext`。

此脚本不会修改系统文件夹下的任何文件。如果你对调整不满意，可以删除 `/CLOVER/kexts/Other/` 里的 `CPUFriend*.kext`，再重启来恢复原样。


## 使用前提

- 阅读 [CPUFriend WARNING](https://github.com/acidanthera/CPUFriend/blob/master/Instructions.md#warning)
- 网络环境良好
- 确保 `IOPlatformPluginFamily.kext` 未经修改
- 确保[Lilu](https://github.com/acidanthera/Lilu)在工作
- `plugin-type=1`


## 使用方法

- 在终端输入以下命令并回车：

```bash
bash -c "$(curl -fsSL https://raw.githubusercontent.com/daliansky/XiaoMi-Pro-Hackintosh/master/one-key-cpufriend/one-key-cpufriend_cn.sh)"
```

- <b>如果是Clover用户：</b>
  - 把桌面上的 `CPUFriend.kext` 和 `CPUFriendDataProvider.kext` 复制进 `/CLOVER/kexts/Other/` 并重启。
  
- <b>如果是OC用户：</b>
  - 把桌面上的 `CPUFriend.kext` 和 `CPUFriendDataProvider.kext` 复制进 `/OC/Kexts/`。
  - 打开 `/OC/config.plist` 并找到以下代码：
```
<dict>
    <key>BundlePath</key>
    <string>CPUFriend.kext</string>
    <key>Comment</key>
    <string>Power Management</string>
    <key>Enabled</key>
    <false/>
    <key>ExecutablePath</key>
    <string>Contents/MacOS/CPUFriend</string>
    <key>MaxKernel</key>
    <string></string>
    <key>MinKernel</key>
    <string></string>
    <key>PlistPath</key>
    <string>Contents/Info.plist</string>
</dict>
<dict>
    <key>BundlePath</key>
    <string>CPUFriendDataProvider.kext</string>
    <key>Comment</key>
    <string>Power Management</string>
    <key>Enabled</key>
    <false/> 
```
修改为：
```
<dict>
    <key>BundlePath</key>
    <string>CPUFriend.kext</string>
    <key>Comment</key>
    <string>Power Management</string>
    <key>Enabled</key>
    <true/>
    <key>ExecutablePath</key>
    <string>Contents/MacOS/CPUFriend</string>
    <key>MaxKernel</key>
    <string></string>
    <key>MinKernel</key>
    <string></string>
    <key>PlistPath</key>
    <string>Contents/Info.plist</string>
</dict>
<dict>
    <key>BundlePath</key>
    <string>CPUFriendDataProvider.kext</string>
    <key>Comment</key>
    <string>Power Management</string>
    <key>Enabled</key>
    <true/>  
```


## 恢复

- <b>如果是Clover用户：</b>
  - 如果你对调整不满意，删除 `/CLOVER/kexts/Other/` 里的 `CPUFriend.kext` 和 `CPUFriendDataProvider.kext`，再重启来恢复原样。

  - 如果很不幸，你无法进入系统，而且你确定是由 `CPUFriend*.kext` 导致的，

    - 当你进入Clover界面时，按 `空格键` 
    - 用键盘来选择 `Block Injected kexts` - `Other` 
    - 勾选 `CPUFriend.kext` 和 `CPUFriendDataProvider.kext`
    - Return到主界面并启动系统，然后从你的CLOVER文件夹删除 `CPUFriend*.kext`

- <b>如果是OC用户：</b>
  - 逆向操作[使用方法](#使用方法)小节并重启


## 修改macOS下的CPU电压

[fladnaG86](https://github.com/fladnaG86)在[#150](https://github.com/daliansky/XiaoMi-Pro/issues/150)提供了macOS上降低CPU/GPU/缓存存储器电压的脚本，欢迎大家尝试！


## 鸣谢

- 感谢 [Acidanthera](https://github.com/acidanthera) 提供 [CPUFriend](https://github.com/acidanthera/CPUFriend)。
- 感谢 [shuhung](https://www.tonymacx86.com/members/shuhung.957282) 提供[配置修改思路](https://www.tonymacx86.com/threads/skylake-hwp-enable.214915/page-7)。
- 感谢 [PMheart](https://github.com/PMheart) 和 [xzhih](https://github.com/xzhih) 提供一些建议。
