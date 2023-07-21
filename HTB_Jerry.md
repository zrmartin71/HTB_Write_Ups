# Jerry
## Introduction
This is a write-up for the Hack The Box "Jerry" room. Let's get Started!

## Difficulty: Easy
![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/0b8dc803-47b5-427e-b44d-7c833c12fdf1)

## Tools Used
Nmap, Metasploit
## Resources

## Skill(s)
Web, Vulnerability Assessment, Java

## Walkthrough
Starting off with a Nmap scan I can see that tcp port 8080 (http) is open and running Apache Tomcat.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/8749a4ba-d8ae-4ce3-9c00-60996ec1dd70)

My brain got stuck on what to do after this because my Firefox kept timing out when I put in the IP address. After going back and reading some of the starting point content I realized that I could add the listening port to the end of the ip.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/d8540962-fc3a-4218-b00c-a9584da17539)

Now I can see that it is a webpage for Apache Tomcat.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/c1f8aefa-e4c1-4fd7-adbf-ac4ec35fecb9)

Got stuck again, but this time I read the review section on the machine. I watched the official walkthrough video and he was just doing too much. A user said this can be done with Metasploit so I gave that a try.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/4a767732-5b2f-4d6f-bfa8-3808e54721ea)

First I searched in Metasploit for "Apache tomcat manager" because the manager app button and host manager button throw a 403 "Access Denied" error message.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/c73960ff-3de3-4d2f-a264-977638015660)

I am going to try to use option 2 since remote code execution is a vulnerability for this machine.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/ca1713bf-d34c-4f73-bb5d-670978ed7b18)

I am choosing the authenticated version since I used the default login admin:admin to gain access to other parts of the web page. Plus Default creds are also a vulnerability for this machine.

So as far as setting everything up for this exploit I had to google it lol. Found this write-up on how to set up the reverse shell.

- Ethical Hacks - https://ethicalhacs.com/jerry-hackthebox-walkthrough/

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/b60461d3-90e4-4b0c-94d8-738bdbf3c798)

The user name and password here are pulled from the 403 error mentioned earlier.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/79443582-f843-4c9b-97f2-1826a8ca0847)

Then type shell.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/daec55ff-0f34-464d-983e-be213d134ca2)

After that, I navigated through the files until I captured the flags.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/07041b42-cbf1-411b-921e-4bc1bd6c5735)
