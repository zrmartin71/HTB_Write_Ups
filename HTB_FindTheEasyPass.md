# Find The Easy Pass
## Introduction
This is a write-up for the Hack The Box "Find The Easy Pass" room. Let's get Started!

## Difficulty: Easy
![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/8f2054a4-6c52-4db5-8399-f9996ed6f58c)

## Tools Used
Ghidra

## Resources
A video guide that helped me install Ghidra: https://youtu.be/FceecDBW_N4  
FTEP Video Guide I used: https://youtu.be/_TTZxA6Plv0  
FTEP Text Guide I used: https://haxez.org/2021/09/hack-the-box-reversing-find-the-easy-pass-has-been-pwned/

## Skill(s)
Reverse Engineering

## Step 1
Download the file and move it to your VM. Enter the password provided on the information page to unzip the file. It should pop up after you've downloaded the file. 

 ![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/274823b8-9356-47d0-a2a7-20ebb50b65f6)  ![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/90da15ca-c0db-473b-84eb-21b1b8b53031)

 Once you've done that the Easy Pass.zip file should show up wherever you unzipped the file.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/181ef2a9-c170-4466-b8f6-78d0a0a79f4e)

## Step 2
I wasn't sure what to do after this, so I did a bit of Googling and found some guides that taught me how to use Ghidra for this room. They are linked in the Resources section. Both guides had teaching styles that were super helpful to me in learning how Ghidra works in this room!

Next, we will put the EasyPass.exe file into Ghidra. You can do this by File > Import File and then navigating to EasyPass file. A pop-up will show once the file has been imported.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/fe575c66-fde9-4cbe-bdaf-a7adb85164c4)

Click Yes and then I just let the default analysis happen.

Next, I searched for strings and used the default settings.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/32854fe0-7808-454c-b4b6-b662630cb8b3)

Then I searched for a password and got two hits

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/5852fda6-9577-4457-b2ab-49c2bfdb20c8)

From here I used the text guide. Select the first location 00454200. Then right-click 00454200. Select "References" > "Show References to Address"

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/7949afc8-da58-4080-a4ee-e8862d47341c)

In the write up they get two references, but I only got one.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/8cd6b744-7d1b-4844-89e0-011c2184989a)

Double-click the reference and you should have an output similar to the image below.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/6c3a52c1-8ba3-439d-a343-ffd8286daa0b)

After that, I selected the reference and then clicked the "Display Function Graph" button. In the text write up he calls it the "hierarchical order icon".

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/df87f4b4-976e-470a-a82f-707c58d7d0fa)

After you click that you should have an output like the image below.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/5ea1bc23-6b00-4e22-8092-96882f423e0f)

Then find the reference to the if statement in the function graph.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/013d72bc-e445-49f0-b9cc-c953ac760dfd)

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/cf1f31c3-4679-4b35-8abd-20cd1e25d7c4)

Make a note of the function number for the if statement "004540c4". 

At this point, the two write up kinda go different ways as far as what debugger to use. I used the one in the text because the one from the video just looked ugly. So I will be using Ollydbg. There are steps on how to install this in the write-up. However, I did run into issues installing Ollydbg on my Kali VM. I had to install wine and then install Ollydbg.

To install wine I followed the following links:
- https://www.sysnettechsolutions.com/en/install-wine-kali-linux/
- https://wiki.winehq.org/Debian

After that, I used "sudo apt install ollydbg" to install ollydbg.

Welp nvm for some reason EasyPass.exe completely farts out when I put it in ollydbg. So let's try something else.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/e3d0efa6-e95d-419b-bfe5-965792cf0540)

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/74f8815d-a7c9-4aad-acee-2563fa7c7037)

After (what felt like) hours of reading and watching different write-ups I found one that made this machine easy.

Security Sphinx: https://security-sphinx.medium.com/find-the-easy-pass-walkthrough-14571d5da3a4

If it wasn't for this write up I'd still be looking for the password.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/f933d5c8-97b3-47de-b770-ddbd103c1280)

They noted that there are letters not highlighted between the code. I swear I didn't notice this for hours until I read this write-up. Overall I wouldn't say this machine is for beginners. I feel like reverse engineering is an intermediate-level skill.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/c3eec145-3d67-48ec-bb75-222d424ec377)
