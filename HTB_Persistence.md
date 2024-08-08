# Persistence
## Introduction
This is a write-up for the Hack The Box "Persistence" room. Let's get Started!

## Difficulty: Easy
![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/a2c24890-fc6e-4c7e-96db-44aead939afa)


## Room Description
We&#039;re noticing some strange connections from a critical PC that can&#039;t be replaced. We&#039;ve run an AV scan to delete the malicious files and rebooted the box, but the connections get re-established. We&#039;ve taken a backup of some critical system files, can you help us figure out what&#039;s going on?

## Tools Used
SAN SIFT VM

## Skill(s)
Analyzing a Windows registry file

Basic Windows persistence knowledge and techniques

## Points
![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/a604e486-b35e-4871-b908-3e2b8ad406ce)

## Walkthrough

I want to try out the SANS Forensics VM for this task. It has a bunch of cool tools and cheat sheets I've never used before.

SANS SIFT Link: https://www.sans.org/tools/sift-workstation/

SANS SIFT workstation how-to video: https://www.youtube.com/watch?v=ai_7Fkv6igw

First, I need to transfer the file over to the SIFT Workstation.

![image](https://github.com/user-attachments/assets/509e27eb-65ce-44cc-ac12-fadc25b8a71c)

Alright. It's there. Now it's time to start the challenge. Let's see what's in the file.

![image](https://github.com/user-attachments/assets/89c4ac4a-eeb5-4a17-8658-1b23a0b87400)

It's a bunch of stuff I can't read. Let's pull some strings.

![image](https://github.com/user-attachments/assets/4bc2f358-6cf7-43cb-8ec6-90e5d276d56c)

Have some weird text here. Let's throw it into cyberchef.

![image](https://github.com/user-attachments/assets/1b2755da-c336-4f74-9a43-e675359b5bc8)

Used magic in hopes that it would find something useful, but I didn't get any recipes out of it. Would probably be useful to get the file type to know what I'm working with.

![image](https://github.com/user-attachments/assets/a85d324d-de8d-4a12-89c7-fb130aca9108)

![duh](https://github.com/user-attachments/assets/465fc447-672f-4a18-891e-2db77e6be1da)

Alright. Now I just need to google how to use this file. There is a way to use this through Linux, but I want to use the EZ registry tool so I'll have to use Windows.

![image](https://github.com/user-attachments/assets/c423cfbc-553d-4dd4-b284-a15fa9dd264d)

Open and load the "query" file into RegistryExplorer

![image](https://github.com/user-attachments/assets/0f88c6fc-dec5-4e84-a5f1-15c0d196ac06)

Now to look through all of this.

![image](https://github.com/user-attachments/assets/3cfc1378-9959-4d95-a604-d0868488277e)

This took a while but I found the key. I knew it was Microsoft from the file type. Root > Software > Microsoft 

![image](https://github.com/user-attachments/assets/2f395f12-3c02-421f-b097-9cbff1f76e7a)

Then Microsoft > Windows > Current Version. This has the most stuff in it to look at so I started there.

![image](https://github.com/user-attachments/assets/7f75c0db-b2fc-441d-8f7e-fcdb992921bd)

Check "Run" for Executables. There is one.

![image](https://github.com/user-attachments/assets/247895b0-166c-4a55-a7b8-c5dc682c2753)

That's an odd name for an executable. Let's throw it into Cyber Chef.

![who_are_you](https://github.com/user-attachments/assets/2641baae-d10b-4932-a4e6-d77bb18e912f)


![image](https://github.com/user-attachments/assets/670b8893-1b99-4a45-99c4-651eda68e564)

Using magic it's possibly encoded with Base64. Let's decode it from base64 in Cyber Chef.

![image](https://github.com/user-attachments/assets/34e5b42f-f2f7-420c-9eec-8c8b7ddefa63)

There it is!

![image](https://github.com/user-attachments/assets/dcb03a3f-1318-4477-8b36-60dc24509e0e)
