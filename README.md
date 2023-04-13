## Welcome to Red Canary Event Monitor for Mac
Red Canary Mac Monitor is an advanced, stand-alone system monitoring tool tailor-made for macOS security research. Beginning with Endpoint Security (ES), it collects and enriches system events, displaying them graphically, with an expansive feature set designed to reduce noise. The telemetry collected includes process, interprocess, file, file metadata, file system, code signing, and more. Red Canary Mac Monitor includes several core enhancements, such as a graphical event viewer full of deep-linked events, event correlation, dynamic event subscriptions, path muting, artifact filtering, telemetry export, and rich iconography. This core feature set makes it an ideal analysis companion for validating suspicions or conducting macOS behavioral malware analysis.

## How can I install this thing?
* Go to the releases section and download the latest installer: https://github.com/redcanaryco/mac-monitor/releases/tag/v1.0.1
* Open the app: `Red Canary Mac Monitor.app`
* You'll be prompted to "Open System Settings" to "Allow" the System Extension.
* Next, System Settings will automaticlly open to `Full Disk Access` -- you'll need to flip the switch to enable this for the `Red Canary Security Extension`. Full Disk Access is a *requirement* of Endpoint Secuirty.
* 🏎️ Click the "Start" button in the app and you'll be propted to reopen the app. Done!

![Install process](https://github.com/redcanaryco/mac-monitor/blob/main/Resources/Install.png?raw=true)


## How are updates handled?
* When a new version is avalible for you to download we'll make a new release.
* We'll include updated notes and telemetry summaries (if applicable) for each release
* All you, as the end user, will need to do is download the update and run the installer. We'll take care of the rest 😉.


## How to use this repository
Here we'll be hosting:
* The distribution package for easy install. See the `Releases` section. Each major build corresponds to a code name. The first of these builds is `roadrunner`.
* Release notes `/Release notes`
* 
* and telemetry reports in `/Telemetry reports` (i.e. all the artifacts that can be collected by the Securty Extension).

Additionally, you can submit feature requests and bug reports here as well. When creating a new Issue you'll be able to use one of the two provided templates.


## How are releases structured?
Each release of Red Canary Mac Monitor has a corresponding major and minor build version associated. Distribution packages are named like: `Red-Canary-Mac-Monitor-Roadrunner-V2.pkg`. This means that the major version corresponds to the `Roadrunner` release and `V2` corresonds to the version of the build. The final build reads as: "Red Canary Event Monitor for Mac Roadrunner release version 2".

