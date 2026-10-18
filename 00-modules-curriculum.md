# WiFi Red Team Lab — Module Curriculum

Lab gear: 3 WiFi routers, 10 Android phones, 1 Mac, 1 iPad, 1 Windows laptop,
1 Linux laptop, WiFi Pineapple, ALFA AWUS036ACHM, Flipper Zero.

Rule for every module: do it manually with raw tools first (scapy / aircrack-ng /
hostapd by hand), only then repeat with the Pineapple's automated module for the
same attack. If you can't explain what the automated module did better than the
tool's own description, you're not done with that module yet.

Status key: `[ ]` not started · `[~]` in progress · `[x]` done (date + router/device
used goes in the note after it).

---

## Module 1 — See the frames (no attack)
- [ ] ALFA + Linux laptop in monitor mode, Wireshark capture of beacon / probe /
      auth / assoc / deauth / EAPOL frames from all 3 routers + an Android phone joining.
- Goal: name every frame type in a connection + 4-way handshake by sight.

## Module 2 — Recon
- [ ] `airodump-ng` / Pineapple recon module against the 3 lab routers only.
- BSSID/ESSID/channel/hidden-SSID/client-list enumeration, signal behavior.

## Module 3 — Deauth / disassoc, and why it stops working
- [ ] Manual deauth (`aireplay-ng`, or raw `scapy`) against own router + an Android phone.
- [ ] Repeat against a router with WPA3 + PMF (802.11w) enabled — confirm it fails,
      and explain why at the frame level (management frame protection).

## Module 4 — Handshake capture + offline cracking
- [ ] Capture WPA2 4-way handshake, crack with `hashcat`/`aircrack-ng` against a
      PSK you set yourself.
- [ ] Repeat against WPA3-SAE, confirm offline dictionary attack no longer applies
      the same way (PAKE vs PSK) — see `00-attack-survey-protocol-scope.md`.

## Module 5 — Rogue AP / Evil Twin / Karma
- [ ] Build by hand: `hostapd` + `dnsmasq` + captive portal, target your own Android phone.
- [ ] Repeat identical attack via Pineapple PineAP/MANA module, compare — confirm
      you can name everything it automated.

## Module 6 — Client-side targeting across OSes
- [ ] Repeat Module 5 evil twin against Android phone, iPad, Mac, Windows laptop, Linux
      laptop. Compare MAC randomization, captive-portal detection, trust prompts.

## Module 7 — MITM once associated
- [ ] `bettercap` ARP/DNS spoof inside your own rogue AP, inspect traffic. Note
      where HTTPS/HSTS blocks you — that limitation is itself the lesson.

## Module 8 — Protocol-version attacks (WPA3 doesn't mean "unattackable")
- [ ] WPA3 transition-mode downgrade: force a dual-mode SSID client down to WPA2,
      capture the partial handshake.
- [ ] Check your 3 routers' WPA3/SAE firmware against Dragonblood CVEs (group
      downgrade, timing side-channel, anti-clogging DoS) — patched or not?
- [ ] PMKID attack (`hcxdumptool`/`hcxpcapngtool`) where the router supports it.
- [ ] WPS PIN brute force (`reaver`/`bully`) on any router with WPS enabled.

## Module 9 — Enterprise auth (separate surface, if any router supports it)
- [ ] Stand up WPA2/3-Enterprise SSID (802.1X) on a router that supports it.
- [ ] Rogue RADIUS / EAP downgrade against an Android phone + the Windows laptop.

## Module 10 — Flipper Zero (separate track, mostly non-WiFi)
- [ ] Park until modules 1–9 are solid. See `devices/flipper-zero-checklist.md` —
      sub-GHz, RFID/NFC, BadUSB, IR are a different skill track, not WiFi.

---

Each module's working notes (commands run, captures saved, pass/fail) belong in a
dated session log — ask for that doc separately if you want it tracked alongside
this curriculum.

## References

- Protocol-level feasibility behind Modules 4 and 8: `00-attack-survey-protocol-scope.md`
  in this folder (Dragonblood CVEs, PMF, OWE, KRACK, WPS).
- Per-device attack lists and tool references: `devices/alfa-awus036achm-checklist.md`,
  `devices/wifi-pineapple-checklist.md`, `devices/flipper-zero-checklist.md`.
- [Aircrack-ng documentation](https://www.aircrack-ng.org/doku.php)
- [Wireshark 802.11 capture setup](https://wiki.wireshark.org/CaptureSetup/WLAN)
