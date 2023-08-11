# Netmon
## Introduction
This is a write-up for the Hack The Box "Netmon" room. Let's get Started!

## Difficulty: Easy
![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/355b8dc6-5a15-4934-b52e-08b71ed27c66)

## Tools Used
nmap, libreoffice

## Resources


## Skill(s)
Vulnerability Assessment, Windows Exploitation, Enumeration

## Points

## Walkthrough
For this walkthrough, I am going to follow the new guided feature for VIPs.

## Task 1 - What is the name of the application running on port 80? Given the three words in the logo.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/8d07c264-df22-4752-b13e-f4e3dbdb078f)

If you run an Nmap scan it doesn't show port 80. Took me a second to understand what they're looking for, but you just have to type the IP into your browser to get the answer for this one.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/4ec917bb-da03-4493-89e5-0d000d0ebcbb)

### Answer: PRTG Network Monitor

## Task #2 - What service is running on TCP port 21?

### Answer: ftp

## User Flag

For this, you need to log in with anonymous.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/73ff4d98-9c37-4814-ac12-b8c17cc6bcca)

Then look through the folders until you find the user flag.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/b098862f-44d1-45a3-852d-f883d679c3a2)

## Task 4 - What is the full path of the folder where PRTG Network Monitor saves its configuration files by default?

Just gonna Google where to find PRTG configuration files.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/73d4aeb8-0a03-4199-8fbd-c8cd4ea81554)

Just gonna go for this first link here.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/347aa472-d3ec-4013-8030-40f369188e64)

I saw in the Nmap scan that Windows server 2008 R2 is on port 445 so the config files will be stored in programdata\Paessler\PRTG Network Monitor. Program data is a hidden file in the C drive. To get the full path for the answer you have to put C:\programdata\Paessler\PRTG Network Monitor.

### Answer: C:\programdata\Paessler\PRTG Network Monitor

## Task 5 - What is the name of the backup config file?

Navigate to the PRTG Network Monitor Directory. Once you're there you will see a list of files 3 of which have the same name. However, the one you want is the one that has .bak. The .bak file extension means that the file is a backup file.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/41b00228-c016-4be6-8869-9d6952a53acd)

### Answer: PRTG Configuration.old.bak

## Task 6 - What was the prtgadmin user's password according to that file?

Gonna grab the file.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/e3c87b5e-bf0f-4ed0-a9a5-a6e1d51eec96)

Then open it with LibreOffice and search for "prtgadmin".

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/db5fae9d-efe0-4400-901f-d090decc8a0e)

### Answer: PrTg@dmin2018

## Task 7 - What is the prtgadmin user's password on the website now?

If you used the password found in the last task it doesn't work. Just add a year and boom!

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/5549bc85-d4bc-4b09-bdaf-ee78e7967ead)

### Answer: PrTg@dmin2019

## Task 8 - What version of PRTG is installed?

### Answer: 18.1.37.13946

## Task 9 - Which user is this software running as by default? Don't include anything before a `\`.

After a few minutes of digging around the website, I decided to take a look at the hint.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/61e7b6f6-a299-43cd-a11f-b4fd64dc5287)

With a Google search, I found CVE-2018-9276. I can do an OS command injection vulnerability via notifications.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/63f41a4f-2dbb-44d0-bf71-5c9e523e3c72)

The setup pages have a notification section.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/10fce11f-05ac-46ed-a196-46a8455f0b9c)

Created a new notification and set the parameter

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/36d0b112-440f-4613-95a1-333bd7a71fb2)

I ran into some issues using psexec.py. The was a lib causing an issue, so I decided to use the Metasploit exploit mentioned in the CVE.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/5df8685f-74a5-49bb-8dbe-668f2a1b3a44)

Now time to set up the exploit.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/60c5a671-1a72-4348-852a-a04540669b4c)

Setting parameters

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/5869c788-05ae-4b5c-a342-e0552fefa45b)

Now I'm all set up.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/dbbee31e-7889-45e9-8955-628b2a52143d)

Run a check and run.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/7a469d40-5a05-48b9-b10f-27ccc29abfa3)

There's our answer.

### Answer: System

## Root Flag

From here I just need to look around and find the root flag...

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/03907440-fa61-4376-97a6-b39845302389)

Got it!

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/598eb458-8f23-44ec-86ab-5588f2f27eb8)

Another Machine Pwned!

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/0217fb04-fcae-496f-a032-f43c9dd9204d)

## Review of Guided Mode

I enjoyed using the guided mode. It is VERY similar to how Try Hack Me has its learning platform setup. It doesn't give you all the answers but has hints to get you moving in the right direction. I tried the guided mode for Jerry, but I don't think the hints for the machine we're useful enough for me to use for a review. So the biggest issue I see with the guided mode is who is writing it. Although something might be intuitive for the writer might not be for the learner. In my opinion, Netmon is a good machine to use the guided mode for. It seems like the creator had a good idea of the scope of their audience. Because of that, I think this machine fits perfectly in the beginner track. You can complete this machine if you haven't done the academy and solely used the starting point machines to begin your pen-testing journey. 
