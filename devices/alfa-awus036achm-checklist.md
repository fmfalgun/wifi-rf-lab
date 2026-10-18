# Device Checklist — ALFA AWUS036ACHM

Dual-band AC1200 USB adapter with monitor mode + packet injection on Linux. This
is the "do it by hand" radio in the lab — run everything here with raw tools
(aircrack-ng suite, scapy, hostapd) against your own 3 routers and lab clients
before repeating the same attack through a Pineapple module.

Driver note: confirm injection works before trusting any result — `iw list`
should show monitor mode, and `aireplay-ng --test <iface>` should confirm
injection on the chipset/driver combo you installed.

Status key: `[ ]` not tried · `[~]` partial · `[x]` done (add date + which
router/client in the note).

## Feasible to learn/verify on this device

- [ ] Monitor-mode frame capture (beacon/probe/auth/assoc/EAPOL) — Module 1 baseline
- [ ] Recon / enumeration of the 3 lab routers (`airodump-ng`)
- [ ] Deauth/disassoc against a non-PMF network, then against a PMF-enabled one
      to confirm the expected failure
- [ ] WPA2 4-way handshake capture + offline crack against a PSK you set yourself
- [ ] PMKID capture + crack where the router supports it
- [ ] WPS PIN brute force where WPS is left on
- [ ] WPA3 transition-mode downgrade check on a mixed WPA2/WPA3 SSID
- [ ] WPA3/SAE Dragonblood checks (group downgrade, timing side-channel) against
      each router's actual firmware patch level
- [ ] Manual rogue AP / evil twin / captive portal build with `hostapd`+`dnsmasq`
- [ ] MITM inspection (`bettercap`) once a lab client associates to your own AP

## CVEs & research to check firmware/drivers against

- WPA3/SAE Dragonblood: **CVE-2019-9494 / 9495 / 9496 / 9497 / 9498 / 9499** —
  [paper](https://papers.mathyvanhoef.com/dragonblood.pdf),
  [project page](https://wpa3.mathyvanhoef.com/)
- KRACK reinstallation bugs: **CVE-2017-13077 through CVE-2017-13088** —
  [krackattacks.com](https://www.krackattacks.com/)
- WPS PIN brute force design flaw: **CVE-2011-5053** —
  [NVD entry](https://nvd.nist.gov/vuln/detail/CVE-2011-5053)
- Driver/chipset injection support reference: aircrack-ng compatibility list —
  [aircrack-ng.org wiki](https://wiki.aircrack-ng.org/doku.php?id=compatibility_drivers)

## Non-security / other uses for this adapter (to try apart from attacks)

- [ ] Wardriving / signal mapping of your own space (`Kismet`, `wigle`-style logging)
- [ ] Spectrum/channel-utilization survey to pick the cleanest channel for the 3 routers
- [ ] Long-range client bridge / external antenna experiments for a weak-signal area
- [ ] General packet-capture tool for diagnosing your own home network issues

## References for verification

- [Aircrack-ng documentation](https://www.aircrack-ng.org/doku.php)
- [Wireshark 802.11 capture setup](https://wiki.wireshark.org/CaptureSetup/WLAN)
- [hashcat WPA/WPA2 hcx reference](https://hashcat.net/wiki/doku.php?id=hashcat)
- [Wi-Fi Alliance WPA3 specification page](https://www.wi-fi.org/discover-wi-fi/security)
