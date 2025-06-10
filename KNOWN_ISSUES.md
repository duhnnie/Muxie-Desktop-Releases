# Muxie's Known Issues

## Issue #1: Fake timestamps for old scrobbles

### Description
The iPod only keeps track of two things: the total number of plays since the last sync, and the date and time of the most recent play. This means Muxie cannot determine the exact times of earlier plays—only the timestamp of the last one is reliable.

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

## Conclusion

- [Issue #2](KNOWN_ISSUES.md#issue-2-duplicate-scrobbles-after-syncing) may be fixed in a future update by deleting automatically the PlayCount file after syncing.

