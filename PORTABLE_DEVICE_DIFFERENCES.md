# Scrobbling Differences: iPod (Original Software) vs `.scrobbler.log` Devices

![](./assets/logo.png)

Muxie supports scrobbling listens from portable music players in two distinct ways:

1. **Direct scanning of iPods running Apple’s original firmware**
2. **Importing listens from a `.scrobbler.log` file** (Portable Player Logging format)

While both approaches ultimately send listens to Last.fm, they differ significantly in how plays are recorded, displayed, and processed. This document explains those differences in detail.

---

## 1. How Plays Are Recorded and Displayed

### iPod with Apple Original Software

iPods running Apple’s original firmware do **not** store individual play events. Instead, for each track they only record:

- The **last played date and time**
- The **number of plays since the last sync** with iTunes / Music.app

As a result:

- Muxie cannot know *exactly when* each individual listen occurred, only the timestamp of the last one is reliable.
- Plays are **condensed** into a single entry per track.
- In Muxie’s *iPod Scrobbles* section, you may see:
  - One row per track
  - A play count equal or greater than `1`, representing one or multiple listens since the last sync with iTunes/Music app.
  - Date and time for last play only is displayed
- How Muxie scrobbles:
  - Track is scrobbled with displayed date and time (the date and time of last play for that track)
  - If option for scrobbling repeated plays is on, then Muxie treats all remaninig plays as having occurred consecutively just before the last play. It does this by subtracting the length of the track from the timestamp of the last play to estimate when each earlier play occurred.
  - As a result, when the tracks are scrobbled, it will look as though you listened to all the songs in a continuous sequence, ending with the most recent play.

Additionally:
  - Unlike devices with `.scrobbler.log` support, Muxie is capable of including **album artist** information (if available) in the scrobbled track for supported iPods running Apple's stock software, even though this is not displayed in the application's UI. You might want to check this related [known issue](./KNOWN_ISSUES.md#issue-4-album-artist-scrobbling).

This is a limitation of the data provided by the device itself. You might want to read this related know issues: [#1](./KNOWN_ISSUES.md#issue-1-fake-timestamps-for-old-scrobbles) and [#2](./KNOWN_ISSUES.md#issue-2-duplicate-scrobbles-after-syncing).

---

### Devices Using `.scrobbler.log`

Devices that generate a `.scrobbler.log` file (Portable Player Logging format) record **every individual play event**, including:

- One entry per listen
- A specific date and time for each play

As a result:

- Muxie imports **each listen separately**
- In the *iPod Scrobbles* section, you might see:
  - Multiple rows for the same track
  - Each row with a play count of `1`
- What Muxie scrobbles:
  - Each row is scrobbled regardless the existence of many rows with the same track.

**This behavior is expected and reflects the higher granularity of the logging format.**

Additionally:
  - Unlike with iPods running Apple's stock software, Muxie is **not capable to include album artist** info in the scrobbled track for for `.scrobbler.log` devices. This is not a limitation of Muxie, but a limitation of the [`.scrobbler.log` v1.1 specification](https://web.archive.org/web/20170107015006/http://www.audioscrobbler.net/wiki/Portable_Player_Logging). You might want to check this related [known issue](./KNOWN_ISSUES.md#issue-4-album-artist-scrobbling).

---

## 2. How Timestamps Are Determined

### iPod with Apple Original Software

- The iPod stores timestamps in **local time**, without timezone information.
- There is no reliable way to determine the timezone configured on the iPod.

Muxie handles this by:

1. Reading the local timestamp from the iPod
2. Assuming it belongs to the **host machine’s timezone**
3. Converting it to UTC before scrobbling

If the iPod’s timezone differs from the host machine’s timezone, the resulting scrobble timestamps may be incorrect. You might want to check this related [known issue](./KNOWN_ISSUES.md#ipods-with-apple-original-software).

---

### `.scrobbler.log` Files

Depending on the Portable Player Logging (`.scrobbler.log`) implementation for the device, timezone information **may or may not be included** in each log entry.

Muxie behaves as follows:

- **If timezone information is present**:
  - The timestamp is converted to UTC correctly
  - Scrobbles reflect the original listen time accurately

- **If timezone information is not present**:
  - Muxie assumes the timestamp is expressed in the **host machine’s timezone**
  - That timezone is used to convert the timestamp to UTC

If the device logged the plays in a different timezone than the host machine, this can result in shifted scrobble times. You might want to check this related [known issue](./KNOWN_ISSUES.md#for-devices-with-scrobblerlog-files)

---

## 3. Manual Cleanup of `.scrobbler.log` Files

Unlike iPods with original firmware, `.scrobbler.log` files are **not automatically cleared** after importing. Every new listen will just append a new record to the file. While Muxie's algorithm avoids duplicated listen imports from this file, after some time this could result on a huge file making Muxie need more time to read unnecessary and already-scrobbled records.

For that is recommended to remove this file after syncing with Muxie, some implementations (such as Rockbox’s `lastfm_scrobbler` plugin) provide an option in the device UI to clear or delete the log file after export.

---

## 4. Required Fields in `.scrobbler.log` Entries

According to the Portable Player Logging specification:

https://web.archive.org/web/20170107015006/http://www.audioscrobbler.net/wiki/Portable_Player_Logging

Each listen entry must include a set of **required fields** (such as artist, track title, timestamp, and others depending on the format version).

Muxie enforces this strictly:

- If **any required field is missing or malformed**, that listen entry is **excluded**
- The listen will not appear in Muxie therefore it will not be scrobbled to Last.fm

This ensures compatibility with Last.fm’s submission requirements and avoids invalid scrobbles.

---

## Summary

| Feature | iPod (Original Software) | `.scrobbler.log` Devices |
|------|-------------------------|--------------------------|
| **Play granularity** | Condensed (count + last play) | One entry per play |
| **Display in Muxie** | Single row, play count >= 1 | Multiple rows, play count = 1 |
| **Timestamp source** | Local time, no timezone<sup>1</sup> | With or without timezone |
| **Timestamp conversion** | Uses host timezone<sup>1</sup> | Uses embedded timezone if present, otherwise host timezone |
| **Post-sync cleanup** | Automatic when syncing with iTunes or Music app | Depends on device software |
| **Albumt Artist scrobbling** | Yes (if available) | No, [`.scrobbler.log` specification](https://web.archive.org/web/20170107015006/http://www.audioscrobbler.net/wiki/Portable_Player_Logging) doesn't include `album artist` |

Understanding these differences will help you interpret your scrobbles correctly and avoid unexpected timestamp or duplication issues.

---
<sup>1</sup> _While we are not able to determine which file from iPod's original software contains that information. If you know it please let us know opening a [new issue](https://github.com/duhnnie/Muxie-Desktop-Releases/issues)._

