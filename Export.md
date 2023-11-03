# Export
## Introduction
This is a write-up for the Hack The Box "Export" room. Lets get Started!

## Difficulty: Easy
![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/b1ed8027-b0d3-48f7-9613-13aca912f64f)

## Description


## Tools Used
Volatility

## Resources
Commando VM

## Skill(s)
Forensics 

## Points
![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/d8cc0871-1c77-4704-8717-397b1ac16217)

## Walkthrough

When you unzip the file you get a single .raw file. It is a Windows memory file. After some research I found that you can open this file with a tool called Volatility.

Link to info - https://www.magnetforensics.com/docs/axiom/html/Content/en-us/acquire-computer/loading-memory.htm

I followed this video to install Volatility - https://youtu.be/-bMde2glwnE?si=hsv--G1GvZnO_p6t

I used the Volatility Windows documentation to learn how to use the tool - https://volatility3.readthedocs.io/en/latest/getting-started-windows-tutorial.html

I am going to use the windows.pslist command to see what processes were running at the time of the memeory dump.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/7ff1b61d-1c10-47e0-93e8-4b34a153a030)

I didn't see much here other than when they used a tool to caputure the memory dump.

I'm going to run the help command to see what else I can do in Volatility.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/c8df88d6-ba3f-48ac-b7b0-cd13fbf923ed)

The windows.cmdline.Cmdline looks interesting. Let's check that one out.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/87b92f32-2869-4858-a895-9fe83071140f)

Not much here either.

![thinking](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/5e423bac-1cd1-446e-a24a-2e51297d7ce1)

Let's try windows.info

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/9e70e9ed-fe62-4a91-9c53-57b4d8fb2c5e)

After looking up what most of these fields, I now know that this is a Windows 7 machine.

Build wiki page - https://betawiki.net/wiki/Build_lab#:~:text=Originally%2C%20a%20build%20lab%20was,official%20builds%20of%20Windows%20NT.

Alright, so i took a look at every walkthrough I could find for this challenge and everything uses Volatility 2, but there are no new write ups after May 2023. I also haven't been able to get my hands on the source code for Vol 2. It just redirects to the download page when you click it to get the source code.

![trash](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/0d5bfa35-2451-4041-aa87-67ad04d4bc91)

I found a work around for not having a Vol 2 copy. SANS SIFT work station has a copy of Vol 2. Now I'm just having a issue with the .raw file itself.

SANS SIFT - https://www.sans.org/tools/sift-workstation/

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/6df832dc-4c65-48a3-96c1-8b094c78e998)

It seems that after I changed the filename and used .001 for the file extention it worked. I came to this conlusion after i saw other .raw files with a similar extention.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/4e626a5f-e7e3-4ed5-87da-787a7e6c8481)

Now I'm starting to get the same output as the offical walkthrough.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/049b122e-72d3-4c1a-b34e-c4ae90ae32d9)

Going to take this highlighted part from the output and put it into cyberchef.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/e8e5b5db-10e6-4102-a69a-9933bbcbe071)

Finally! This took way longer than i expected lol.

![celebration_yes](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/65a755f9-3722-410a-81ba-9891a8e726b7)

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/c2014dbc-ba1c-49b2-95c8-69a2c0a12862)
