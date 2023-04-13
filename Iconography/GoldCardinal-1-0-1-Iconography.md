# **Event Iconography**
## **Distribution details**
- Build name: `GoldCardinal`
- App version: `1.0.1`

## **Overview**
Utilizing **[SF Symbols](https://developer.apple.com/sf-symbols/)** we've assigned each ES event a symbol and colors which correspond to facts about any given event.

## **Color summary**
* `Blue`: Login of some kind (e.g. login window unlock)
* `Orange`: Generally speaking, a low volume "security relevant" event (e.g. background tasks being added)
* `Red`: Something to potentially look into. For example, `com.apple.quarantine` extended attribute deletion -- [generally not a problem on its own](https://redcanary.com/blog/gatekeeper/).
* `Purple`: Something you should *definitely* look at. Some heuristics developed include [Gatekeeper bypass](https://redcanary.com/threat-detection-report/techniques/gatekeeper-bypass/#:~:text=creating%20this%20file-,Detection%20opportunities,-While%20it%20might) at the File Quarantine level. XProtect detection events are also colored purple.
* `Green`: A remediation action / setting a security policy occurred -- right now just XProtect Remediator / setting the quarantine flag.

## **Event breakdown detailed**
Please note. In most cases, we've included "help" / "tooltip" text for each symbol which you can see by hovering the cursor over any given symbol. 

## **Process events**
### `ES_EVENT_TYPE_NOTIFY_EXEC`
- **Event symbol: "checkmark.seal"** or
- **event symbol: "xmark.seal"**

- **Code signing**
    - **Event symbol: "checkmark.seal"** represents `process_exec` events with a valid code signature (and not adhoc).
    - If the process is adhoc signed the event will be colored in `orange` with the **event symbol: "xmark.seal"** and a `yellow` "exclamationmark.triangle.fill" symbol proceeding it.
    - If the process is not signed at all it will be colored in `red` with the **event symbol: "xmark.seal"** and a `red` "exclamationmark.triangle.fill" symbol proceeding it.

- **Dylib injection**
    - If we've observed this target process having `dyld_insert_libraries` in its environment variables we'll prefix the event symbol with a: "bookmark.slash".

- **File Quarantine-aware processes**
    - If we've identified that this process is "File Quarantine-aware" then we'll prefix the event symbol with a: "lock.icloud". 

### `ES_EVENT_TYPE_NOTIFY_FORK`
- **Event symbol: "point.topleft.down.curvedto.point.bottomright.up".**

### `ES_EVENT_TYPE_NOTIFY_SIGNAL`
- **Event symbol: "dot.radiowaves.forward".**

### `ES_EVENT_TYPE_NOTIFY_PROC_SUSPEND_RESUME`
- **Event symbol: "autostartstop.trianglebadge.exclamationmark".**

### `ES_EVENT_TYPE_NOTIFY_CS_INVALIDATED`
- **Event symbol: "signature"** and we'll color this event `red` / prefix the event symbol with a `yellow`: "exclamationmark.triangle.

### `ES_EVENT_TYPE_NOTIFY_REMOTE_THREAD_CREATE`
- **Event symbol: bolt.horizontal.fill"** and we'll color this event `red` / prefix the event symbol with a `yellow`: "exclamationmark.triangle.fill" symbol.

### `ES_EVENT_TYPE_NOTIFY_TRACE`
- **Event symbol: "stethoscope"** and we'll color this event `orange`.

### `ES_EVENT_TYPE_NOTIFY_GET_TASK`
- **Event symbol: "creditcard.trianglebadge.exclamationmark"** and we'll color this event `orange`.

### `ES_EVENT_TYPE_NOTIFY_PROC_CHECK`
- **Event symbol: "barcode.viewfinder".**

### `ES_EVENT_TYPE_NOTIFY_EXIT`
- **Event symbol: "eject.fill".**

- **Non-zero exit codes**
    - If this event is representing a non-zero exit code then we'll prefix the event symbol with an: "info.square".



## **Memory events**
### `ES_EVENT_TYPE_NOTIFY_MMAP`
- **Event symbol: "memorychip".**

- **OSA (Open Scripting Architecture)**
    - If this event is mapping an OSA component into memory then we'll add a `yellow`: "exclamationmark.triangle.fill" symbol proceeding it.



## **File events**
### `ES_EVENT_TYPE_NOTIFY_CREATE`
- **Event symbol: "doc.plaintext".**

- **File Quarantine**
    - If we've identified a potential "File Quarantine violation" (see our Gatekeeper blogs) we'll color the event `red` (unquarantined file downloaded by a File Quarantine-aware app).
    - Additionally, if the file was found on disk to be quarantined we'll prefix the event symbol with: "lock.shield".

### `ES_EVENT_TYPE_NOTIFY_DUP`
- **Event symbol: "folder.badge.plus".**

### `ES_EVENT_TYPE_NOTIFY_RENAME`
- **Event symbol: filemenu.and.cursorarrow".**

- **File Quarantine**
    - If we've identified a potential "File Quarantine violation" (see our [Gatekeeper bypass](https://redcanary.com/threat-detection-report/techniques/gatekeeper-bypass/#:~:text=creating%20this%20file-,Detection%20opportunities,-While%20it%20might) blogs) we'll color the event:
        - `purple`: As the result of a deep search on an inflated archive by `Archive Utility.app` we found that a file was not quarantined, but its parent directory was. The quarantine flag should *always* propagate. **This heuristic should be high fidelity.** Additionally, we'll prefix the event symbol with: "bolt.trianglebadge.exclamationmark.fill".
        - `red`: We noticed that an app bundle was unarchived with `Archive Utility.app` and it's not quarantined, but, on the surface we have no way to tell "which" process ordered the unarchive operation. This means that **false positives are more likely** due to the missing "File Quarantine-aware" artifact. Additionally, we'll prefix the event symbol with: "hand.raised.app".

### `ES_EVENT_TYPE_NOTIFY_UNLINK`
- **Event symbol: "trash".**

### `ES_EVENT_TYPE_NOTIFY_OPEN`
- **Event symbol: "envelope.open.fill".**

### `ES_EVENT_TYPE_NOTIFY_WRITE`
- **Event symbol: "square.and.pencil".**

### `ES_EVENT_TYPE_NOTIFY_LINK`
- **Event symbol: "link.badge.plus".**

### `ES_EVENT_TYPE_NOTIFY_CLOSE`
- **Event symbol: "xmark.square".**



## **File metadata events**
### `ES_EVENT_TYPE_NOTIFY_DELETEEXTATTR`
- **Event symbol: "delete.backward.fill".**

- **File Quarantine**
    - If this event is deleting the quarantine flag then we'll color this event `red`.

### `ES_EVENT_TYPE_NOTIFY_SETEXTATTR`
- **Event symbol: "filemenu.and.selection".**

- **File Quarantine**
    - If this event is setting the quarantine flag then we'll color this event `green`.



## **File system events**
### `ES_EVENT_TYPE_NOTIFY_MOUNT`
- **Event symbol: "mount".**



## **Background Task events**
### `ES_EVENT_TYPE_NOTIFY_BTM_LAUNCH_ITEM_ADD`
- **Event symbol: "lock.doc"** and we'll color this event `orange` / prefix the event symbol with a `yellow`: "exclamationmark.triangle.fill" symbol.

### `ES_EVENT_TYPE_NOTIFY_BTM_LAUNCH_ITEM_REMOVE`
- **Event symbol: "lock.doc"** and we'll color this event `orange` / prefix the event symbol with a `yellow`: "exclamationmark.triangle.fill" symbol.



## **Login events**
### `ES_EVENT_TYPE_NOTIFY_OPENSSH_LOGIN`
- **Event symbol: "network"** and we'll color this event `blue`

### `ES_EVENT_TYPE_NOTIFY_OPENSSH_LOGOUT`
- **Event symbol: "network"** and we'll color this event `blue`

### `ES_EVENT_TYPE_NOTIFY_LOGIN_LOGIN`
- **Event symbol: "person.fill.checkmark".**

### `ES_EVENT_TYPE_NOTIFY_LW_SESSION_LOGIN`
- **Event symbol: "macwindow.badge.plus".**

### `ES_EVENT_TYPE_NOTIFY_LW_SESSION_UNLOCK`
- **Event symbol: "lock.open".**



## **XProtect events**
### `ES_EVENT_TYPE_NOTIFY_XP_MALWARE_DETECTED`
- **Event symbol: "bolt.shield"** and we'll color this event `purple`

### `ES_EVENT_TYPE_NOTIFY_XP_MALWARE_REMEDIATED`
- **Event symbol: "checkmark.shield"** and we'll color this event `green`



## **Kernel events**
### `ES_EVENT_TYPE_NOTIFY_IOKIT_OPEN`
- **Event symbol: "captions.bubble".**


![Event iconography](https://github.com/redcanaryco/mac-monitor/blob/main/Resources/GoldCardinal-1-0-1-event-iconography.png?raw=true)