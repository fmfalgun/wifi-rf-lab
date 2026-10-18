# Device Checklist — WiFi Pineapple

Hak5 platform built around `hostapd`/`dnsmasq` + a module marketplace + web UI.
Use this **after** you've done the same technique by hand with the ALFA, so the
Pineapple's modules stay explainable rather than magic.

Status key: `[ ]` not tried · `[~]` partial · `[x]` done (add date + router/client).

## Feasible to learn/verify on this device

- [ ] Recon module (PineAP) against the 3 lab routers — compare output to manual
      `airodump-ng` from the ALFA checklist
- [ ] PineAP / MANA rogue-AP and Karma-style association against an Android phone, iPad,
      Mac, Windows laptop, Linux laptop — compare OS behavior per device
- [ ] Captive-portal module against your own rogue AP
- [ ] Deauth module — compare behavior against PMF vs non-PMF router, same as
      the manual test in the ALFA checklist
- [ ] PMKID harvesting module where supported
- [ ] Loot/reporting module — treat as evidence logging, not just automation
- [ ] Cloud C2 feature (if your unit has it) for staged, multi-session testing

## CVEs & advisories to check against your unit's firmware

- Check Hak5's own changelog/advisories for your specific Pineapple model and
  firmware version before relying on any module — vulnerabilities in the
  management web UI itself have been reported in older firmware releases.
  [Hak5 WiFi Pineapple docs](https://docs.hak5.org/wifi-pineapple)
- Underlying techniques inherit the same protocol-level references as the ALFA
  checklist (Dragonblood, KRACK, WPS) — see `alfa-awus036achm-checklist.md`.

## Non-security / other uses for this device

- [ ] Portable travel AP / network diagnostics tool (it's a full Linux box with
      a web UI — usable for general WiFi troubleshooting, not just offense)
- [ ] Classroom/demo tool for teaching evil-twin concepts visually via its UI
- [ ] Network forensics practice: use its logging/loot features to build an
      incident-response style report of your own staged scenario

## References for verification

- [Hak5 WiFi Pineapple documentation](https://docs.hak5.org/wifi-pineapple)
- [Hak5 community forums / module index](https://forums.hak5.org/)
- Cross-reference any module's underlying technique against
  `00-attack-survey-protocol-scope.md` in this folder before assuming it still
  works on a WPA3/PMF-enabled router.
