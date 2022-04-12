﻿# Monitorian

Monitorian is a Windows desktop tool to adjust the brightness of multiple monitors with ease.

![Screenshot](Images/Screenshot_main.png)<br>
(DPI: 200%)

The user can change the brightness of monitors, including external ones, either individually or in unison. For the system with an ambient light sensor, the adjusted brightness can be shown along with configured one.

![Screenshot](Images/Screenshot_unison.png)<br>
(DPI: 100%)

In addition, the user can change the adjustable range of brightness and contrast for each monitor seamlessly.

![Screenshot](Images/Screenshot_range.png)&nbsp;
![Screenshot](Images/Screenshot_contrast.png)<br>

Additional languages:

 - Arabic (ar) by @MohammadShughri
 - Catalan (ca) by @ericmp33
 - German (de) by @uDEV2019
 - Spanish (es) by @josemirm and @ericmp33
 - French (fr) by @AlexZeGamer
 - Italian (it) by @GhostyJade
 - Japanese (ja-JP) by @emoacht
 - Korean (ko-KR) by @VenusGirl
 - Dutch (nl-NL) by @JordyEGNL
 - Polish (pl-PL) by @Daxxxis and @FakeMichau
 - Portuguese (pt-BR) by @guilhermgonzaga
 - Romanian (ro) by @calini
 - Russian (ru-RU) by @SigmaTel71
 - Turkish (tr-TR) by @webbudesign
 - Simplified Chinese (zh-Hans) by @ComMouse, @zhujunsan, @XMuli and @FISHandCHEAP
 - Traditional Chinese (zh-Hant) by @toto6038 and @XMuli

## Requirements

 * Windows 7 or newer
 * .NET Framework __4.8__
 * An external monitor must be DDC/CI enabled.
![OSD](Images/Dell_ddcci.jpg)

## Download

 * Microsoft Store (Windows 10 (1607) or newer):<br>
   [Monitorian](https://www.microsoft.com/store/apps/9nw33j738bl0)<br>
   <a href='//www.microsoft.com/store/apps/9nw33j738bl0?cid=storebadge&ocid=badge'><img src='https://developer.microsoft.com/store/badges/images/English_get-it-from-MS.png' alt='Monitorian' width='142px' height='52px'/></a>

 * Winget (a.k.a. [Windows Package Manager](https://docs.microsoft.com/en-us/windows/package-manager), App Installer):
   ```
   winget install Monitorian
   ```

 * Other:<br>
:floppy_disk: [Installer](https://github.com/emoacht/Monitorian/releases/download/3.10.1-Installer/MonitorianInstaller3101.zip)

## Install/Uninstall

If you wish to place executable files on your own, you can extract them from installer file (.msi) by the following command:

```
msiexec /a [source msi file path] targetdir=[destination folder path (absolute path)] /qn
```

In such case, please note the following:

 - The settings file (and other file) will be created at: `[system drive]\Users\[user name]\AppData\Local\Monitorian\`
 - When you check [Start on sign in], a registry value will be added to: `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run`

## Remarks

 - The monitor name shown in main window can be changed to distinguish monitors easily. To change the name, press and hold it until it turns to be editable.
 - To adjust the brightness by a touchpad, place two fingers on it and swipe horizontally. The touchpad must be a precision touchpad.
 - The number of monitors shown at a time is up to 4.

## Add-on Features

Add-on features are available for Microsoft Store version on a subscription basis.

### Hot keys & Shortcut keys

![Screenshot](Images/Screenshot_keys_en.png)

### Command-line options

You can use command-line options to get/set the brigtness.

| Actions                                | Options                                |
|----------------------------------------|----------------------------------------|
| Get brightness of a monitor.           | /get                                   |
| Get brightness of a specified monitor. | /get [Device Instance ID]              |
| Get brightness of all monitors.        | /get all                               |
| Set brightness of a monitor.           | /set [Brightness]                      |
| Set brightness of a specified monitor. | /set [Device Instance ID] [Brightness] |
| Set brightness of all monitors.        | /set all [Brightness]                  |

If this app is called with `/get` option, it will return [Device Instance ID] [Monitor name] [Brightness]. The device instance ID is an unique identifier given by the OS to each monitor. The brightness ranges from 0 to 100%. It can be specified with brightness itself (e.g. 20), increase (e.g. +10) or decrease (e.g. -10) when you use `/set` option.

You can call this app by its name `Monitorian` in command prompt or bat file. From Task Scheduler, it can be performed by the path to its alias `%LOCALAPPDATA%\Microsoft\WindowsApps\Monitorian.exe`. For example, to increase brightness of all monitors by 30%, the Action will be the following:

![Task Scheduler](Images/TaskScheduler_action.png)

The code for add-on features is not included in this repository.

## Development

This app is a WPF app developed and tested with Surface Pro 4 and 7.

### Reporting

The controllability of an external monitor depends on whether the monitor successfully responds to DDC/CI commands. Even if a monitor is expected to be DDC/CI compatible, it may fail to respond (a) if the monitor is weird, (b) if its connection to the system is problematic, or (c) when the system starts or resumes. If an issue is case (a) or (b), this app cannot help it. If case (c), this app may be able to handle it.

In any case, reporting on the controllability of a monitor MUST include probe.log and operation.log described below. The logs will be the starting point to look into the issue.

### Probe

 - You can check the compatibility of your monitor by __probe.log__. It will include raw information on monitors, including capabilities through DDC/CI, from various APIs that are used to find accessible monitors. To get this log, tap `Probe into monitors` in the hidden menu described below.
 - To open the hidden menu, <ins>click app title at the top of menu window 3 times.</ins> 

### Rescan

 - As part of testing, you can manually trigger to rescan monitors via `Rescan monitors` in the hidden menu. A system sound will be played when completed.

### Operations

 - As part of testing, you can set this app to record operations to scan monitors and reflect their states. To enable the recording, check `Make operation log` in the hidden menu. After some information is recorded, you will be able to copy __operation.log__ by `Copy operation log`.
 - If you notice an issue, <ins>enable the recording and then wait until the issue happens. When you notice the issue again, copy this log and check the information including the change before and after the issue.</ins>

### Command-line arguments

 - As part of testing, you can store persistent arguments in `Command-line arguments` in the hidden menu. They will be tested along with current arguments when this app starts.
 - For example, if you want to fix this app's language to English (default), set `/lang en` in this box.

### Exceptions

 - If anything unexpected happens, __exception.log__ will be saved. It will be useful source of information when looking into an issue.

### Setup

1. [Install Visual Studio](https://docs.microsoft.com/en-us/visualstudio/install/install-visual-studio).
2. In Visual Studio Installer, go to the **Individual components** tab and make sure the following components are checked and installed. The version must match the corresponding field of project (.csproj) file of each project.

| Components                                                  | Fields                 |
|-------------------------------------------------------------|------------------------|
| .NET Framework 4.8 SDK<br>.NET Framework 4.8 targeting pack | TargetFrameworkVersion |
| Windows 10 SDK (10.0.19041.0)                               | TargetPlatformVersion  |

3. Load the solution by specifying `/Source/Monitorian.sln`. Then go to the solution explorer and right click the solution name and execute `Restore NuGet Packages`.
4. To open installer project, install [WiX Toolset Build Tools](https://wixtoolset.org/releases/) and [WiX Toolset Visual Studio Extension](https://marketplace.visualstudio.com/items?itemName=WixToolset.WiXToolset). For Visual Studio 2022, Use [latest release](https://github.com/wixtoolset/VisualStudioExtension/releases/tag/v1.0.0.18).

### Globalization

An alternative language can be shown by adding a Resources (.resx) file into `/Source/Monitorian.Core/Properties` folder. Each Resources file stores name/value pairs for a specific language and will be selected automatically depending on the user's environment.

 - The file name must be in `Resources.[language-culture].resx` format.
 - The name of a name/value pair must correspond to that in the default `Resources.resx` file to override it.

## History

Ver 3.10 2022-4-12

 - Redesign small slider
 - Add Catalan (ca) language. Thanks to @ericmp33!
 - Supplement Spanish (es) language. Thanks to @ericmp33!
 - Improve Simplified Chinese (zh-Hans) language. Thanks to @FISHandCHEAP!
 - Supplement Traditional Chinese (zh-Hant) language. Thanks to @XMuli!

Ver 3.9 2022-1-20

 - Add Portuguese (pt-BR) language. Thanks to @guilhermgonzaga!
 - Supplement Simplified Chinese (zh-Hans) language. Thanks to @XMuli!
 - Fix Dutch (nl-NL) language. Thanks to @JordyEGNL!

Ver 3.8 2021-12-18

 - Add Romanian (ro) language. Thanks to @calini!

Ver 3.7 2021-12-3

 - Fix issue of combination of moving in unison and deferring change
 - Modify DPI awareness of the icon

Ver 3.6 2021-9-30

 - Fix count for scan process
 - Add Italian (it) language. Thanks to @GhostyJade!

Ver 3.5 2021-9-9

 - Make rounded corners default on Windows 11
 - Add Traditional Chinese (zh-Hant) language. Thanks to @toto6038!

Ver 3.4 2021-8-30

 - Add Dutch (nl-NL) language. Thanks to @JordyEGNL!
 - Supplement Simplified Chinese (zh-Hans) language. Thanks to @zhujunsan!

Ver 3.3 2021-8-20

 - Add Arabic (ar) language. Thanks to @MohammadShughri!

Ver 3.2 2021-8-9

 - Supplement German (de) language. Thanks to @uDEV2019!

Ver 3.1 2021-8-4

 - Supplement Polish (pl-PL) language. Thanks to @FakeMichau!
 - Add Turkish (tr-TR) language. Thanks to @webbudesign!
 - Supplement Russian (ru-RU) language. Thanks to @SigmaTel71!
 - Add Spanish (es) language. Thanks to @josemirm!

Ver 3.0 2021-7-1

 - Change UI

Ver 2.19 2021-6-16

 - Enable to adjust brightness by precision touchpad

Ver 2.18 2021-5-23

 - Add German (de) language. Thanks to @uDEV2019!

Ver 2.17 2021-5-19

 - Add French (fr) language. Thanks to @AlexZeGamer!

Ver 2.16 2021-4-11

 - Add Korean (ko-KR) language. Thanks to @VenusGirl!

Ver 2.14 2021-3-26

 - Improve internal processes

Ver 2.13 2021-2-13

 - Improve internal process

Ver 2.11 2021-1-26

 - Add Russian (ru-RU) language. Thanks to @SigmaTel71!
 - Add Polish (pl-PL) language. Thanks to @Daxxxis!
 - Add Simplified Chinese (zh-Hans) language. Thanks to @ComMouse!

Ver 2.9 2020-12-22

 - Improve codes

Ver 2.8 2020-11-23

 - Adjust mouse wheel roll

Ver 2.7 2020-10-30

 - Enable to change adjustable range
 - Adjust scan process
 - Add get/set brightness test to probe

Ver 2.6 2020-8-10

 - Enable to defer update of brightness

Ver 2.5 2020-8-1

 - Fix issue on empty description

Ver 2.4 2019-12-30

 - Improve scan process

Ver 2.3 2019-11-28

 - Change scan process

Ver 2.2 2019-11-18

 - Change setting to show adjusted brightness by ambient light enabled as default
 - Fix bugs

Ver 2.1 2019-11-6

 - Change location to show when the icon is in overflow area
 - Change behavior when sliders are moving in unison
 - Fix bugs

Ver 2.0 2019-8-6

 - Enable operation by arrow keys
 - Redesign slider

Ver 1.12 2019-3-9

 - Modify to handle raw brightnesses correctly when raw minimum and maximum brightnesses are not standard values. Thanks to @reflecat!
 - Change target framework to .NET Framework 4.7.2

Ver 1.11 2019-2-7

 - Further suppress an exception

Ver 1.10 2019-2-3

 - Change to enable transparency and blur effects only when transparency effects of OS is on

Ver 1.9 2018-12-5

 - Change scan timings after resume

Ver 1.8 2018-11-24

 - Supplement generic monitor name with connection type

Ver 1.7 2018-8-22

 - Improved finding monitor name for Windows 10 April 2018 Update (1803)

Ver 1.6 2018-5-25

 - Extended function to control DDC/CI connected monitor
 - Modified function to enable moving together

Ver 1.5 2018-2-12

 - Improved handling of uncontrollable monitor

Ver 1.4 2018-1-17

 - Modified handling of monitor names

Ver 1.2 2017-10-12

 - Added control by mouse wheel
 - Added function to show adjusted brightness

Ver 1.0 2017-2-22

 - Initial release

## License

 - MIT License

## Libraries

 - [XamlBehaviors for WPF](https://github.com/microsoft/XamlBehaviorsWpf)

## Developer

 - emoacht (emotom[atmark]pobox.com)
