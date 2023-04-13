## Welcome to Red Canary Mac Monitor
![Feature overview](https://github.com/redcanaryco/mac-monitor/blob/First-Release-Roadrunner-Build/Resources/FeatureSummary.png?raw=true)

Red Canary Mac Monitor is an advanced, stand-alone system monitoring tool tailor-made for macOS security research, malware triage, and system troubleshooting. Harnessing Apple Endpoint Security (ES), it collects and enriches system events, displaying them graphically, with an expansive feature set designed to surface only the events that are relevant to you. The telemetry collected includes process, interprocess, and file events in addition to rich metadata, allowing users to contextualize events and tell a story with ease. With an intuitive interface and a rich set of analysis features, Red Canary Mac Monitor was designed for a wide range of skill levels and backgrounds to detect macOS threats that would otherwise go unnoticed. As part of Red Canary’s commitment to the research community, the Mac Monitor distribution package is available to download for free.

## How can I install this thing?
* Go to the releases section and download the latest installer: https://github.com/redcanaryco/mac-monitor/releases
* Open the app: `Red Canary Mac Monitor.app`
* You'll be prompted to "Open System Settings" to "Allow" the System Extension.
* Next, System Settings will automaticlly open to `Full Disk Access` -- you'll need to flip the switch to enable this for the `Red Canary Security Extension`. Full Disk Access is a *requirement* of Endpoint Secuirty.
* 🏎️ Click the "Start" button in the app and you'll be propted to reopen the app. Done!

![Install process](https://github.com/redcanaryco/mac-monitor/blob/First-Release-Roadrunner-Build/Resources/Install.png?raw=true)


## How are updates handled?
* When a new version is avalible for you to download we'll make a new release.
* We'll include updated notes and telemetry summaries (if applicable) for each release
* All you, as the end user, will need to do is download the update and run the installer. We'll take care of the rest 😉.


## How to use this repository
Here we'll be hosting:
* The distribution package for easy install. See the [`Releases` section](https://github.com/redcanaryco/mac-monitor/releases/). Each major build corresponds to a code name. The first of these builds is `GoldCardinal`.
* Release notes `/Release notes`
* Updated mute set summaries in `/Mute sets`
* and telemetry reports in `/Telemetry reports` (i.e. all the artifacts that can be collected by the Securty Extension).

Additionally, you can submit feature requests and bug reports here as well. When creating a new Issue you'll be able to use one of the two provided templates.


## How are releases structured?
Each release of Red Canary Mac Monitor has a corresponding build name and version number. The first release has the build name of: `GoldCardinal` and version number `1.0.1`.


## What are some standout features?
- High fidelity ES events modeled and enriched with some events containing further enrichment. For example, a process being File Quarantine-aware, a file being quarantined, code signing certificates, etc.
- Dynamic ES event subscriptions at runtime. You have the ability to on-the-fly modify your event subscriptions -- enabling you to cut down on noise while you're working through traces.
- Very detailed event facts -- for each event we display as much information as pssible in the UI. Each event has a curated set of data it represents.
- Event correlation is an *exceptionally* important component in any analyst's toolbelt. The ability to see which events are "related" to one-another enables you to manipulate the telemetry in a way that makes sense (other than simply dumping to JSON or representing an individual event). We perform event correlation at the process level -- this means that for any given event (which have an initiating and/or target process) we can deeply link events that any given process instigated. 
- Process grouping is another helpful way to represent process telemetry around a given `ES_EVENT_TYPE_NOTIFY_EXEC` or `ES_EVENT_TYPE_NOTIFY_FORK` event. By grouping processes in this way you can easily identify the chain of activity.
- Path muting at the API level -- Apple's Endpoint Security team has put a lot of work recently into enabling advanced path muting / inversion capabilities. Here, we cover the majority of the API features: `es_mute_path` and `es_mute_path_events` along with the types of `ES_MUTE_PATH_TYPE_PREFIX`, `ES_MUTE_PATH_TYPE_LITERAL`, `ES_MUTE_PATH_TYPE_TARGET_PREFIX`, and `ES_MUTE_PATH_TYPE_TARGET_LITERAL`. Right now we do not support inversion. I'd love it if the ES team added inversion on a per-event basis instead of per-client.
- Artifact filtering enabled users to remove (but not destroy) events from view based on: event type, initating process path, or target process path. This standout feature enables analysts to cut through the noise quickly while still rataining all data.
  - Destructive filtering is also avalible in the form of "dropping platform binaries" -- another useful technqiue to cut through the noise.
- Telemetry export. Right now we support pretty JSON and JSONL (one JSON object per-line) for the full or partial system trace (keyboard shortcuts too).
- Dynamic event distribution chart. This is another fun one enabled by the SwiftUI team. The graph shows the distribution of events you're subscribed to, currently in-scope (i.e. not filtered), and have a count of more than nothing. This enables you to *very* quickly identy noisy events. The chart auto-shows/hides itself, but you can bring it back with the: "Mini-chart" button in the toolbar.
- 
