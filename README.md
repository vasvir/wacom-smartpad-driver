wacom-smartpad-driver
======
## Note: The driver is not functioning. Don't loose your time here.

## Aim
The aim of this project is to develop a Userpace Windows Universal Driver based on DMF Framewrok (DMFU). The driver should be able to communicate with a Wacom SmartPad device in live mode and export a virtual HID interface for general consumption from other windows applications and Windows Ink.

Since I currently only have a Bamboo Slate device the initial support will be for that. However other devices should be easy to add since tuhi has support for them.

## Other Solutions
* Tuhi is a great project that works in Linux and manages to communicate with the device in download and live mode. Tuhi also exposes a virtual HID device so other linux applications such as Krita can use the device. If you are using Linux you don't need to look further than this https://github.com/tuhiproject/tuhi
* Inkspace is the provided solution from Wacom. It is an application (2.7.4) that supports also live mode. The problem is no other application can utilize the pad in live mode. Inkscpace is an electron app and looks like that somebody has posted its sources (2.7.3) on github. Here it is https://github.com/elliotberry/wacom-inkspace

## Windows Driver
Luckily there was a lot of recent work to expose the virtual hid driver as a module in the DMF tree. See here for the relevant discussion.
* https://stackoverflow.com/questions/45773666/developing-an-hid-input-device-driver-for-a-ble-gatt-device-on-windows-10
* https://github.com/microsoft/DMF/issues/69
* https://github.com/Microsoft/DMF/issues/13

So we just need to flesh this sample virtual HID driver with bluetooth communication protocol details from Tuhi.

## How to compile the driver
1. Install Visual Studio
1. From Github get (clone) DMF: https://github.com/microsoft/DMF
1. From Github get (clone) this project: https://github.com/vasvir/wacom-smartpad-driver The projects should be siblings
1. Build DMFU (U is for userspace). Turn off warnings in the following subprojects DmfU, DmfUFramework, DmfUModules.Library if compilation fails. See here how https://stackoverflow.com/questions/2520853/warning-as-error-how-to-rid-these
1. Now build the wacom-smartpad-driver
