# Hackintosh_Of_Lenovo_R720

![info](img/info.png)

这个项目是我根据远景论坛上的项目修改而来，并非原创。本人加上了USB定制，从而做到睡眠基本正常，USB定制请参考黑果小兵的[Hackintool(原Intel FB-Patcher)使用教程及插入姿势](https://blog.daliansky.net/Intel-FB-Patcher-tutorial-and-insertion-pose.html)。目前我测试到**10.15.2**，~~最新的10.15.2还没有测试过，如果你想试的话，请更新CLOVERX64.efi到最新版本~~。本项目自带的序列号等信息已经被我更改了，请你自行更改成你需要的。

> 由于我使用的是dw1560网卡，没有使用该网卡的请自行删除/kext/Other/目录下的AirportBrcmFixup.kex、BrcmBluetoothInjector.kext、BrcmFirmwareData.kext、BrcmPatchRAM3.kext这四个与该网卡有关的驱动。


声卡注入ID是28，采用AppleALC.kext驱动。

![audio](img/audio.png)

蓝牙、Wi-Fi、核显正常。

![info](img/gpu.png)

![info](img/Bluetooth.png)

- 2020-1-27更新

  由于我的系统更新为10.15.2版本，因而更新clover为最新版本。不得不说的是，之前定制了USB驱动之后，睡眠正常了几天，但是下载睡眠功能又不正常了。出现的具体问题为睡眠唤醒后，鼠标的左键功能损坏，点击后与右键更能一致。

- 2020-1-27晚更新

  鼠标左键问题已经定位，在macOS中，ctrl+鼠标左键就是点击鼠标右键，因而你唤醒后按一下ctrl键就没有问题。