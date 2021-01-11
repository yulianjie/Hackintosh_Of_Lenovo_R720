# Hackintosh_Of_Lenovo_R720

![info](img/info_bigsur.png)

> 10.15.x的efi使用请查看[clover10.15.7.md](clover10.15.7.md)说明，本项目已经兼容到11.1.

这个项目直接基于官方的clover文件，本人加上了USB定制，从而做到睡眠基本正常，USB定制请参考黑果小兵的[Hackintool(原Intel FB-Patcher)使用教程及插入姿势](https://blog.daliansky.net/Intel-FB-Patcher-tutorial-and-insertion-pose.html)。目前我测试到`Big Sur 11.1`。本项目自带的序列号等信息已经被我更改了，请你自行更改成你需要的。

由于我使用的是dw1560网卡，没有使用该网卡的请自行删除/kext/Other/目录下的AirportBrcmFixup.kext、BrcmBluetoothInjector.kext、BrcmFirmwareData.kext、BrcmPatchRAM3.kext这四个与该网卡有关的驱动。

1. 声卡注入ID是28，采用AppleALC.kext驱动。

![audio](img/audio-11.1.png)

2. 蓝牙、Wi-Fi、核显正常，但是由于我更换了dw1560网卡，所以在更新到11.1的时候WiFi无法驱动，看来远景论坛上各位网友的方法后，发现需要删除AirportbcmFixup.kext中的4360驱动。

   ![airportbcmfixup](img/airportbcmfixupedit.png)

![info](img/gpu-11.png)

![info](img/Bluetooth-11.png)



3. 变频我还没完善，10.15.7默认的有20档，基本可以说是非常完美了。但是升级到了11.1，好像是CPUs的bug，一开启软件CPU频率就会拉满，只测到了8个频档

![变频](img/cpu-20.png)

![变频11.1](img/cpu-8.png)

![intel power gadget](img/cpu-intel.png)

4.核显驱动方法见：[黑苹果 | 4 步驱动 Intel 核显](https://blog.zuiyu1818.cn/posts/Hac_Intel_Graphics_simple.html) ，我使用的是0x16190000 ，至于为什么模拟的是上一代的CPU，主要是我试了用0x591B00，发现效果并没有这个好，而且日常使用也没有任何问题。

5. 睡眠后点击鼠标左键有问题的请点击`Ctrl`键，详见[Issue #1](https://github.com/JackietYu/Hackintosh_Of_Lenovo_R720/issues/1)



- 2021-01-11

  更新支持到了11.1，如果你不想更新到11.1，请勿采用最新的efi文件。

- 2021-01-08

  最近没有更新系统版本，但是对部分驱动更新了，现在运行10.15.6版本感觉不错，不插电耗电也比之前好多了。Opencore都出来这么久了，不是我不想换，而是我正在尝试当中，还有许多问题没有解决。

- 2020-08-06

  更新到了10.15.6，电量显示掉了，加了`ACPIBatteryManager.kext`这个驱动后，现在显示正常。

- 2020-05-12

  更新支持到10.15.4，只是我个人使用没什么问题，不保证都能使用

- 2020-1-27晚更新

  鼠标左键问题已经定位，在macOS中，ctrl+鼠标左键就是点击鼠标右键，因而你唤醒后按一下ctrl键就没有问题。

- 2020-1-27更新

  由于我的系统更新为10.15.2版本，因而更新clover为最新版本。不得不说的是，之前定制了USB驱动之后，睡眠正常了几天，但是下载睡眠功能又不正常了。出现的具体问题为睡眠唤醒后，鼠标的左键功能损坏，点击后与右键更能一致。

  

