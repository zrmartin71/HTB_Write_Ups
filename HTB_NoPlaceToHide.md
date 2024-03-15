# No Place To Hide
## Introduction
This is a write-up for the Hack The Box "No Place To Hide" room. Let's get Started!

## Difficulty: Easy
![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/8e8dbe2b-8358-4b73-b971-3ed339511a81)

## Room Description
We found evidence of a password spray attack against the Domain Controller and identified a suspicious RDP session. We'll provide you with our RDP logs and other files. Can you see what they were up to?

## Tools Used
BMC tool

## Resources


## Skill(s)
Analyzing RDP cached bitmap files

## Points
![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/a604e486-b35e-4871-b908-3e2b8ad406ce)

## Walkthrough

Unzip the folder.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/4c2d1590-59ed-4419-9847-ab71de507b55)

We have two files here. Just gonna google what kind of data these files hold.

bcache24.bmc is a bit map file used for RDP. The following link explains this well.

Link: https://www.allthingsdfir.com/do-you-even-bitmap-cache-bro/

Their article mentions the BMC tool. I can use that to parse the bcache file and the Cache0000 file.

BMC Tool - https://github.com/ANSSI-FR/bmc-tools

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/2180693c-a5b9-4a52-bde3-39343eb65dd4)

Having trouble parsing the bcache24 file, but that could just be a user error. Let's try the other file and then go back.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/34cdcbc4-1f02-433e-ae11-85c2335cc80b)

Let's see what we have here.

![search_gif](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/08418d4b-cfd6-4be3-afa9-d8292a4bf275)
 
Oof...should've put that in a folder -___-

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/890686f7-67f1-461a-98aa-174fbaff7edd)

![facepalm_gif](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/e38f3f8b-6768-4ac0-8b07-f2024daa06f5)

Let's try this again.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/e5d35f8b-441e-4608-a8ca-bee9c478c882)

Alright, this is better, but I definitely broke something.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/2aa8fd49-ea6a-47d8-abed-46f51071910b)

After clicking through 1039 pictures we've found the flag. 

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/eea2af4d-36a9-4683-9050-be54ef7993a6)
![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/7dd3d694-96cd-43c0-9cff-244a2463dd48)
![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/e6b9723c-674e-4470-8f24-72e690af7b0e)
![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/39ffd05c-63fc-4b50-9f20-632c069bb888)
![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/a4552ca9-4f42-440d-b154-99f306155a92)

Done!

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/9f50ba06-2071-4c12-9208-ba4ed0ec2c81)



