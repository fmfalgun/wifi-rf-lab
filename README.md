# WiFi / RF Lab Notes

Personal learning lab for understanding WiFi security at the protocol level
(WPA2/WPA3, PMF, SAE, OWE) and for scoping which techniques are actually
feasible to practice against a small home lab of routers and client devices,
using a WiFi Pineapple, an ALFA AWUS036ACHM, and a Flipper Zero.

This is a study/reference repo, not a tool. Everything here is meant to be run
only against hardware you own and control. No content here targets a specific
third party, network, or device outside a personal lab setup.

## Contents

- [`00-modules-curriculum.md`](00-modules-curriculum.md) — a 10-module learning
  path, concept-first: see the raw 802.11 frames before automating anything,
  manual technique before any tool's "one-click" version of the same thing.
- [`00-attack-survey-protocol-scope.md`](00-attack-survey-protocol-scope.md) —
  what WPA3 / PMF / WiFi6E / WiFi7 actually close off vs. what survives
  regardless of protocol version, with CVE references for anything claimed.
- [`devices/`](devices) — per-device checklists (feasible techniques to learn,
  CVEs/research to check firmware against, and non-security uses), one file
  per piece of gear:
  - [`alfa-awus036achm-checklist.md`](devices/alfa-awus036achm-checklist.md)
  - [`wifi-pineapple-checklist.md`](devices/wifi-pineapple-checklist.md)
  - [`flipper-zero-checklist.md`](devices/flipper-zero-checklist.md)

## How to use this

Each list uses `- [ ]` checkboxes so you can track what's actually been done,
not just what's theoretically possible. Every CVE or technique claim links to
a primary source (paper, NVD entry, vendor doc) in that file's References
section — verify there before trusting the summary.

## Scope / ethics note

All techniques described are scoped to personal lab equipment the author owns
(routers, phones, laptops). None of this is intended for, or should be used
against, networks or devices you don't own or don't have explicit authorization
to test.
