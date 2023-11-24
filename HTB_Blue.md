# Blue
## Introduction
This is a write-up for the Hack The Box "Blue" room. Let's get Started!

## Difficulty: Easy
![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/21a49280-314e-4028-9e57-11d78f0ed1f1)

## Room Description
Blue, while possibly the most simple machine on Hack The Box, demonstrates the severity of the EternalBlue exploit, which has been used in multiple large-scale ransomware and crypto-mining attacks since it was leaked publicly.

## Tools Used
Nmap, Metasploit

## Resources


## Skill(s)


## Points
![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/a604e486-b35e-4871-b908-3e2b8ad406ce)

## Walkthrough
Nmap scan

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/3145c67c-f8a9-4c3d-98d2-cbe97c185c9c)

Let's see what shares I get with SMB Client.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/7cb4f49b-19c8-4e5a-aaf0-e3d2f4a64d5c)

Load up metasploit to use EternalBlue

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/4c933405-3f64-45b8-a5a7-605459a062e9)

Set options

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/cffa860b-c778-43bc-93e5-66c6eca650cd)

Sweet! I'm in!

![yes_meme_gif](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/a24ecfa5-2b91-4d31-adc3-84eba37a6e5c)

Time to look around.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/ad799a53-2073-4153-b523-4f3f64acf9a8)

User Flag acquired.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/db525c1c-239b-4950-9b5b-582eeb071c4f)

Root Flag acquired.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/fca85ba9-c100-42f3-8bff-a9cf0a8d8569)

Blue Pwned!

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/27c59450-ee1c-40a4-853b-2af4e49d1659)

This is the most script kiddie thing I've ever done XD. A win is a win ¯\\\_(ツ)_/¯

![win_gif](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/adc16bc9-3b19-4e99-92ae-78b94b3aa4d1)

