# WeakRSA
## Introduction
This is a write-up for the Hack The Box "Weak RSA" room. Let's get Started!

## Difficulty: Easy
![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/70bf0943-a21b-4987-b7bd-ce00c17d3dc2)

## Tools Used
Libre Office

RSA tool
## Resources
Link to RSA tool - https://github.com/RsaCtfTool/RsaCtfTool

Link to learn more about RSA - https://www.encryptionconsulting.com/education-center/what-is-rsa

## Skill(s)
Cryptography

## Step 1
Unzip the file with the password provided when you downloaded the file.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/96efb711-36c1-4795-9074-f51d44ff586a)

You will get two files. To view the key.pub file I downloaded libre office onto my kali vm. 

- sudo apt update
- suod apt install libreoffice

Once LibreOffice is installed you can view the key.pub file.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/28127fef-9a99-4967-9a16-c6ed1566c97f)

IDK what to do from here, so I googled "how to crack weak rsa" and this tool pops up.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/be8982dc-178b-4d17-8992-2743a390cab4)

Let's give this a try. 

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/77c2d448-5a25-4288-b154-a71e88c3c05b)

After running the installation commands the tool opens with its help page.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/78e7adf1-e483-4665-a284-d09b8fc07a93)

You can uncipher files using the RSA tool with the following command:
- ./RsaCtfTool.py --publickey ~/Desktop/key.pub --uncipherfile ~/Desktop/flag.enc

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/e2ddf268-7595-461f-9e26-d55b1e184a5b)

Completed!

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/9df55c48-25e0-4205-8f4e-f8fd32217b3c)
