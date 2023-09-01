# Chase
## Introduction
This is a write-up for the Hack The Box "Chase" room. Lets get Started!

## Difficulty: Easy
![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/28528171-0ebf-49e0-999f-0668c5636656)

## Room Description
One of our web servers triggered an AV alert, but none of the sysadmins say they were logged onto it. We've taken a network capture before shutting the server down to take a clone of the disk. Can you take a look at the PCAP and see if anything is up?

## Tools Used
Wireshark

## Resources
- THM Wireshark: The Basics - https://tryhackme.com/room/wiresharkthebasics
- Wireshark Documentation - https://www.wireshark.org/docs/wsug_html_chunked/ChWorkDisplayFilterSection.html

## Skill(s)
Forensics

## Points
![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/7fde5184-6639-471c-a6c6-81855e13982b)

## Walkthrough

Unzip the file and open the pcap.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/cbed6a60-5274-407b-84f0-43444db56387)

This is my first time using Wireshark without any guidance, so I'm just gonna look around at the different tabs and see how I can use them. There's a total of 216 packets, so I'm not going to look at them one by one. I'll first try filtering them by http protocol.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/a5deadc1-212b-4447-9fb1-0f50df19764c)

This brought my number of packets to look at down to 21. There are some GET requests that have a text file! I'm gonna check that out.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/23d542e1-6c8b-4f40-ba20-948bb60efcc4)

Not sure how this is encoded. It looks like BASE64, but idk.

![GLC_shrug](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/4c342e13-8577-44fa-9111-353e8790ecff)

Gonna use this website to decode the filename > https://cryptii.com/pipes/caesar-cipher

Turns out it was base32.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/3df7d06b-6a15-4e03-9b89-112828d50a63)

Flag Captured!

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/a92220ef-1d0d-47ad-a64e-86bd1205f053)
