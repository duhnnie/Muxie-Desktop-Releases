# About "Reset Playback Logs after sync" feature

![](./assets/logo.png)

From Muxie 2.1.0 the "Reset Playback Logs after sync" feature was added as **experimental**. By enabling this option the `Play Counts` and `.scrobbler.log` files in your devices will be deleted after syncing them with Muxie. Continue reading to know in which cases this can be useful and in which cases you could consider not to use this feature.

There's a [known issue](https://github.com/duhnnie/Muxie-Desktop-Releases/blob/main/KNOWN_ISSUES.md#issue-2-duplicate-scrobbles-after-syncing) that can be prevented by deleting the _Play Counts_ file after every sync with Muxie. Normally, this file is deleted when the device is synced with iTunes or the Music app, since their sync process clears it automatically. However, some users either do not use those applications or prefer not to sync with them every time they sync with Muxie. For those users turning on the **Delete **Play Counts** file** option will be useful.

On the other hand, automatically deleting specifically _Play Counts_ file would prevent subsequent syncing with iTunes or the Music app from properly updating metadata such as “last played”. In some workflows, that metadata is still useful. For example, if you use dynamic playlists that depend on accurate “last played” information, so periodic syncing ensures those playlists stay correctly updated. In such case it would be preferable you sync your device with iTunes/Music app after syncing with Muxie and keep the feature turned off for _Play Counts_ file.

And about _.scrobbler.log_ file, firmwares like Rockbox allows the user to remove that file from the software itself, but it can be removed by Muxie also if you enable that option.
