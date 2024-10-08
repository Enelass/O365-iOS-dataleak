 # iPhone Data Exfiltration Guide

## Overview
This guide provides step-by-step instructions for exfiltrating data from an iPhone. The process involves jailbreaking the iPhone, setting up an SSH server, bypassing jailbreak detection, and transferring files using SCP.

## Purpose
I am sharing this guide to give organizations the means to protect themselves. Organizations should actively monitor which iPhone models and iOS versions can be jailbroken and take measures to forbid access to Office 365 using Conditional Access policies. They should also be cautious about Bring Your Own Device (BYOD) policies, as these devices are more likely to be jailbroken since they are unmanaged.

## Steps

### 1. Jailbreak iPhone and Setup SSH Server
- Jailbreak your iPhone using a trusted tool.
- Set up the SSH server on the iPhone.
- Change the default password for the SSH server to enhance security.

### 2. Bypass Jailbreak Detection
- Use tools like Shadow, LibertyLite, or Flex to bypass jailbreak detection.
- Alternatively, install an older version of the app (e.g., using AppStore++) that does not have jailbreak detection.

### 3. Patch OneDrive (if necessary)
- For OneDrive version 12.11.6, use the OneDrive patch on Flex (other tools may not work).
- If the installed version of OneDrive is not the right one, download an older version using AppStore++.

### 4. Login and Select Files for Offline Access
- Log in to OneDrive using your work credentials.
- Select "Make Available Offline" for the files you want to exfiltrate.

### 5a. Transfer Files from iPhone Filesystem (iOS 13)
- Use SCP to transfer files from the iPhone filesystem.
- Connect to the iPhone via SSH:
  ```bash
  ssh root@<iPhone>
  ```
- Replace `<iPhone>` with the Bonjour-resolved name (e.g., `iphone.local`) or the IP address (found in Settings / WiFi).
- Navigate to the top directory:
  ```bash
  cd /
  ```
- Search for the file:
  ```bash
  find . -name "<File>"
  ```
- Replace `<File>` with the name of the file you are looking for (e.g., `file.zip`, `*.zip`, `whateverthef*`).
- The directory for offline files is typically: `/private/var/mobile/Containers/Shared/AppGroup/DBD29029-B5D0-4DF5-86C6-ACB767D4DA7D/OneDrive/StreamCacheQt/`


### 5b. Transfer Files from iPhone Filesystem (iOS 14)
- Since iOS 14, data is encrypted at rest, making exfiltration slightly harder.
- You do not need to mark the file for offline access.
- A workaround is to click on "Open in another App," which will place a clear text copy of the files in the cache.
- The new directory includes "tmp" in its address, e.g.: `/private/var/mobile/Containers/Data/Application/31C8BB3C-404D-49A2-BDC9-E61C349211CA/tmp/i2k5ymqgmus4yxgt8evtwq/`

### 6. Download the File(s) Using SCP
- Navigate to your desired download location on your computer and use SCP to download the file(s):
  ```bash
  cd ~/Desktop; scp root@<iPhone>:<Path> .
  ```
- Replace <iPhone> with the Bonjour-resolved name or IP address, and <Path> with the path to the file on the iPhone.


### Important Notes
- Ensure you have the necessary permissions to perform these actions.
- Be aware of the legal and ethical implications of exfiltrating data.
- Always back up important data before performing any operations that could potentially cause data loss.

## Purpose
I am sharing this guide to give organizations the means to protect themselves. Organizations should actively monitor which iPhone models and iOS versions can be jailbroken and take measures to forbid access to Office 365 using Conditional Access policies. They should also be cautious about Bring Your Own Device (BYOD) policies, as these devices are more likely to be jailbroken since they are unmanaged.

## Disclaimer
This guide is provided for educational purposes only. Unauthorized access to computer systems is illegal and unethical. Always ensure you have explicit permission before using any offensive security tools or techniques.

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
