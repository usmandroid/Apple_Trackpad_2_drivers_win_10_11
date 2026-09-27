Apple Magic Trackpad Version 2 (A3120) USB-C via Bluetooth Windows Precision Drivers.
---
Windows 10/11 Install

First connect as usual with USB-C or Bluetooth from Windows Settings.

Next Install drivers and finally patch update drivers.

Restart and Uninstall older drivers if run into issues or drivers don't show up.
---
Verified Steps:

https://github.com/lc700x/MagicTrackPad2_Windows_Precision_Drivers/issues/6

---
**A3120 / PID 0324 on Windows 10: release ZIP works, repo checkout INF may fail hash check, manual 'Have Disk' install is required #6**


Hi,

I’d like to share a working installation path for the newer USB-C Magic Trackpad (`A3120`, Bluetooth HID `VID 004C / PID 0324`) on `Windows 10 19045 x64`, because it may help other users.

## Device details

My device is detected as:

- Bluetooth device: `BTHENUM\DEV_80124299B479...`
- Bluetooth HID: `BTHENUM\{00001124-0000-1000-8000-00805F9B34FB}_VID&0001004C_PID&0324...`

This appears to correspond to the newer USB-C Magic Trackpad (`A3120`).

## Problem

If I use the files directly from a git checkout of this repository, importing the Bluetooth driver with `pnputil` can fail with:

```text
The hash for the file is not present in the specified catalog file.
The file is likely corrupt or the victim of tampering.
```

Also, even after the driver is preloaded into the Driver Store, Windows 10 does not automatically switch the connected Bluetooth HID device to the Apple driver for `PID 0324`.

## What worked

Using the `Release` asset ZIP worked reliably:

- `MagicTrackpad2_Precision_Drivers.zip`

After extracting the release ZIP, I could successfully add the drivers with:

```powershell
pnputil /add-driver ApplePrecisionTrackpadBluetooth\ApplePrecisionTrackpadBluetooth.inf /install
pnputil /add-driver ApplePrecisionTrackpadUSB\ApplePrecisionTrackpadUSB.inf /install
```

Then I manually changed the Bluetooth HID device in Device Manager:

1. Connect the trackpad over Bluetooth
2. Open Device Manager
3. Go to `Human Interface Devices`
4. Open the `Bluetooth HID Device` whose Hardware ID starts with:
   `BTHENUM\{00001124-0000-1000-8000-00805F9B34FB}_VID&0001004C_PID&0324`
5. `Update driver`
6. `Browse my computer for drivers`
7. `Let me pick from a list of available drivers on my computer`
8. `Have Disk`
9. Select `ApplePrecisionTrackpadBluetooth.inf` from the extracted release ZIP
10. Choose `Apple Bluetooth Precision Trackpad`

After that, the device installed successfully as:

- `Apple Bluetooth Precision Trackpad`

and Precision Touchpad features started working correctly.

## Suggestion

It may help users if the README or release notes mention that:

- for some systems, the files from a normal git checkout may not be directly installable due to catalog/hash validation
- the `Release` ZIP asset is the safer source for installation
- for `A3120 / PID 0324` on Windows 10, users may need to use:
  - `Let me pick from a list of available drivers on my computer`
  - `Have Disk`
  - and manually select `Apple Bluetooth Precision Trackpad`

Thanks for maintaining this repository.



Verified Release File:
---
Based on https://github.com/lc700x/MagicTrackPad2_Windows_Precision_Drivers/releases latest

Verfied Release 2.1 June 19th 2026

https://github.com/lc700x/MagicTrackPad2_Windows_Precision_Drivers/commit/ffbf1f1877197406d29328ed957dd46a1b58627b


https://github.com/lc700x/MagicTrackPad2_Windows_Precision_Drivers/releases/tag/2.1 

Download Drivers:

https://github.com/lc700x/MagicTrackPad2_Windows_Precision_Drivers/releases/download/2.1/ApplePrecisionTrackpad_amd64.USB-C.zip 

---





