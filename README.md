# NETWORKWALKS-OHIS-B084C-WK1-PM1-CYBERSECURITY-LAB-SETUP

## Project Overview

- **Program:** Networkwalks Cybersecurity program, Batch BO84C
- **Task:** Week 1, Project Module 1 (WK1-PM1) - Cybersecurity testing lab setup
- **Author:** Ohiorenuan Ohis Osigele-Kehinde
- **Date completed:** 28-10-2016
- **Goal:** Build a virtual cybersecurity practice environment on a personal laptop or desktop computer, using VirtualBox as the base and Kali Linux as the attacking machine.

---

## Task Requirements

- Use VirtualBox as the base (latest recommended version).
- Set up Kali Linux as the attacking machine.
- Set up the network in the subnet 10.0.0.0/24.
- Use a Network Address Translation Network (named NatNetwork) with the range 10.0.0.0/24.
- Enable the clipboard and file drag and drop in the virtual machine settings.
- Enable shared folders, with the Downloads folder shared from the host machine.
- Set the Kali Linux Internet Protocol address to 10.0.0.2/24.
- Confirm that Kali Linux has full Internet access.

---

## Lab Environment

- **Host operating system:** Windows 11
- **Host memory:** 4GB
- **Host storage:** 2GB
- **Host processor:** 16GB
- **VirtualBox version:** VirtualBox-7.2.22-175245-Win
- **Kali Linux version:** kali-linux-2026.2-virtualbox-amd64
- **Network name:** NatNetwork
- **Network range:** 10.0.0.0/24
- **Kali Linux address:** 10.0.0.2/24
- **Gateway:** 10.0.0.1
- **Domain Name System server:** 8.8.8.8

---

## Tools Used

- **7-Zip** - used to extract the compressed Kali Linux virtual machine download
- **Oracle VirtualBox** - virtualization platform that hosts the lab
- **Kali Linux** - security-focused operating system used as the attacking machine

---

## Step-by-Step Implementation

### Step 1: Download and Install 7-Zip

- Downloaded 7-Zip from the official website.
- Installed it on the host machine.
- Purpose: extract the compressed Kali Linux virtual machine file.


### Step 2: Download and Install VirtualBox

- Downloaded the latest recommended VirtualBox version from the official website.
- Installed it on the host machine with the default options.
- Confirmed that VirtualBox opened successfully.


### Step 3: Create the Network Address Translation Network

- Opened VirtualBox, then selected **File**, then **Tools**, then **Network**.
- Selected the **NAT Networks** tab and clicked **Create**.
- Configured the network with these values:
  - **Name:** NatNetwork
  - **IPv4 Prefix:** 10.0.0.0/24
  - **Enable DHCP:** checked (Dynamic Host Configuration Protocol)
  - **Enable IPv6:** unchecked
- Clicked **Apply**.


### Step 4: Download and Import Kali Linux

- Downloaded the Kali Linux virtual machine image for VirtualBox from the official Kali website.
- Extracted the download using 7-Zip.
- Imported the virtual machine into VirtualBox.
- Confirmed that the Kali Linux virtual machine appeared in the VirtualBox list.


### Step 5: Configure the Virtual Machine Settings

- **Network settings (Adapter 1):**
  - Enabled the network adapter.
  - Attached to: **NAT Network**
  - Name: **NatNetwork**
  - Promiscuous Mode: **Allow All**
  - Virtual cable connected: checked
- **General settings, Advanced tab:**
  - Shared Clipboard: **Bidirectional**
  - Drag and Drop: **Bidirectional**
- **Shared Folders:**
  - Added the host machine **Downloads** folder as a global folder.
  - Access: **Full**
  - Auto Mount: **Yes**
- **System settings (optional adjustment):**
  - Adjusted base memory and processors to suit the host machine.


### Step 6: Configure the Internet Protocol Address on Kali Linux

- Started the Kali Linux virtual machine.
- Right-clicked the network icon in the top panel and selected **Edit Connections**.
- Opened **Wired connection 1**, then the **IPv4 Settings** tab.
- Changed the method from Automatic to **Manual**.
- Added this address:
  - **Address:** 10.0.0.2
  - **Netmask:** 24
  - **Gateway:** 10.0.0.1
- Set the **Domain Name System servers** to 8.8.8.8 (10.0.0.1 can be used if the Internet gives issues).
- Saved the connection.


### Step 7: Verify Network Configuration and Internet Access

- Opened a terminal in Kali Linux and ran the following checks:

```bash
ip a
ping -c 4 10.0.0.1
ping -c 4 8.8.8.8
ping -c 4 google.com
```

- Confirmed the results:
  - The address 10.0.0.2/24 appears on the network interface.
  - The gateway replies.
  - An external address replies (proves Internet connectivity).
  - The domain name resolves (proves Domain Name System resolution works).


### Step 8: Test Shared Folder, Clipboard, and Drag and Drop

- Confirmed that the host Downloads folder is visible inside Kali Linux.
- Copied text from the host machine and pasted it inside Kali Linux.
- Dragged a file from the host machine into Kali Linux.


### Step 9: Take a Clean Snapshot

- With the virtual machine working correctly, opened the **Snapshots** section in VirtualBox.
- Clicked **Take** and named the snapshot, for example: `Clean Kali Linux - Lab Setup Complete`.
- Purpose: allows quick recovery if the virtual machine breaks during future labs.


---

## Verification Checklist

- [ ] VirtualBox installed (latest recommended version)
- [ ] Kali Linux imported and running
- [ ] NatNetwork created with 10.0.0.0/24
- [ ] Clipboard and drag and drop enabled
- [ ] Shared folder (Downloads) enabled
- [ ] Kali Linux address set to 10.0.0.2/24
- [ ] Kali Linux has full Internet access
- [ ] Clean snapshot taken

---

## Troubleshooting

### Problem: Kali Linux had no Internet access

- **Symptom:** [Describe exactly what you saw, for example: pings to external addresses failed.]
- **Possible causes checked:**
  - NatNetwork was not created properly.
  - Network settings were incorrect.
  - Another virtual machine on the same network was already using 10.0.0.2.
- **Solution applied:** Ran these three commands, then restarted Kali Linux (a known issue with VirtualBox version 7 and Kali Linux 2026.1 or newer):

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
sudo nmcli connection down "Wired connection 1"
sudo nmcli connection up "Wired connection 1"
```

- **Result:** Internet access was restored.


---

## What I Learned

- How virtual machine networking works in VirtualBox
- The difference between a Network Address Translation connection and a Network Address Translation Network
- How to assign a manual Internet Protocol address, gateway, and Domain Name System server on Kali Linux
- How to enable shared folders, clipboard sharing, and drag and drop
- How to use snapshots for recovery
- How to document technical work clearly with screenshots

---

## Acknowledgements

- Thank you to Waqas Karim CCIE and the Networkwalks team for the guidance and support.

## Next Step

- Week 2 project tasks
