# Windows Registry — DFIR Writeup

**Date:** 2026-04-16 **Category:** DFIR **Level:** Beginner

---

## What was this about?

Learning the basic concepts of the Windows Registry: what can I find there, and how do I find it.

---

## What did I know beforehand?

Never heard of it before. Totally new and somewhat overwhelming.

---

## What did I do?

I looked for a reliable source and hands-on practice material.

---

## What did I learn?

I first learned where to find the registry on a live system. Using the Windows key + R opens the Run prompt — typing `regedit.exe` opens the live registry. Inside you find keys and values: files are keys, and the data inside a key is the value. The registry is divided into what are called **hives** — a hive is a group of keys, subkeys, and values stored in a file on disk.

**To acquire a disk image, you need tools like:**

1. KAPE
2. Autopsy
3. FTK Imager

**For reading the data:**

1. Registry Explorer (Eric Zimmerman) — supports transaction logs
2. Registry Viewer — no transaction logs
3. RegRipper — takes hives as input and outputs a `.txt` report, available in both CLI and GUI. No transaction logs.

---

## The 5 root keys

|Root Key|Abbreviation|Contains|
|---|---|---|
|`HKEY_LOCAL_MACHINE`|HKLM|System-wide configuration — hardware, software, all users|
|`HKEY_CURRENT_USER`|HKCU|Settings of the currently logged-in user|
|`HKEY_USERS`|HKU|All user profiles on the system|
|`HKEY_CLASSES_ROOT`|HKCR|File associations (which program opens .pdf, .docx, etc.)|
|`HKEY_CURRENT_CONFIG`|HKCC|Hardware profile of the current session|

---

## The hives

|Hive|Location on disk|Contains|
|---|---|---|
|`SAM`|`C:\Windows\System32\config\SAM`|User accounts + password hashes|
|`SYSTEM`|`C:\Windows\System32\config\SYSTEM`|System configuration, hardware|
|`SOFTWARE`|`C:\Windows\System32\config\SOFTWARE`|Installed software, system settings|
|`SECURITY`|`C:\Windows\System32\config\SECURITY`|Security policy|
|`NTUSER.DAT`|`C:\Users\[username]\NTUSER.DAT`|Personal settings per user|
|`UsrClass.dat`|`C:\Users\[username]\AppData\Local\Microsoft\Windows\UsrClass.dat`|ShellBags: evidence of folders opened in Explorer — even after the folder or USB has long been removed|

---

## Key artefacts

|Artefact|Location on disk|Contains|Tool|
|---|---|---|---|
|`AmCache.hve`|`C:\Windows\AppCompat\Programs\Amcache.hve`|Executed/installed programs + **SHA1 hash** — persists even after file deletion|AmcacheParser (Zimmerman)|
|`Shimcache` _(AppCompatCache)_|`HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\AppCompatCache`|Programs that were ever executed or seen + last modification time — binary format, not directly readable|AppCompatCacheParser (Zimmerman)|
|`Prefetch`|`C:\Windows\Prefetch\` → `.pf` files _(not registry)_|Program name, **last 8 execution times**, run count, referenced files/DLLs|PECmd (Zimmerman)|

---

## Transaction logs 

Always check the `.LOG` files. They can contain information not yet committed to the hive. The relevant concepts here are **transaction log** and **write-ahead logging**. Each hive has two `.LOG` files and alternates between them.

Every 10 days, Windows creates a registry backup called the **Registry Backup**, found at: `C:\Windows\System32\Config\RegBack`

---

## Investigation order

A structured starting point for registry-based investigations:

| Step | What to check                        | What you find                             | Path                                                                                                                                                                                                                                                              |
| ---- | ------------------------------------ | ----------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1    | OS version                           | Windows version and build                 | `HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion`                                                                                                                                                                                                               |
| 2    | Current control set                  | Active hardware/system config             | `HKLM\SYSTEM\CurrentControlSet`                                                                                                                                                                                                                                   |
| 3    | Computer name                        | Hostname of the system                    | `HKLM\SYSTEM\CurrentControlSet\Control\ComputerName\ComputerName`                                                                                                                                                                                                 |
| 4    | Time zone                            | System time zone (critical for timeline)  | `HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation`                                                                                                                                                                                                       |
| 5    | Network interfaces & past networks   | IP config, known networks                 | `HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\Interfaces`                                                                                                                                                                                              |
| 6    | Autostart programs (autorun)         | Programs that run at boot/login           | `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run`                                                                                                                                                                                                              |
| 7    | SAM hive & user information          | Local accounts, last login, RID           | `HKLM\SAM\SAM\Domains\Account\Users`                                                                                                                                                                                                                              |
| 8    | Recent files                         | Last opened files per user                | `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs`                                                                                                                                                                                        |
| 9    | UserAssist                           | GUI-launched programs only — not CLI      | `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist\{GUID}\Count`                                                                                                                                                                           |
| 10   | Shimcache                            | Programs seen/executed — includes deleted | `HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\AppCompatCache`                                                                                                                                                                                            |
| 11   | USB devices/first and last time/name | Connected USB history                     | `HKLM\SYSTEM\CurrentControlSet\Enum\USBSTOR - SYSTEM\CurrentControlSet\Enum\USB - SYSTEM\CurrentControlSet\Enum\USBSTOR\Ven_Prod_Version\USBSerial#\Properties\{83da6326-97a6-4088-9453-a19231573b29}\#### - SOFTWARE\Microsoft\Windows Portable Devices\Devices` |

**Note:** If autorun shows `02x02`, a boot was initiated. **Note:** UserAssist only records GUI activity — CLI execution does not appear here. Found in `NTUSER.DAT` under a GUID key. **Note**: BAM/DAM for background activity, desktop activity moderator, programs, full paths and last run. 
**Note**: USB 
- 0064 = First connection time 
- 0066 = Last connection time
- 0067 = Last removal time

---

## Sources

- https://tryhackme.com/room/windowsforensics1
- https://learn.microsoft.com/en-us/windows/win32/sysinfo/registry-hives

---

## Next step

Practice with Registry Explorer on a live system. Next writeup: Registry Explorer practical.