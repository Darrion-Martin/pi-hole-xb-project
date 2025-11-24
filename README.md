# Pi-hole + XB Ad-Block Project

## Project Description
This project documents setting up Pi-hole on a Raspberry Pi 400 for network-wide ad-blocking, complemented by the XB browser extension for YouTube and in-browser ads. The goal is to reduce ads and trackers across all devices while keeping work devices unaffected.
## Today's Log (2025-11-24)

- **Hardware & Network Setup**
  - Raspberry Pi 400 connected to TP-Link Deco XE75 mesh
  - Reserved static IP: 192.168.68.87
  - SSH access from MacBook (2014)

- **Installation Steps**
  - Installed Pi-hole via terminal using the official installer
  - Configured network interface, upstream DNS (Cloudflare), web interface, query logging, and privacy settings
  - Accessed admin dashboard at http://192.168.68.87/admin

- **Troubleshooting**
  - Fixed “site cannot be reached” by pointing Mac DNS to Pi-hole and flushing cache
  - Verified DNS with `dig yahoo.com @192.168.68.87`
  - Noted Yahoo queries spiked from ~130 → ~1200; initial block %: 30.9%

- **Enhancements**
  - Added extra blocklists: StevenBlack, MalwareDomains, SmartTV-AGH, adblock-nocoin, Spam404, Disconnect
  - Added regex filters for major ad networks (doubleclick.net, ads.yahoo.com, adservice.google.com)
  - Installed XB browser extension for YouTube ad-blocking

- **Results**
  - Pi-hole blocked ~30–40% initially; expected higher with updated lists
  - XB blocks YouTube pre-roll and in-browser ads in Chrome
  - All devices on network benefit without disrupting work devices
  
## Lessons Learned
- DNS-level blocking alone cannot fully block YouTube video ads
- Chrome Manifest V3 limits traditional browser ad-blockers; XB is a suitable workaround
- Combining Pi-hole + browser-level ad-blocker achieves near-complete coverage
- Always reserve static IPs in mesh/router before running Pi-hole

