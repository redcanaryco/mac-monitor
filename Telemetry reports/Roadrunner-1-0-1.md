# Red Canary Mac Monitor Telemetry Summary
## Distribution details
- Build name: `Roadrunner`
- App version: 1.0.1

## Overview
The following is an in-depth look behind the "Red Canary Security Extension" telemetry curtain. While this information is readily viewable to users at any time by exporting telemetry or selecting the "JSON" tab in any "Event Facts" window these report(s) will serve as a "snapshot" of telemetry capabilities over time.
- Total Endpoint Security (ES) events collected: 32
- Covering the following telemetry classes (abridged)
  * Process
  * Interprocess
  * File
  * File metadata
  * File system
  * Memory mapping
  * Login
  * Background Task Management (BTM)
  * XProtect

## Telemetry record structure
Each event is delivered in a record which can be modeled in JSON in the following way: 
```
{
    // Initiating process metadata (responsible for the target event)
    {
        // Target event metadata (e.g. OpenSSH login, etc)
    }
}
```

Each event has a process which was responsible for it. In terms of process execute events this is the “parent” process, for XProtect detect events it’ll be Gatekeeper (aka syspolicyd), for file creation events it’ll be the process which created the file, etc. A sample telemetry object is shown below:

```json
{
  "initiating_ruid" : 502,
  "responsible_audit_token" : "502-502-20-502-20-12327-100019-1883731",
  "initiating_is_platform_binary" : false,
  "parent_audit_token" : "502-502-20-502-20-13018-100019-1885461",
  "target" : "AppleScript",
  "initiating_process_cdhash" : "bb836a032af6a389f1a086803202fce60dd9f1b2",
  "initiating_process_file_quarantine_type" : 0,
  "macOS" : "13.2.1 (Build 22D68)",
  "sensor_id" : "bf169d19f3e7bea1b61c00db1bc9c98318007ae5f7a2b6c15e3f64f9ed5760c7cd8a49268472e75e0f916fe8acd503d9f9580a030d7d021582271813b6a3ff38",
  "initiating_process_path" : "/Users/brandondalton/.pyenv/versions/3.10.4/lib/python3.10/site-packages/posixath/tests/macos/library/T1059_002/nsapplescript_example",
  "initiating_process_name" : "nsapplescript_example",
  "initiating_euid_human" : "brandondalton",
  "initiating_ruid_human" : "brandondalton",
  "initiating_euid" : 502,
  "initiating_process_group_id" : 13018,
  "es_event_type" : "ES_EVENT_TYPE_NOTIFY_MMAP",
  "initiating_process_signing_id" : "nsapplescript_example",
  "path_is_truncated" : false,
  "audit_token" : "502-502-20-502-20-13051-100019-1885479",
  "initiating_pid" : 13018,
  "mmap_event" : {
    "path" : "/System/Library/Components/AppleScript.component/Contents/MacOS/AppleScript"
  },
  "activity_at_ts" : "2023-03-13T22:08:37.569Z"
}
```

## Endpoint Security event listing
The following ES events are supported by the Red Canary Security Extension. Users can utilize the dynamic event subscriptions feature to subscribe to any supported event.
- `ES_EVENT_TYPE_NOTIFY_EXEC`
- `ES_EVENT_TYPE_NOTIFY_FORK`
- `ES_EVENT_TYPE_NOTIFY_EXIT`
- `ES_EVENT_TYPE_NOTIFY_CREATE`
- `ES_EVENT_TYPE_NOTIFY_DELETEEXTATTR`
- `ES_EVENT_TYPE_NOTIFY_MMAP`
- `ES_EVENT_TYPE_NOTIFY_BTM_LAUNCH_ITEM_ADD`
- `ES_EVENT_TYPE_NOTIFY_BTM_LAUNCH_ITEM_REMOVE`
- `ES_EVENT_TYPE_NOTIFY_OPENSSH_LOGIN`
- `ES_EVENT_TYPE_NOTIFY_OPENSSH_LOGOUT`
- `ES_EVENT_TYPE_NOTIFY_XP_MALWARE_DETECTED`
- `ES_EVENT_TYPE_NOTIFY_XP_MALWARE_REMEDIATED`
- `ES_EVENT_TYPE_NOTIFY_MOUNT`
- `ES_EVENT_TYPE_NOTIFY_LOGIN_LOGIN`
- `ES_EVENT_TYPE_NOTIFY_LW_SESSION_LOGIN`
- `ES_EVENT_TYPE_NOTIFY_LW_SESSION_UNLOCK`
- `ES_EVENT_TYPE_NOTIFY_DUP`
- `ES_EVENT_TYPE_NOTIFY_RENAME`
- `ES_EVENT_TYPE_NOTIFY_UNLINK`
- `ES_EVENT_TYPE_NOTIFY_OPEN`
- `ES_EVENT_TYPE_NOTIFY_WRITE`
- `ES_EVENT_TYPE_NOTIFY_LINK`
- `ES_EVENT_TYPE_NOTIFY_CLOSE`
- `ES_EVENT_TYPE_NOTIFY_SIGNAL`
- `ES_EVENT_TYPE_NOTIFY_REMOTE_THREAD_CREATE`
- `ES_EVENT_TYPE_NOTIFY_IOKIT_OPEN`
- `ES_EVENT_TYPE_NOTIFY_CS_INVALIDATED`
- `ES_EVENT_TYPE_NOTIFY_SETEXTATTR`
- `ES_EVENT_TYPE_NOTIFY_PROC_SUSPEND_RESUME`
- `ES_EVENT_TYPE_NOTIFY_TRACE`
- `ES_EVENT_TYPE_NOTIFY_GET_TASK`
- `ES_EVENT_TYPE_NOTIFY_PROC_CHECK`


## Initiating process metadata
Each component of our initiating process structure is listed below along with its type. Types which are suffixed with a question mark are optional. This means that any given telemetry object can have any given event we have modeled.
- `audit_token: String`
- `es_event_type: String`
- `initiating_pid: Int32`
- `initiating_process_name: String`
- `initiating_process_signing_id: String`
- `initiating_process_path: String`
- `initiating_ruid: Int64`
- `initiating_euid: Int64`
- `initiating_ruid_human: String`
- `initiating_euid_human: String`
- `initiating_process_cdhash: String`
- `parent_audit_token: String`
- `path_is_truncated: Bool`
- `responsible_audit_token: String`
- `macOS: String`
- `sensor_id: String`
- `activity_at_ts: String`
- `initiating_process_file_quarantine_type: Int16`
    - We attempt to read the app’s bundled property list for this information
      - `0`: The process is not File Quarantine-aware
      - `1`: The process has opted-into File Quarantine
      - `2`: The process has been forced into File Quarantine
- `initiating_process_group_id: Int32`
- `initiating_is_platform_binary: Bool`
- `btm_launch_item_add_event: RCESLaunchItemAddEvent?`
- `delete_xattr_event: RCESXattrEvent?`
- `set_xattr_event: RCESXattrSetEvent?`
- `exec_event: RCESProcessExecEvent?`
- `code_signature_invalidated_event: RCESCodeSignatureInvalidatedEvent?`
- `process_socket_event: RCESProcessSocketEvent?`
- `process_trace_event: RCESProcessTraceEvent?`
- `get_task_event: RCESGetTaskEvent?`
- `process_check_event: RCESProcessCheckEvent?`
- `process_signal_event: RCESProcessSignalEvent?`
- `remote_thread_create_event: RCESRemoteThreadCreateEvent?`
- `exit_event: RCESProcessExitEvent?`
- `file_event: RCESFileEvent?`
- `fork_event: RCESProcessForkEvent?`
- `mmap_event: RCESMMapEvent?`
- `btm_launch_item_remove_event: RCESLaunchItemRemoveEvent?`
- `openssh_login_event: RCESOpenSSHLoginEvent?`
- `openssh_logout_event: RCESOpenSSHLogoutEvent?`
- `xprotect_detect_event: RCESXProtectDetect?`
- `xprotect_remediate_event: RCESXProtectRemediate?`
- `mount_event: RCESMountEvent?`
- `login_login_event: RCESLoginLoginEvent?`
- `lw_login_event: RCESLWLoginEvent?`
- `lw_unlock_event: RCESLWUnlockEvent?`
- `fd_duplicate_event: RCESFDDuplicateEvent?`
- `file_rename_event: RCESFileRenameEvent?`
- `file_delete_event: RCESFileDeleteEvent?`
- `file_open_event: RCESFileOpenEvent?`
- `file_write_event: RCESFileWriteEvent?`
- `link_event: RCESLinkEvent?`
- `file_close_event: RCESFileCloseEvent?`
- `iokit_open_event: RCESIOKitOpenEvent?`


## Process execute target event metadata (`exec_event`): `ES_EVENT_TYPE_NOTIFY_EXEC`
- `allow_jit: Bool`
- `audit_token: String`
- `command_line: String`
- `get_task_allow: Bool`
- `pid: Int32`
- `is_adhoc_signed: Bool`
- `is_es_client: Bool`
- `is_platform_binary: Bool`
- `parent_audit_token: String`
- `process_name: String`
- `process_path: String`
- `ruid: Int64`
- `euid: Int64`
- `ruid_human: String`
- `euid_human: String`
- `responsible_audit_token: String`
- `rootless: Bool`
- `signing_id: String`
- `cdhash: String`
- `skip_lv: Bool`
- `team_id: String?`
- `start_time: String`
- `certificate_chain: String?`
- `env_variables: String`
- `file_quarantine_type: Int16`
  - We attempt to read the app’s bundled property list for this information
    - `0`: The process is not File Quarantine-aware
    - `1`: The process has opted-into File Quarantine
    - `2`: The process has been forced into File Quarantine
- `cs_type: String`
- `group_id: Int32`


## Process fork target event metadata (`fork_event`): `ES_EVENT_TYPE_NOTIFY_FORK`
- `audit_token: String`
- `pid: Int32`
- `ruid: Int64`
- `euid: Int64`
- `ruid_human: String`
- `euid_human: String`
- `parent_audit_token: String`
- `process_name: String`
- `process_path: String`
- `responsible_audit_token: String`
- `signing_id: String`
- `cdhash: String`
- `start_time: String`
- `group_id: Int32`
- `is_platform_binary: Bool`


## Process code signature invalidated target event metadata (`code_signature_invalidated_event`): `ES_EVENT_TYPE_NOTIFY_CS_INVALIDATED`
- Note: This target event specifies that the initiating process's code signature was invalidated in-memory.


## Process socket target event metadata (`process_socket_event`): `ES_EVENT_TYPE_NOTIFY_PROC_SUSPEND_RESUME`
- `target_process_name: String`
- `target_process_path: String`
- `target_process_signing_id: String`
- `target_process_audit_token: String`
- `type: String`


## Process trace target event metadata (`process_trace_event`): `ES_EVENT_TYPE_NOTIFY_TRACE`
- `process_name: String`
- `process_path: String`
- `process_signing_id: String`
- `process_audit_token: String`


## Process task port target event (`get_task_event`): `ES_EVENT_TYPE_NOTIFY_GET_TASK`
- `process_path: String`
- `process_name: String`
- `process_audit_token: String`
- `process_signing_id: String`
- `type: String`


## Process check target event metadata (`process_check_event`): `ES_EVENT_TYPE_NOTIFY_PROC_CHECK`
- `process_name: String`
- `process_signing_id: String`
- `process_path: String`
- `process_audit_token: String`
- `flavor: Int32`
- `type: String`


## Process signal target event metadata (`process_signal_event`): `ES_EVENT_TYPE_NOTIFY_SIGNAL`
- `signal_id: Int32`
- `process_name: String`
- `process_path: String`
- `audit_token: String`
- `signing_id: String`
- `signal_name: String`


## Process remote thread created target event metadata (`remote_thread_create_event`): `ES_EVENT_TYPE_NOTIFY_REMOTE_THREAD_CREATE`
- `target_process_name: String`
- `target_process_path: String`
- `target_process_signing_id: String`
- `target_process_audit_token: String`
- `thread_state: String`


## Process exit target event metadata (`exit_event`): `ES_EVENT_TYPE_NOTIFY_EXIT`
- `exit_code: Int32`


## File creation target event metadata (`file_event`): `ES_EVENT_TYPE_NOTIFY_CREATE`
- `destination_path: String`
- `file_name: String`
- `is_quarantined: Int16`
    - We attempt to determine if the file being created is quarantined. If a file is deleted / delete `xattr` event occurs too too quickly the file cannot be found.
      - `0`: The file is not quarantined
      - `1`: The file is quarantined
      - `2`: The file could not be found


## File rename target event metadata (`file_rename_event`): `ES_EVENT_TYPE_NOTIFY_RENAME`
- `file_name: String`
- `destination_path: String`
- `source_path: String`
- `archive_files_not_quarantined: String?`
    - If this file rename event is moving an inflated archive we perform a deep search of the destination file path to determine if any files are not quarantined.
- `type: String`
- `is_quarantined: Int16`
    - We attempt to determine if the file being created is quarantined. If a file is deleted / delete `xattr` event occurs too too quickly the file cannot be found.
      - `0`: The file is not quarantined
      - `1`: The file is quarantined
      - `2`: The file could not be found


## File system mount target event metadata (`mount_event`): `ES_EVENT_TYPE_NOTIFY_MOUNT`
- `total_files: Int64`
- `mount_flags: Int64`
- `type_name: String`
- `source_name: String`
- `mount_directory: String`
- `owner_uid: Int64`
- `fs_id: String`
- `owner_uid_human: String`


## File duplicate target event metadata (`fd_duplicate_event`): `ES_EVENT_TYPE_NOTIFY_DUP`
- `file_path: String`
- `file_name: String`


## Extended attribute (xattr) delete target event metadata (`delete_xattr_event`): `ES_EVENT_TYPE_NOTIFY_DELETEEXTATTR`
- `file_name: String`
- `file_path: String`
- `operation: String`
- `xattr: String`


## Extended attribute (xattr) set target event metadata (`set_xattr_event`): `ES_EVENT_TYPE_AUTH_SETEXTATTR`
- `file_name: String`
- `file_path: String`
- `operation: String`
- `xattr: String`

## Background Task Management (BTM) add target event metadata (`btm_launch_item_add_event`): `ES_EVENT_TYPE_NOTIFY_BTM_LAUNCH_ITEM_ADD`
- `file_name: String`
- `file_path: String`
- `uid: Int64`
- `uid_human: String`
- `is_legacy: Bool`
- `is_managed: Bool`
- `type: String`
- `plist_contents: String`
    - We pull the legacy property list for the BTM item added if the property list is not in the Apple Binary Property List
- `app_process_path: String`
- `app_process_signing_id: String`
- `app_process_team_id: String`
- `instigating_process_path: String`
- `instigating_process_signing_id: String`
- `instigating_process_team_id: String?`


## Background Task Management (BTM) remove target event metadata (`btm_launch_item_remove_event`): `ES_EVENT_TYPE_NOTIFY_BTM_LAUNCH_ITEM_REMOVE`
- `app_process_path: String?`
- `app_process_signing_id: String?`
- `app_process_team_id: String?`
- `instigating_process_path: String?`
- `instigating_process_signing_id: String?`
- `instigating_process_team_id: String?`
- `file_path: String?`
- `file_name: String?`
- `is_legacy: Bool`
- `type: String?`
- `uid: Int64`
- `uid_human: String?`
- `is_managed: Bool`


## Memory map target event metadata (`mmap_event`): `ES_EVENT_TYPE_NOTIFY_MMAP`
- `path: String`


## LoginWindow login target event metadata (`lw_login_event`): `ES_EVENT_TYPE_NOTIFY_LW_SESSION_LOGIN`
- `username: String`
- `graphical_session_id: Int32`


## LoginWindow unlock target event metadata (`lw_unlock_event`): `ES_EVENT_TYPE_NOTIFY_LW_SESSION_UNLOCK`
- `username: String`
- `graphical_session_id: Int32`


## Login login target event metadata (`login_login_event`): `ES_EVENT_TYPE_NOTIFY_LOGIN_LOGIN`
- `success: Bool`
- `failure_message: String`
- `username: String`
- `uid: Int64`
- `uid_human: String`


## OpenSSH login target event metadata (`openssh_login_event`): `ES_EVENT_TYPE_NOTIFY_OPENSSH_LOGIN`
- `result_type: String?`
- `source_address: String?`
- `source_address_type: String?`
- `success: Bool`
- `user_name: String?`


## OpenSSH logout target event metadata (`openssh_logout_event`): `ES_EVENT_TYPE_NOTIFY_OPENSSH_LOGOUT`
- `source_address_type: String`
- `source_address: String`
- `username: String`


## XProtect Malware detected target event metadata (`xprotect_detect_event`): `ES_EVENT_TYPE_NOTIFY_XP_MALWARE_DETECTED`
- `signature_version: String`
- `malware_identifier: String`
- `incident_identifier: String`
- `detected_path: String`


## XProtect Malware remediated target event metadata (`xprotect_remediate_event`): `ES_EVENT_TYPE_NOTIFY_XP_MALWARE_REMEDIATED`
- `signature_version: String`
- `malware_identifier: String`
- `incident_identifier: String`
- `action_type: String`
- `success: Bool`
- `result_description: String`
- `remediated_path: String`
- `remediated_process_audit_token: String`


## File delete target event metadata (`file_delete_event`): `ES_EVENT_TYPE_NOTIFY_UNLINK`
- `file_path: String`
- `file_name: String`
- `parent_directory: String`


## File open target event metadata (`file_open_event`): `ES_EVENT_TYPE_NOTIFY_OPEN`
- `file_path: String`
- `file_name: String`


## File write target event metadata (`file_write_event`): `ES_EVENT_TYPE_NOTIFY_WRITE`
- `file_path: String`
- `file_name: String`


## File link target event metadata (`link_event`): `ES_EVENT_TYPE_NOTIFY_LINK`
- `source_file_path: String`
- `source_file_name: String`
- `target_file_path: String`
- `target_file_name: String`


## File close target event metadata (`file_close_event`): `ES_EVENT_TYPE_NOTIFY_CLOSE`
- `file_path: String`
- `file_name: String`


## IOKit open target event metadata (`iokit_open_event`): `ES_EVENT_TYPE_NOTIFY_IOKIT_OPEN`
- `user_client_class: String`
- `user_client_type: Int32`

