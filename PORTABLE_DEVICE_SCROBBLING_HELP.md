# Portable Devices Scrobbling - Help

## Overview

Muxie supports two portable listening sources:

- **iPod Classic running Apple’s original firmware**  
  These devices do **not** log every play individually. They store only the *last play time* and a cumulative *play count*.

- **Devices with `.scrobbler.log` support**
  These log every play event with exact timestamps, so each play appears as a separate entry.

Check [here](https://github.com/duhnnie/Muxie-Desktop-Releases/blob/main/DEVICE_SUPPORT.md) for more info about supported devices.

---

## How Plays Are Interpreted

### Apple iPod (Original Software)

- One entry per track with a play count.
- Only the **last play time** is reliable; earlier listens are estimated.
- If *“Scrobble repeated plays”* is enabled, repeated listens are time-spread backward from the last play.
- Album artist information may be included if available on the device.

### Devices with `.scrobbler.log`

- Each logged play becomes its own row.
- Exact date and time from the device are used when available.
- Album artist is not supported by the `.scrobbler.log` specification.

Click [here](./PORTABLE_DEVICE_DIFFERENCES.md) for more information.

---

## Timestamps & Timezones

- iPods store local timestamps **without timezone information**.  
  Muxie assumes the host computer’s timezone, which can cause shifted times if the device used a different timezone.

- For `.scrobbler.log` files, timezone information may be included.  
  If not present, the host timezone is assumed.

---

## Known Issues

### 1. Estimated Timestamps on Older Plays (iPod running Apple original firmware)

Earlier plays do not have real timestamps, they are estimated based on track duration.  

Click [here](https://github.com/duhnnie/Muxie-Desktop-Releases/blob/main/KNOWN_ISSUES.md#issue-1-fake-timestamps-for-old-scrobbles) for more information.

---

### 2. Duplicate Scrobbles (iPod running Apple original firmware)

If you listen repeatedly without syncing with iTunes/Music between Muxie syncs, previously submitted plays may be resubmitted.

Click [here](https://github.com/duhnnie/Muxie-Desktop-Releases/blob/main/KNOWN_ISSUES.md#issue-2-duplicate-scrobbles-after-syncing) for more information.

---

### 3. Timezone Mismatch

If your iPod and your computer use different timezones, scrobbles may appear shifted.

Click [here](https://github.com/duhnnie/Muxie-Desktop-Releases/blob/main/KNOWN_ISSUES.md#issue-3-incorrect-listen-timestamps-due-to-timezone-mismatch) for more information.

---

### 4. Missing Album Artist Information

Some devices do not include album artist metadata. 

Click [here](https://github.com/duhnnie/Muxie-Desktop-Releases/blob/main/KNOWN_ISSUES.md#issue-4-album-artist-scrobbling) for more information

---

## Full Documentation

For complete details and technical explanations:

- https://github.com/duhnnie/Muxie-Desktop-Releases/blob/main/PORTABLE_DEVICE_DIFFERENCES.md  
- https://github.com/duhnnie/Muxie-Desktop-Releases/blob/main/KNOWN_ISSUES.md
