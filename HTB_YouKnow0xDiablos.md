# You Know 0xDiablos
## Introduction
This is a write-up for the Hack The Box "You Know 0xDiablos" room. Let's get Started!

## Difficulty: Easy
![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/9f5b5793-01ca-4944-b4a0-86c7f937fe8f)

## Tools Used
7zip

## Resources
CTF101 - Binary Exploitation: https://ctf101.org/binary-exploitation/overview/

## Skill(s)
Binary Exploitation

## Points
![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/445ed87b-c0e2-42a3-af54-5fa0d72294dd)

## Walkthrough

To start off I downloaded the files I needed and started the instance. When I try to unzip the file it's skipped.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/5ccb347b-5bb6-4c10-a34b-193236a59740)

So I'm just gonna google what this error is...

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/300cc683-acf8-42a2-9488-9efc6e9450f9)

I found this link that helps with opening the file.
 - PK compact error: https://unix.stackexchange.com/questions/183452/error-trying-to-unzip-file-need-pk-compat-v6-1-can-do-v4-6

I used the following command to unzip the file.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/73906017-3805-475b-949c-7e65490ddee5)

Once I unzipped the file there was a file called "vuln" extracted.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/9f0295c3-3e45-4ab4-b16a-e5e372b4ebb0)

I used the file command to see what kind of file it was because I wasn't sure. 

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/235239c2-a44c-4a1a-bc21-69adf59cff6d)

I can see the file is an executable, but I needed to chmod+x to make the file executable. Once again, I am not sure what to do at this point, so I googled for more information on the challenge type.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/07347f5b-7d9f-4840-9c23-a94fba81e172)

Alright, sooo binary-exploitation... never done that before so back to Google we go.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/300cc683-acf8-42a2-9488-9efc6e9450f9)

I know Ghidra can analyze files, but I am not familiar with everything it can do. At least I can see what the program is now lol.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/376d5244-97e2-414a-8c26-019b8f535311)

I did a search for strings and my 4th result was a line that had 'flag.txt' in it. Let's take a look there.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/ac9823eb-77b9-45ed-be29-b5303987cc8f)

Alright here's what we got... I kinda understand what's going on here, but not really.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/39383749-ad08-4739-a2f5-a0baa120289b)

Back to uncle google...

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/dc0a1314-1cfb-4f0c-9d8e-29271a5aec33)

So after about 3 hours of googling and learning about binary exploitation, I caved and found a walkthrough. After this box, I definitely need to gain more experience with binary exploitation.

I learned ALOT from this walkthrough: https://weshsec.medium.com/htb-you-know-0xdiablos-4ad297fe75c0

So the point is to do a buffer overflow attack. The walkthrough uses GDP-peda so I will do the same.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/d5b9c426-4e9f-4792-965d-6e6abe52afac)

I got the first breakpoint. Now I can create the file to find the EIP offset.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/b5cbd30c-32c9-4909-a86e-7492f2c20b78)

Next, I run r < pat.txt.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/01cc1b65-ca5e-4c64-9750-89feeb6781ae)

Finding the offset for the EIP register.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/8e8769f8-bb4e-4fd9-8280-7517a98e70f7)

Next, I disassemble the flag function.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/29201594-68cf-4693-a14e-ca8187c41db3)

Then generate the payload.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/02ee5405-6181-4d08-8633-13fca4cdfd43)

Pipe the cat output of the payload to the vuln executable. I guess this step checks to see if it actually works. Then it tells you to do the same thing but to the server ip provided at the beginning.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/4cde04dc-d9b6-4102-913c-4205736e5d8c)

Now I'm trying the same thing but with my server IP address via Netcat.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/ddc57c10-6476-4aa8-9d44-e8939dc8b168)

That method didn't work. I found another way to do this via a Python script from this write-up: https://haxez.org/2023/03/hack-the-box-you-know-0xdiablos-writeup/

Once I copied the script and made the changes needed, I captured the flag. 

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/6acff6fa-ef84-4e60-bfd6-e636b6eb75cb)

## Review
This was an interesting machine. I've never tried binary exploitation and have a lot to learn. I should also probably pick up Python so that I can write my own scripts or understand what other scripts are doing. Overall, I would say this was not too easy lacking all the knowledge I needed. I feel like this would be easy for someone who goes through the HTB Academy since they cover binary exploitation there. However, since I only used the starting point section it was a huge learning curve for me.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/a304ddde-c896-4368-9061-4f59306e13bf)
