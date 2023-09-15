# Event Horizon
## Introduction
This is a write-up for the Hack The Box "Event Horizon" room. Let's get Started!

## Difficulty: Easy
![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/57607765-3009-4884-8243-1f79787dfb00)

## Description
Our CEO's computer was compromised in a phishing attack. The attackers took care to clear the PowerShell logs, so we don't know what they executed. Can you help us?

## Tools Used
Event Viewer

## Resources
Commando VM

## Skill(s)
Forensics 

## Points
![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/d8cc0871-1c77-4704-8717-397b1ac16217)

## Walkthrough

Download and unzip the file.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/5e7cee21-ecd3-499d-b22a-3c141bd1c56c)

The TraceFormat folder is empty, so I will just look at the logs. It took me 10 minutes of looking at events one by one to realize that an empty event was 68 kb...so I filtered the events by size and added those to my event viewer.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/35ad0e30-04af-4228-92b7-217208b7ad20)

Now instead of 300 somthing logs to look through I only have 28. Now that I've filtered out a lot of them I can actually start looking at the logs in depth. The description mentions the attackers went out of their way to clear Powershell logs so I will look there first.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/db1b5ab9-4c4e-4b12-8f6b-1a6bce5458e1)

Filter further by just looking at the "warning" levels.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/7702c4eb-3acb-4f51-a9cf-4f8e4107a476)

So we can see 2 dominant event IDs:
 - 1.) Event 4100
 - 2.) Event 4104

 We can also see that the attackers used mimikatz.

 ![waiting_gif](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/e4a07764-7536-417e-bd92-1d6a9a1095ba)

 This literally took me forever but I found it.

 ![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/66253311-e9ab-4a1a-9d2c-53df7eaac062)

The hint in the description helped, but if I didn't filter anything this would have easily taken the same amount of time as the first blood.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/43bfc9eb-5003-444e-8308-1f1eb058ee29)

