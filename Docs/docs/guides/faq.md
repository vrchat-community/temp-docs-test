# Frequently Asked Questions
## What does 'VCC' mean?
**V**RChat **C**reator **C**ompanion. It's the official tool for creating and updating Unity projects for VRChat. Read more about the Creator Companion on our [glossary page](https://vcc.docs.vrchat.com/guides/glossary/). 
## Why is my project missing packages? Or why can't I create a backup?
The most common cause we've seen for this is that **the path to your project is longer than Windows can handle**.
* Try creating your project at a path with fewer overall characters, like
  `C:\Projects\My Project` rather than
  `C:\Users\Username\Documents\Projects\VRChat\NewStuff\2022\My very very very very very very very very very very very very very very very very very long project`
* Alternatively, [enable Win32 long paths in your Windows settings](https://learn.microsoft.com/en-us/windows/win32/fileio/maximum-file-path-limitation?tabs=registry#enable-long-paths-in-windows-10-version-1607-and-later). (This setting is disabled by default in Windows and may lead to issues in older software.)
## What are the benefits of the Creator Companion?
The Creator Companion makes VRChat world or avatar creation more accessible and faster. It can automatically install the Unity Editor and Hub, download the VRChat SDKs and create and update your projects.
Starting in 2023, new [VRChat SDK](https://docs.vrchat.com/docs/choosing-your-sdk) updates will only be available through the Creator Companion. If you'd like to use VRChat's newest SDK features in new or existing projects, [use the VCC](https://vcc.docs.vrchat.com/guides/getting-started/).
## Where did my scene go? Why is it blank?
After migration, Unity may show you a blank scene (with a `Main Camera` and `Directional Light`). Your scene is *probably* still there - Browse your `/Assets/` folder to find it.
Some folders are **not** copied during migration. If your scene was previously saved as the SampleScene or the UdonExampleScene, you must first save it to your `/Assets/` folder before migration. Read about [Migrating Projects](https://vcc.docs.vrchat.com/vpm/migrating) to learn more.
## Should I import legacy SDK packages `VRCSDK3[...].unitypackage` with the Creator Companion?
No. VRChat SDK packages are managed by the VCC. Importing VRChat's Legacy SDK into a VCC project may break it. Read our [Getting Started](https://vcc.docs.vrchat.com/guides/getting-started) page to learn more about how the VCC imports the VRChat SDK.
For users who prefer the Legacy style of setting up the SDK, we provide `VRChat-Worlds-SDK-[...].unitypackage` files on our websites. These files can only be used for new projects and are fully compatible with the Creator Companion.
## Can I still use `.unitypackage` files for custom assets?
Yes. The VCC changes how the VRChat SDK is imported, but `.unitypackage` legacy packages can still be distributed and imported as before. Keep in mind that old legacy packages may not work in newer versions of the SDK.
If you create assets for other users, make sure to test them with these new SDKs to discover and fix any compatibility issues. You may need to create new versions of your assets if you're referencing VRChat's built-in assets, or if your Udon programs use older versions of [UdonSharp](https://udonsharp.docs.vrchat.com).
The VCC also allows you to distribute packages using the new VPM format, making it even easier for your users to install and update your custom content. Read the [Packages](https://vcc.docs.vrchat.com/vpm/packages) page to learn more.

## What do I do if Webview2 is not installed correctly?
![VRC Quick Launcher GUI](/images/webview2-error.png)
The Creator Companion uses Webview2 to render its user interface. When you launch the Creator Companion, it will attempt to install it automatically.

If you previously removed Microsoft Edge from your system, the Creator Companion may fail to launch correctly. WebView2 is usually installed alongside Microsoft Edge. 

This can usually be fixed by properly reinstalling Webview2. If Microsoft Edge runs correctly, then the Creator Companion should work correctly, too.

Download links
- Webview2: https://developer.microsoft.com/en-us/microsoft-edge/webview2
- Microsoft Edge: https://www.microsoft.com/en-us/edge

## I just installed Unity Hub and Unity. Why is Unity not launching?

If you've installed Unity Hub but never launched it, your license may not have been activated. Unity cannot run without a valid license. It may try to launch, but silently fail.

[Click here](https://support.unity.com/hc/en-us/articles/211438683-How-do-I-activate-my-license-) to learn how to activate your Personal license. (It's free!)

If Unity is still failing to launch, you may want to view Unity's or Unity Hub's log files to find more information. [Here's how.](https://docs.unity3d.com/Manual/LogFiles.html)

## Where do I find the Creator Companion's log files?
The Creator Companion's logs can be found in:
- In the 'Logs' tab
- In the 'Settings' tab -> Files and Folders -> Logs
- In the folder `C:\Users\[Your Name]\AppData\Local\VRChatCreatorCompanion\Logs`

Every time to start the Creator Companion, it will create a log file like this:
`20230307T025652-log.txt`(Year, month, day, hours, minutes, seconds)

## What do I do if I'm stuck on the Requirements Screen?

Outdated versions of the Creator Companion may get stuck on the 'Requirements' screen. This usually happens if your settings file may be corrupted, or a package listing may have been downloaded incorrectly.
![image](https://user-images.githubusercontent.com/737888/204419137-d4a3a4ee-5035-4540-a27a-f871531bee7c.png)
To fix this, please download the newest version of the Creator Companion at https://vrchat.com/download/vcc and follow the steps below.

## What do I do if my settings file is invalid?
If your settings file is corrupted (either through manual editing or through a bug), the Creator Companion may not launch correctly. You may see an error message, or the Creator Companion may fail to launch.

You can find the settings file at `%LocalAppData%\VRChatCreatorCompanion\settings.json` or at `C:\Users\You\AppData\Local\VRChatCreatorCompanion\settings.json`.

To fix it, you may need to delete your `settings.json` file.
1. Close the VCC.
2. Open the folder `%LocalAppData%\VRChatCreatorCompanion\` 
    - For example:  `C:\Users\Username\AppData\Local\VRChatCreatorCompanion\`
3. Delete `settings.json`.
4. Open the VCC.
    - This should automatically recreate `settings.json`.
    - Your preferences and project list will be reset.

If your settings file was corrupted, please submit a [bug report](https://github.com/vrchat-community/creator-companion/issues/new?assignees=&labels=&template=bug_report.md&title=%5BBUG%5D) and send us your `settings.json`.

## How to add more packages to the Creator Companion?

Beyond the packages provided by VRChat and the Curated creators - you can add your own packages to the Creator Companion.

You can do so in two ways:

1. Add local packages that already exist on your computer. You can do so in the User Packages section of the Packages tab on the Settings page.
2. Add community packages by installing a Community Repository. To add new repositories to the Creator Companion [take a look at this guide](/guides/community-repositories).

## Where can I ask more questions?
Make sure to read the [VCC documentation](https://vcc.docs.vrchat.com/) to learn more about the Creator Companion.

Please submit bug reports and feature requests to our [GitHub issue tracker](https://vcc.docs.vrchat.com/guides/bugs-features/). If you'd like to talk to other creators about the VCC, head to the official [VRChat Discord server](https://discord.com/invite/vrchat).
