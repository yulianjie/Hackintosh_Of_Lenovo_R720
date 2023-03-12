# Hackintosh_Of_Lenovo_R720

![info](img/info-1131.png)

> 10.15.x 的 efi 使用请查看[clover10.15.7.md](clover10.15.7.md)说明，本项目已经兼容到 12.3.1.

这个项目直接基于官方的 OC 文件，本人加上了 USB 定制，从而做到睡眠基本正常，USB 定制请参考国光的[USB定制教程](https://apple.sqlsec.com/6-%E5%AE%9E%E7%94%A8%E5%A7%BF%E5%8A%BF/6-1/)。目前我测试到`Monterey 12.3.1`。**本项目自带的序列号等信息已经被我更改了，请你自行更改成你需要的！！！**

由于我使用的是 dw1560 网卡，没有使用该网卡的请**自行删除**/kext/Other/目录下的 AirportBrcmFixup.kext、BrcmBluetoothInjector.kext、BrcmFirmwareData.kext、BrcmPatchRAM3.kext、BlueToolFixup.kext 这几个与该网卡有关的驱动，并在`config.plist`中删除驱动的加载，或者对于 12 的配置中，将`config_nodw1560.plist`重命名为`config.plist`。


## 修复要点

1. 更新到 macOS 12 版本的时候，使用的 DW1560 网卡需要修复蓝牙驱动，使用[BrcmPatchRAM](https://github.com/acidanthera/BrcmPatchRAM)中采用`BlueToolFixup.kext`驱动，并且在 config.plist 中将`BrcmBluetoothInjector.kext`的驱动加载禁用。

   ![12蓝牙驱动修复](img/Bluetooth-12.png)

2. 声卡注入 ID 是 28，采用 AppleALC.kext 驱动。
   ![audio](img/audio-11.1.png)

3. 蓝牙、Wi-Fi、核显正常，~~但是由于我更换了 dw1560 网卡，所以在更新到 11.1 的时候 WiFi 无法驱动，看来远景论坛上各位网友的方法后，发现需要删除 AirportbcmFixup.kext 中的 4360 驱动~~。
   ![airportbcmfixup](img/airportbcmfixupedit.png)
   ![info](img/gpu-11.png)
   ![info](img/Bluetooth-11.png)

4. CPU 变频基本完美。
   ![变频](img/cpu-12.png)
   ![intel power gadget](img/cpu-intel.png)

5. 核显驱动方法见：[黑苹果 4 步驱动 Intel 核显](https://blog.zuiyu1818.cn/posts/Hac_Intel_Graphics_simple.html) ，~~我使用的是 0x16190000 ，至于为什么模拟的是上一代的 CPU，主要是我试了用 0x591B00，发现效果并没有这个好，而且日常使用也没有任何问题~~最终还是用了 0x59160000。

6. 睡眠后点击鼠标左键有问题的请点击`Ctrl`键，详见[Issue #1](https://github.com/JackietYu/Hackintosh_Of_Lenovo_R720/issues/1)

7. 关于 App Store 无法下载应用或者安装时卡住，请参考[Big Sur 11.01 Clover R5126 Can't download or update from App Store · Issue #300](https://github.com/CloverHackyColor/CloverBootloader/issues/300)，原版是这样描述的：

   > 1. use full installer media (U disk or partition)
   > 2. boot clover r5126, boot installer
   > 3. install 11.0.1 and cover the current partition (we call this partition name as Macintosh in this example)
   > 4. on the 2nd step of installation, choose boot install of your Macintosh partition
   > 5. on the 3rd step of the installation, **MUST** choose Boot **preboot** from Macintosh
   > 6. then you can success install/ update appa from mac app store

   简单的说就是我们升级的时候，在前两部都是选择 install 选项，第三步需要选择 preboot 选项，之前的安装时不需要的，之后每次的启动也需要从 preboot 启动项进入，不然无法正常启动。

8. 升级到了 11.3.1 之后，没法对显示器亮度进行调节，因而对 DSDT 进行编辑，从而基本完美，见[黑苹果修复显示器亮度调节 ](https://www.jianshu.com/p/7119281b6afe)如何使用 DSDT 修复显示器亮度调节。

## 更新日志

- 2023-03-12
  
  更新OC版本到0.9.0，精简了ACPI文件，使用Windows定制了usb驱动。

- 2022-02-28

  由于太久没更新，直接更新到了 12.2.1 版本，修复了蓝牙驱动问题。

- 2021-05-16

  对于本项目进行较大的更新，更新 clover 到 5131 版本，更新了大部分驱动，去除了一些不必要的文件，还有解决了[issue7](https://github.com/JackietYu/Hackintosh_Of_Lenovo_R720/issues/7)中升级 11.3.1 后没法对显示器亮度进行调节的问题调节，见步骤 7。

- 2021-03-11

  更新 clover 到 5131 版本，支持到 11.2.3

- 2021-01-11

  更新支持到了 11.1，如果你不想更新到 11.1，请勿采用最新的 efi 文件。

- 2021-01-08

  最近没有更新系统版本，但是对部分驱动更新了，现在运行 10.15.6 版本感觉不错，不插电耗电也比之前好多了。Opencore 都出来这么久了，不是我不想换，而是我正在尝试当中，还有许多问题没有解决。

- 2020-08-06

  更新到了 10.15.6，电量显示掉了，加了`ACPIBatteryManager.kext`这个驱动后，现在显示正常。

- 2020-05-12

  更新支持到 10.15.4，只是我个人使用没什么问题，不保证都能使用

- 2020-1-27 晚更新

  鼠标左键问题已经定位，在 macOS 中，ctrl+鼠标左键就是点击鼠标右键，因而你唤醒后按一下 ctrl 键就没有问题。

- 2020-1-27 更新

  由于我的系统更新为 10.15.2 版本，因而更新 clover 为最新版本。不得不说的是，之前定制了 USB 驱动之后，睡眠正常了几天，但是下载睡眠功能又不正常了。出现的具体问题为睡眠唤醒后，鼠标的左键功能损坏，点击后与右键更能一致。

  ## 致谢

  黑苹果的顺利安装离不开活跃的社区支持以及一些黑苹果大佬的教学，感谢：
  
  1. 黒果小兵的[教程](https://blog.daliansky.net/)
  2. [国光的黑苹果安装教程：手把手教你配置 OpenCore](https://apple.sqlsec.com/)
