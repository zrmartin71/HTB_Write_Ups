# Ransom
## Introduction
This is a write-up for the Hack The Box "Ransom" room. Let's get Started!

## Difficulty: Easy
![image](https://github.com/user-attachments/assets/28294cfd-f93d-493e-9964-3f84cc7e7dcb)

## Room Description
We received an email from Microsoft Support recommending that we apply a critical patch to our Windows servers. A system administrator downloaded the attachment from the email and ran it, and now all our company data is encrypted. Can you help us decrypt our files?

## Tools Used


## Skill(s)
Reading optimized code
Writing a ransomware decryptor

## Points
![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/a604e486-b35e-4871-b908-3e2b8ad406ce)

## Walkthrough

I am extracting the file contents.

![image](https://github.com/user-attachments/assets/e06c0fbb-78b2-4903-8c72-4a7e67100f98)

I tried opening the "login.xlsx.enc" file in Wireshark, but I got an error saying that the file is not in a format Wireshark understands. To Google, we go cause the guide for this is no help. 

![waiting_gif](https://github.com/user-attachments/assets/91cf1bf9-ce5d-4487-9ba0-5be9bbbdb72e)

So I need to use ghidra for this. According to the guide for the box, you need basic decompiler skills. So let's try putting the .exe file in ghidra and see what I get.

Ghidra was a pain in the ass to install, but this video made it easy: https://www.youtube.com/watch?v=rt6Z_ph8ZAg

![image](https://github.com/user-attachments/assets/9d70ef1f-668c-4667-b5d8-8ab902ef9bbe)

Nice, I'm up and running...Now to learn how to decrypt the file. Gonna search for anything in the code that has to do with encrypting or decrypting.

![image](https://github.com/user-attachments/assets/83008f18-b9a5-4e48-8b07-80107207b20e)

Let's select the first one and see what I can understand.

![image](https://github.com/user-attachments/assets/651748e6-1537-49e0-baa8-8c01f108281a)

![image](https://github.com/user-attachments/assets/530392c2-243e-4225-affc-651678b8d442)

![image](https://github.com/user-attachments/assets/6a6f7518-1e04-4d2a-a643-ad4027caf496)

After mousing over the variables used in the encryption code, I see that the hex translates to "SUPERSECRUE" or "super secure". I did see this when I pulled strings from the "login" file.

![image](https://github.com/user-attachments/assets/a5e10df5-7d26-48e3-8e7c-b56e5538b6b1)

You see it quite a few times at the end of the file. I didn't even notice.

In this video (https://www.youtube.com/watch?v=7ev6Iq4gpTE) they used a Python script to decode the file, but couldn't get the byte array error to go away. I will use the same script, and see if I can solve the issue.
