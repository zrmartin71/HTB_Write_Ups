# Lure
## Introduction
This is a write-up for the Hack The Box "Lure" room. Let's get Started!

## Difficulty: Easy
![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/2b41ab99-7a3a-4d0d-b680-264248d47a01)

## Room Description
The finance team received an important looking email containing an attached Word document. Can you take a look and confirm if it's malicious?

## Tools Used


## Resources


## Skill(s)
Basic malicious Word document analysis, Basic PowerShell deobfuscation

## Points
![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/a604e486-b35e-4871-b908-3e2b8ad406ce)

## Walkthrough

Download and unzip the challenge file.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/8c79b4d2-2e8b-48de-a158-c240708e0e4f)

Here is the document mentioned in the description. Let's open it.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/7a6c5739-c2c4-41e9-a323-75112a424a40)

Not gonna lie if I didn't know any better I would probably click enable editing, but that doesn't matter in this case because we know the file is sus.

![sus_gif](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/03c90288-cae6-4f9d-911e-e26a67f9c176)

Now let's extract the macros using olevba.

```
sudo -H pip install -U oletools
```
![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/0372e8cf-a3bc-4e14-a36a-132a9c1fe0dd)

Extract the macros using olevba.

``` 
olevba UrgentPayment.doc
```
![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/b173eeb4-1f6a-474c-8dea-3590b5c2a8d3)

Certified Sus document smh.

![sus_gif2](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/3c6498cc-09d4-42aa-badd-4095f895702b)

I have a few keywords highlighted in red. Investigating the "shell" and "powershell" keywords are somthing worth looking into. Lets decrypt the text in that area.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/a802653a-fe9c-4f3c-9d8e-fd5fd5bed8b5)

Using magic in cyber chef I can see that base64 is being used. Lets now decode the text from base64.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/cec1705f-4c0b-4b89-86f3-640b8e6ab0ba)

Its a little more readable now, but not what I'm looking for. Let's use the search fuction in cyber chef to help with decoding it further.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/9bb5e4f0-0744-477f-80d2-f0dcfdc3251b)

That's even better. Now copy and paste the yellow part of the output into powershell.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/6bd2a475-9e31-4554-b448-e5e527180adf)
 
Got the flag but it's still a bit murky. I can throw the url back into cyber chef and see if that works.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/fd5ffd80-a74f-4528-90ae-5f99fa96b075)

Got it!

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/3c00232c-cf4d-4055-b323-e5b4722db127)

