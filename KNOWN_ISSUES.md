# Muxie's Known Issues

## Issue #1: Fake timestamps for old scrobbles

### Description
For each track the iPod keeps track of two things: the total number of plays since the last sync, and the date and time of the most recent play. This means Muxie cannot determine the exact times of earlier plays for that track, only the timestamp of the last one is reliable.

To handle this, Muxie makes an assumption: it treats all previous plays as having occurred consecutively just before the last play. It does this by subtracting the length of the track from the timestamp of the last play to estimate when each earlier play occurred.

As a result, when the tracks are scrobbled, it will look as though you listened to all the songs in a continuous sequence, ending with the most recent play.

### Workaround

Muxie provides an option to scrobble only the most recent listen of a track, using the accurate timestamp from the iPod. This helps avoid adding earlier plays with estimated timestamps.

When this option is enabled, Muxie ignores the total play count and scrobbles just the last play. This is useful if you want to avoid a series of backdated scrobbles based on assumptions and only care about tracking the most recent time you listened to the song.

## Issue #2: Duplicate Scrobbles After Syncing

### Description

Sometimes, multiple scrobbles can result in duplicate entries—scrobbles that have already been submitted. This happens under the following scenario:

Imagine you listen to Song A on your iPod 5 times. Then, you sync your iPod with Muxie, and everything is scrobbled correctly. After that, you listen to the same song 3 more times. The iPod's internal database updates the play count from 5 to 8. The next time you sync with Muxie, it sees 8 plays in total and scrobbles all of them again—including the 5 that were already submitted.

### Workaround

To prevent this from happening, you can do one of the following:

Sync your iPod with iTunes after every Muxie sync (this resets the internal play tracking), or
Manually delete the Play Counts file from your iPod after each Muxie sync.

## Issue #3: Incorrect Listen Timestamps Due to Timezone Mismatch

### Description

Muxie may scrobble listens with a timestamp that differs from the original listen time. This happens if the computer running the app is set to a different timezone than the iPod being synced.

iPods store listen records using local time, but they do not include the timezone information along with it. Although we could convert this local time to UTC (which is required for scrobbling), we currently have no reliable way to determine the iPod's timezone automatically.
As a workaround, Muxie uses the timezone of the host machine to convert iPod timestamps to UTC. If the host machine's timezone is different from the iPod’s, this results in incorrect UTC timestamps when scrobbling.

> If you know of a way to extract the timezone from an iPod, please [open a ticket](https://github.com/duhnnie/Muxie-Desktop-Releases/issues) and share the method along with iPod details (version, firmaware version, etc).

### Example 

**Suppose:**

- **iPod Timezone**: Eastern Standard Time (EST; UTC−5)
- **Listen Time of a track on iPod**: 3:00 PM EST
- **Expected UTC Time for Scrobble**: 8:00 PM UTC
- **Host Machine Timezone**: Pacific Standard Time (PST; UTC−8)

**What happens:**

1. You connect your iPod to your machine, Muxie scans it and get the listen with a timestamp of 3:00 PM (local time), but not the timezone.
2. Muxie assumes the timestamp is in PST (the timezone of the host machine).
3. Muxie converts 3:00 PM PST → 11:00 PM UTC.
4. Muxie scrobbles the listen with time 11:00 PM UTC, instead of the correct 8:00 PM UTC.

**Result:**

The listen is scrobbled 3 hours later than when it actually occurred, due to a timezone mismatch between the iPod and the host machine.

### Workaround

- Set the host machine to the same timezone as the iPod before syncing.

- Be mindful when traveling with a laptop:
    - macOS and other systems may automatically update the timezone based on your location.
    - If your iPod remains on its original timezone (e.g., EST), but your Mac switches to a new one (e.g., CET), you'll experience timezone mismatches.

- Verify your machine’s timezone before syncing to ensure consistency with the iPod.


## Final Thoughts

- [Issue #2](KNOWN_ISSUES.md#issue-2-duplicate-scrobbles-after-syncing) may be fixed in a future update by deleting automatically the PlayCount file after syncing.

- [Issue #3](KNOWN_ISSUES.md#issue-3-incorrect-listen-timestamps-due-to-timezone-mismatch) might be fixed if we could extract the timezone from the iPod. If you know how to do it please open a ticket with the info.

