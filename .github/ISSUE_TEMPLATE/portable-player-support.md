---
name: Portable Music Player Support
about: Investigate scrobbling support for an unsupported portable music player
title: "[Portable Player] <Device brand and model>"
labels: portable-player, investigation
assignees: ""
---

## Device Information

Please provide as much detail as possible:

- **Brand:**
- **Model:**
- **Firmware / Software version:**
- **Storage type:** (e.g. USB mass storage, MTP, proprietary)
- **Operating system used to inspect the device:** (macOS / Windows / Linux + version)

---

## Does the Device Track Plays?

- [ ] Yes, it clearly tracks play history
- [ ] Maybe / not sure
- [ ] No obvious play tracking found

If yes or unsure, please describe how you determined this (UI counters, history menus, last played info, etc.).

---

## Files or Folders of Interest

While exploring the device storage, did you find any files that may contain listening data?

Please list:

- **File paths and names:**
- **File formats:** (e.g. text, binary, JSON, database)
- **Approximate file size:**

Example:
```
/System/Logs/playhistory.dat
/Music/.history/log.txt
```


---

## Sample Files (Optional but Highly Recommended)

If possible, attach **sample files** that may contain play history:

- Prefer files with **only a few test listens**
- Do **not** include personal or sensitive data
- If the file is binary or unclear, that’s fine — attach it anyway

> If you are unsure whether a file is relevant, attach it and explain why you suspect it is.

---

## How and When the Data Is Written

If you noticed any patterns, please describe them:

- Is the file updated:
  - [ ] After each play
  - [ ] On device shutdown
  - [ ] On USB connection
  - [ ] On manual sync
- Does the data reset after syncing or persist indefinitely?

---

## Additional Notes

Include anything else that might help:

- Screenshots from the device UI showing play counts or history
- Documentation links
- Forum posts or reverse-engineering notes
- Comparisons with known formats (e.g. `.scrobbler.log`)

---

## Expectations

Please note:

- Not all devices store enough data to enable reliable scrobbling
- Some formats may be impossible to support without firmware changes
- This issue is for **investigation**, not a guaranteed feature request

Thanks for helping expand Muxie’s device support 🚀
