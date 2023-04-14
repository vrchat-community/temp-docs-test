
# CLI
The VRChat Package Manager is available as a Command Line Interface application, for advanced users and automation.

## Installation & Updating
You'll need the [.NET 6 SDK](https://dotnet.microsoft.com/en-us/download/dotnet/6.0) installed.
Then just open a terminal and type:

```console
dotnet tool install --global vrchat.vpm.cli
```

This will make it available at any command prompt just by typing `vpm`! You need the latest templates to make/migrate projects, so a great first thing to run is `vpm install templates` - more on that in the [install templates](#install-templates) section.

You can always update the tool to the latest version with the command: 
```console
dotnet tool update --global vrchat.vpm.cli
```

You can uninstall it with the command:
```console
dotnet tool uninstall --global vrchat.vpm.cli
```

To learn more about what's going on, read the [.NET Tool Docs](https://docs.microsoft.com/en-us/dotnet/core/tools/global-tools#install-a-global-tool).

## Projects
VRChat Projects are Unity projects which have the VRChat SDK in them.
### new
Creates a new VRChat project from a template

```console
vpm new <projectName> [template] [-p path]
```

**Arguments**

* **projectName**: The name for the new project. Will have numbers added to it if another project already exists with this name in the target directory.

* **template**: Optional template to use. If you don't provide one, the barebones "Base" template will be used, which includes only the VRChat Base SDK package. You can use the name of one of the built-in templates, or provide an absolute path to your own template.
  **built-in templates**: "Base", "World", "Avatar", "UdonSharp"

* **path**: Optional absolute path to use when creating the project. If not provided, the current directory will be used.

### check project
Checks whether a given name or path points to a compatible VRChat project.

```console 
vpm check project [<name>]
```

**Arguments**

* **name**: Optional name of the project to find. If not provided, the current directory will be checked.Otherwise, the following places will be searched:
* Name as absolute path
* Name as relative path from current directory
* Name from list in settings stored as `userProjects`

If the project is found, its type will be printed to the console.

Returns a 0 if a project is found, and a 1 if it is not.

### migrate project
Migrates projects created with the legacy .unitypackage SDKs to the new system if they use the SDK3 Worlds or Avatars unitypackages (SDK2 not supported). They can be Unity 2017, 2018 or 2019 projects. Will also migrate UdonSharp and CyanEmu to the new package-based versions.

```console 
vpm migrate project [projectPath]
```

**Arguments**
* **projectPath**: The path to the unity project you want to migrate.

**Options**
* **--inplace**: Migrate project in place instead of creating a copy. Not recommended unless you have your own backup of the project

If the project is found and it can be migrated it will be automatically upgraded to the new system.

Returns a 0 if a project is found and it can be migrated, and a 1 if it is not found or can't be migrated.

## Packages
[Packages](packages) are code and assets in a portable format, stored in in zip files and pulled into your project by the VRChat Package Manager.

### check package
Reports the info from a package, or tells if you if it is not found/invalid.

```console 
vpm check package <name>
```

**Arguments**

* **name**: The package to check. This can be the unique name of any package in the Official or Curated package listings, like `com.vrchat.worlds` or `com.vrchat.udonsharp`, or it can be a relative or absolute path to a local package.

**Examples**
* `vpm check com.vrchat.avatars`
  * Prints info about the official Avatars package
* `vpm check "C:/MyPackages/MirrorExploder"`
  * Prints info about the local package "MirrorExploder".

### add package
Adds a VPM package to an existing Project

```console 
vpm add package <packageName> [-p <project>]
```

**Arguments**
* **packageName**: The package to add. This can be the unique name of any package in the Official or Curated package listings, like `com.vrchat.worlds` or `com.vrchat.udonsharp`, or it can be a relative or absolute path to a local package.

**Options**
* **-p|--project**: Specifies the project to which the package will be added. If no argument is provided, the method will look in the current directory. If provided, the value can be an absolute or relative path to a Unity Project, or the name of a project which you have added to your `userProjects` list. 

**Examples**
* `vpm add package com.vrchat.avatars`
  * Adds the official Avatars package to the project in the current directory.
* `vpm add package "C:/MyPackages/MirrorExploder" "../MyProjectDir"`
  * Adds my local package "MirrorExploder" to the project which is one directory up from the current working directory.

## Templates
[Templates](templates) are barebones VRChat projects which can be used as a starting point for new projects, pulling in your favorite packages, prefabs and tools to get running quickly.

:::tip

We also provide the templates as git repositories you can use directly. [Here's the guide](/guides/using-project-template-repos) with all the links and instructions.

:::

### install templates
Installs the latest version of the VRChat templates to `AppData/Local/VRChatCreatorCompanion/VRCTemplates`, overwriting files that are there. Useful if you're using the CLI without having installed the VCC GUI. 

```console 
vpm install templates
```

Note that this will clear out the existing template first - user templates should be put into `AppData/Local/VRChatCreatorCompanion/Templates` instead.

### list templates
Prints out the names and paths of the Official VRChat Templates, and the paths of the installed User Templates.

```console 
vpm list templates
```

### check template
Reports the version from a template, or tells if you if it is not found/invalid.

```console 
vpm check template <template>
```

**Arguments**

* **template**: The template to check. This can be the displayName of any built-in template or an absolute path to your own project template.

**built-in templates**: "Base", "World", "Avatar", "UdonSharp"

## Repos
Repos are listings of Packages. You always have access to the Official and Curated repos, and you can add your own Community repos.

### list repos
Lists all the sources available for loading packages. This includes the Official and Curated package listing, as well as any User repos add to the Settings.

```console 
vpm list repos
```

### add repo
Adds a local or remote repo of packages.

```console 
vpm add repo <path>
```

**Arguments**

* **path**: The path to add. It can be an absolute path to a local json file, or a url to a remote json file. If it's a local file, it must exist to be added. If it's a remote file, it must connect within 10 seconds of the request to be added.

Returns 0 if the repo was added and 1 if it was not.

### new repo
Create a new json file for a package listing.

```console 
vpm new repo [path] [--name MyName] [--author email@domain.com]
``` 

** Arguments**

* **path**: The path at which to create the file, can be absolute or relative to current directory. If not provided, it will be created in the default sources directory (~User/AppData/Local/VRChatCreatorCompanion/Sources) and given a GUID name like `4d6ffbe7-fe91-449f-ae7e-c8688e315a83.json`.

**Options**
* **-n|--name**: The name for the source, like "VRChat Official Packages" or "Momo's Messy Mix"
* **-a|--author**: An email address at which people can contact you with questions.

### remove single repo
Removes the repo from your settings by id.
Returns 0 if the repo was removed and 1 if it was not.

If the repo listing did not provide an explicit id - a url can be used in its place.

```console 
vpm remove repo [id]
```
 
### remove repos
Removes all the repos from your settings.
Returns 0 if the repos were removed and 1 if they weren't.

```console 
vpm remove repos
```

## Requirements
The VCC and VPM require a few things to be installed in order to run properly. These commands can help you quickly get your machine or a cloud build set up.

### check hub
On Windows, checks if there is a registry key for the Unity Hub at `HKEY_LOCAL_MACHINE\SOFTWARE\Classes\unityhub\DefaultIcon`.
On Mac, checks if there is a file at `/Applications/Unity Hub.app/Contents/MacOS/Unity Hub`.

```console 
vpm check hub
```

Returns 0 if it is found and 1 if it is not.

### install hub
Installs Unity Hub 3.0 for Windows

```console 
vpm install hub
```

Specifically, it downloads the hub installer from 
```console 
https://public-cdn.cloud.unity3d.com/hub/prod/UnityHubSetup.exe
``` 
and runs it with the argument `/S` to install silently.

Returns 0 if the Hub was installed and 1 if it was not.

### check unity
Checks if there is a valid installation of Unity installed at the path specified in the Settings as `pathToUnityExe`. If the Unity Hub is installed, runs the hub in a background process to list any Unity Editors using the args:
```console
-- --headless editors -i
```
Updates the Settings with the paths to the Unity Editors if found.

```console 
vpm check unity
```

Returns 0 if a compatible version of Unity is specified there and 1 if it is not.

### install unity
Installs a compatible version of the Unity Editor for Windows with Android Build Support

```console 
vpm install unity
```

Specifically, it runs the Unity Hub with these args:
```console
-- --headless install -v 2019.4.31f1 -c bd5abf232a62 -m android
``` 

returns 0 if Unity was installed and 1 if it was not.

### list unity
Lists the Unity Editors found on the current system.

```console 
vpm list unity
```

Checks:
* Windows Registry
* Unity Hub (by running it with the args `-- --headless editors -i`
* Subdirectories of the Unity Hub

## Mac and Linux Support
The only fully-supported platform at the moment is Windows 10.
However, we are working to make the vpm tool available to Mac and Linux users.

:::tip

If you're having trouble using the CLI on non-Windows platforms, you can check out our [Project Templates](/guides/using-project-template-repos) to get you started with the latest VRChat packages without relying on VCC.

:::

### Mac Setup

1. Follow the directions under [Installation & Updating](#installation--updating) above.
2. Install [Unity Hub for Mac](https://public-cdn.cloud.unity3d.com/hub/prod/UnityHubSetup.dmg) and then [Unity 2019.4.31f1](unityhub://2019.4.31f1/bd5abf232a62).
3. Open a terminal and run [vpm install templates](#install-templates) to install the latest VRChat project templates.
4. Run [vpm check hub](#check-hub) to find and save the location of Unity Hub. For now, we assume it has been installed to its default location of `/Applications/Unity Hub.app/Contents/MacOS/Unity Hub`. If this is not the case, you'll need to open your settings file and set the `pathToUnityHub` to the correct absolute path manually. Make sure to target the executable inside of the UnityHub.app as shown in the default path.
5. Run [vpm check unity](#check-unity) to find and save the location of the Unity Editor. VPM will use the Hub to find and save the path(s), so make sure VPM can find the Hub first.

That's it! You should be able to [make new projects from templates](#new), [add packages to projects](#add-package) and most other functions. You can [file a Canny](https://vrchat.canny.io/creator-companion-beta) for any methods that don't work.

### Linux Setup
The system is completely untested on Linux distributions at this point, but may work anyway due to the work done for the Mac version. The VPM will not be able to find your Unity Hub or Unity Editor paths however, so you'll need to update your settings.json file to set them manually for now.