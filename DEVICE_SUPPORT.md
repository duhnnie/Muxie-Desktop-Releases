# Expanding Device Support

![](./assets/logo.png)

## Supported models

Muxie is capable of scrobbling from following devices:

- [iPod classic (Late 2019)](https://support.apple.com/en-us/103823#ipod) with software updated to 2.0.4 Mac formatted. The iPod Classic Late 2019 is, according [Wikipedia](https://en.wikipedia.org/wiki/IPod_Classic#Models), 6th generation, and according many users, 7th generation. 

- **iPod (5th generation)** also known as iPod with video or Fifth Generation iPod. Firmware 1.3 (6.3), Mac formatted.

- Any device capable of generating a [`.scrobbler.log`](https://web.archive.org/web/20170107015006/http://www.audioscrobbler.net/wiki/Portable_Player_Logging) file like [Rockbox](https://download.rockbox.org/daily/manual/rockbox-ipod6g/rockbox-buildch12.html#x19-36200012.4.12)-powered devices.

Currently, support is limited to these particular models. If your iPod model is supported and is not listed above please let us know.

While we support the mentioned models, there are still some little known issues, [check them out](https://github.com/duhnnie/Muxie-Desktop-Releases/blob/main/KNOWN_ISSUES.md) and [differences in how Muxie work with them](./PORTABLE_DEVICE_DIFFERENCES.md).

We are exploring the possibility of supporting additional iPod models or other devices in future updates. **This excludes any model of iPod Touch**. 

---

## For iPod models running Apple's original software

### What We Need?

If you would like to help, we may need you to provide some information and a few files from your iPod.

#### iPod Information

Please provide the following details about your iPod:

- Model and generation (e.g., iPod Nano 5th Gen, iPod Mini 2nd Gen, etc.) (Check this [list of models](https://support.apple.com/en-us/103823))
- Storage capacity (e.g., 16GB, 80GB, etc.)
- Software version installed on the device (please ensure the device is updated to the latest version available for it)
- Whether any client (at any time) has been able to **scrobble** songs from this device.

#### Files Needed

We will also need some files and information from your iPod.  
Since we do not know the file structure of all iPod models, we can only provide general guidance:

- First, **please make sure your iPod is updated to the latest software version available** before extracting the files.

- Second, **listen to a few tracks** on your iPod before extracting the files.  
  - This is important so we have recent listening activity to work with.
  - Please provide a list of the tracks you listened to, along with an approximate time when you started and finished each track.  
    - If the iPod has a screen, use the device's displayed time.
    - If the iPod does not have a screen, use your local time.

- We need the file that contains the **song database** from your iPod.  
  - On the iPod Classic, this file is called `iTunesDB`, located at `/iPod_Control/iTunes/`.  
  - (Note: The `iPod_Control` folder and its contents might be hidden.)

- We also need the file that stores the **play counts**.  
  - On the iPod Classic, this file is named `Play Counts`, and it is also located at `/iPod_Control/iTunes/`.  
  - (The play count information may be inside the same file as the song database or in a separate file.)

- (Optional) If possible, please also provide the **Preferences** file.  
  - On the iPod Classic, this file is located at `/iPod_Control/Device/Preferences`.
  - However, in other iPod models, the Preferences file might have a **different name or be located in a different folder**.
  - This file may contain the **timezone configuration** of the iPod, which can help us correctly scrobble tracks using UTC time instead of assuming the iPod's time is local.

- Please include the **original location (full path)** of each file you send.  
  - This will help us replicate a real scenario with the correct file structure during testing.


> **Note:**  
> The file structure in other iPod models might be different. Files may have different names, be stored in different locations, or all the needed information could be contained within a single file.  
> In some cases, certain iPod models might **not store** the necessary information at all, in that situation, unfortunately, we won't be able to support that model.

> If you're unsure about which files to send, feel free to open an Issue in this repository. We'll guide you through the process!

> **Reminder:**  
> Providing this information and files does **not guarantee** that support for your device will be possible. However, your contribution will help us evaluate and potentially expand compatibility.

Thank you for being part of this effort!

### How to Provide the Information

Once you have gathered all the necessary information and files, please follow these steps to provide them:

1. **Search for an existing issue**:  
   Before creating a new issue, please search in the Issues section of the repository to see if anyone has already requested support for the **same iPod model** you have.  
   - If a relevant issue exists, feel free to **add your information** to that issue.  
   - You can also provide a **link to the files** from your device using a file-sharing service like Dropbox or any similar service. Just make sure to include the link in your comment.

2. **Create a new issue**:  
   If no relevant issue exists, please create a new issue in the Issues section of the repository. You can use the following [link to the Issues section](https://github.com/duhnnie/Muxie-Desktop-Releases/issues) to get started.  
   - When creating the issue, use the **"iPod Support Request"** issue template.  
   - In the issue template, fill in the required fields, including the **link to your files** (provided via a service like Dropbox). This will ensure we can access the necessary information and start working on your request.

3. **Be patient**:  
   Once your issue is submitted, please allow some time for us to review the information and files you've provided.  
   We may need to ask you for further details or clarification. We appreciate your patience and understanding as we evaluate your request and work to expand iPod model support.

Thank you for helping us improve compatibility with additional iPod models!

## Support for other Portable Music Players

Beyond iPods running Apple’s original software and devices that generate a `.scrobbler.log` file, there is a wide variety of portable music players with unknown or undocumented ways of storing play history, if they store it at all.

At this time, there is **no generic guide** for enabling scrobbling support on other portable players. Each device may:

- Store play history in a proprietary format
- Store only partial play information
- Not store play history at all
- Expose logs in unexpected locations or file formats

Because of this, adding support for new devices requires **device-specific investigation**.

If you’re interested in using Muxie with a portable player that is not currently supported, you’re encouraged to:

1. Explore the device’s storage when connected to your computer.
2. Look for files that may contain play history or listen logs.
3. Identify anything that resembles:
   - Track identifiers
   - Play counts
   - Timestamps
   - Sequential or append-only log files

If you find files that you believe may contain listening data, please **open a ticket** and include:

- Device brand and model
- Firmware or software version
- File paths and filenames involved
- Sample files (if possible)
- Any insights about how or when the data is written

This information is essential to evaluate whether support can be added and how reliable it could be.

Community contributions are especially valuable here, many supported formats start with curious users exploring their devices.


