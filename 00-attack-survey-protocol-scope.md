# Attack Feasibility Survey — WPA2/WPA3 / WiFi 4–7, for this lab

What changes at each protocol generation, what that closes off, and what survives
it regardless of version. Use this to decide which module is still worth your time
against which of the 3 lab routers.

## What WPA3 / PMF / WiFi6E / WiFi7 actually close off

- **PMF (Protected Management Frames)** — mandatory on WiFi6E/7, optional on
  WPA3/WPA2: encrypts/authenticates deauth & disassoc frames. This is why plain
  `aireplay-ng --deauth` already failed against a WPA3 router in earlier testing —
  confirmed real finding, not a config fluke.
- **SAE (Dragonfly handshake)** replaces the WPA2 4-way PSK exchange with a PAKE,
  so offline dictionary cracking of a captured handshake doesn't apply the same way.
- **Enhanced Open (OWE)** replaces "open" networks with opportunistic encryption —
  defeats passive sniffing on open APs, but does **not** authenticate the AP (gap
  noted below).
- **WiFi6E/7 at 6 GHz**: WPA3 + PMF + OWE are mandatory for certification, no WPA2
  fallback at all in that band. If any lab router supports 6 GHz, that band is a
  genuinely harder target than 2.4/5 GHz on the same router.

## What still works — this is the real Module 8+ scope

1. **Dragonblood-class attacks on SAE itself** (Vanhoef & Ronen, USENIX Security
   2019) — not fixed by "turning on WPA3," only by patched firmware:
   - WPA3 transition-mode downgrade to WPA2, partial handshake leaks enough for
     a dictionary attack.
   - SAE group-negotiation downgrade to a weak elliptic curve/group.
   - Timing + cache side-channels enabling password partitioning.
   - CPU-exhaustion DoS bypassing the anti-clogging defense.
   - CVEs: **CVE-2019-9494 / 9495 / 9496 / 9497 / 9498 / 9499**.
   - [Dragonblood paper (Vanhoef & Ronen)](https://papers.mathyvanhoef.com/dragonblood.pdf)
   - [Black Hat 2019 whitepaper](https://i.blackhat.com/USA-19/Wednesday/us-19-Vanhoef-Dragonblood-Attacking-The-Dragonfly-Handshake-Of-WPA3-wp.pdf)
   - **Action**: check each of the 3 routers' WPA3 firmware against these — patched
     or not. Directly checkable, not theoretical.
2. **WPA3 transition-mode downgrade** — if a router runs WPA2+WPA3 mixed mode
   (common default for client compatibility), still exploitable. Check router
   config screens.
3. **Evil twin / Karma** — version-independent. Attacks the client's trust
   decision (auto-reconnect to known SSID, no pre-association AP authentication),
   not the crypto. Highest-value, least version-dependent skill in the lab, and
   closest to what real engagements actually lean on.
4. **OWE's gap** — encrypts traffic, still doesn't authenticate the AP, so an
   OWE evil-twin is as feasible as an open-network one.
5. **Enterprise auth (802.1X)** — separate attack surface regardless of
   Personal-mode version: rogue RADIUS, EAP downgrade, credential relay.
6. **KRACK (reinstallation attacks)** — driver/implementation bug, not strictly
   version-tied. **CVE-2017-13077 through CVE-2017-13088.** Check router/client
   driver patch status rather than assuming "WPA2 = vulnerable, WPA3 = safe."
7. **WPS PIN brute force** — design flaw independent of WPA version, present
   whenever WPS is left enabled. **CVE-2011-5053.**
8. **PMKID attack** (`hcxdumptool`) — doesn't need a client handshake at all,
   works against many WPA2/WPA3-mixed APs that support PMKID caching. Check per
   router.

## How to filter "feasible in this lab" going forward

Ask three questions per candidate attack:
- Does it target the **protocol/crypto** or the **client's trust behavior**?
  Trust-behavior attacks stay feasible across every generation; protocol attacks
  need a per-device patch-status check.
- Can you **verify pass/fail objectively** with your gear (handshake captured:
  y/n, client associated to rogue AP: y/n)? If not, it's a demo, not a lab result.
- Do the **3 routers' actual firmware/settings** support the precondition (PMF
  toggle, mixed-mode toggle, 6 GHz radio, Enterprise mode)? Check the admin panel,
  don't assume from the spec sheet.

## References worth reading directly

- [Dragonblood paper](https://papers.mathyvanhoef.com/dragonblood.pdf) — read
  cover to cover before Module 8.
- [Dragonblood Black Hat slides/whitepaper](https://i.blackhat.com/USA-19/Wednesday/us-19-Vanhoef-Dragonblood-Attacking-The-Dragonfly-Handshake-Of-WPA3-wp.pdf)
- [Dragonblood mirror, aircrack-ng.org](https://dl.aircrack-ng.org/wiki-files/doc/additional_papers/dragonblood.pdf)
- Wi-Fi Alliance's own WPA3 and 6 GHz security specs (wi-fi.org) — ground truth
  for what's mandatory per generation, to check routers against spec.
- USENIX Security / IEEE S&P / NDSS proceedings — search their archives directly
  for "WPA3", "SAE", "802.11w" for legitimate new research; treat vendor
  marketing pages and "top 10 WiFi attacks" listicles as noise.
