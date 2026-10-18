# Device Checklist — Flipper Zero

Mostly **not** a WiFi tool — park this until the modules in
`00-modules-curriculum.md` are solid. It touches sub-GHz, RFID/NFC, IR, BadUSB,
GPIO, and WiFi only via an add-on dev board (ESP32-based). Treat it as a
separate skill track, not part of the WiFi curriculum.

Status key: `[ ]` not tried · `[~]` partial · `[x]` done (add date + target item
you tested, e.g. "own garage remote", "own NFC badge").

## Feasible to learn/verify, on your own devices only

- [ ] Sub-GHz capture/replay against your own remote (garage/gate opener you own)
      — fixed-code vs rolling-code, and why rolling code resists simple replay
- [ ] RFID/NFC read of your own access cards/badges — identify Mifare Classic vs
      more modern/encrypted tag types
- [ ] NFC clone/emulate test against a tag you own, to see which tag classes
      are actually clonable with stock firmware
- [ ] IR universal-remote capture/replay against your own devices
- [ ] BadUSB scripting (DuckyScript) against a VM or a lab laptop you control,
      to understand HID-injection as a delivery mechanism
- [ ] iButton read/clone against a tag you own
- [ ] GPIO/UART use as a general electronics debug tool (unrelated to attacks)
- [ ] WiFi add-on board (if you get one): deauth/PCAP/evil-portal firmware
      (e.g. Marauder-style) — compare against the ALFA's manual equivalents

## Known issues / research worth reading, not device CVEs as such

- BLE advertising "spam" affecting iOS/Android/Windows notification popups —
  not a Flipper-specific vulnerability, it's a design gap in how those OSes
  handle unauthenticated BLE advertisements; Apple shipped mitigations in
  iOS 17.2. Worth reading as a case study in platform-level BLE trust, not as
  something to script. [Background coverage, Bleeping Computer](https://www.bleepingcomputer.com/news/apple/apple-patches-flipper-zero-bluetooth-crash-attacks-in-ios-172/)
- Rolling-code sub-GHz vulnerabilities (e.g. older car/garage remotes) are
  implementation-specific per manufacturer, not a single CVE — check your own
  remote's chipset/protocol before assuming any result transfers.

## Non-security / other uses for this device

- [ ] Universal remote consolidation for your own IR devices
- [ ] NFC-based access-control testing for your own badges before deployment
- [ ] GPIO prototyping companion for small electronics projects
- [ ] iButton/NFC asset tagging experiments

## References for verification

- [Official Flipper Zero documentation](https://docs.flipper.net/)
- [Flipper Zero firmware source, official](https://github.com/flipperdevices/flipperzero-firmware)
- [RFID/NFC background, Proxmark wiki (cross-reference for tag classes)](https://github.com/RfidResearchGroup/proxmark3/wiki)
