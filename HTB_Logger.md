# Logger
## Introduction
This is a write-up for the Hack The Box "Logger" room. Let's get Started!

## Difficulty: Easy
![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/7457043a-f953-43ee-996d-2311f0a112d3)

## Room Description
A client reported that a PC might have been infected, as it's running slow. We've collected all the evidence from the suspect workstation, and found a suspicious trace of USB traffic. Can you identify the compromised data?

## Tools Used
Wireshark

## Resources


## Skill(s)
Analyzing USB traffic, Recovering pressed keys from captured USB traffic



## Points
![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/a604e486-b35e-4871-b908-3e2b8ad406ce)

## Walkthrough
New day, new skill. I will be following the offical walkthrough for this room since I am not familiar with how to analyze USB traffic.

The write up mentions 5 "GET Requests" and 5 "GET response" for devices.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/1ab14b5b-b0a1-4065-874a-5b7e75a7a42a)

Here are the 5 requests.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/3cc6d6ba-9889-47e5-a4a3-832776e90690)

Here are the 5 responses.

Next, the walkthrough identifies devices with the most traffic. According to the walkthrough, those are device addresses 13 and 16.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/a5a4d413-d7e7-4857-aaa7-585769adc58c)

I found the device address, but didn't see the "device description" section he mentioned. However, when I clicked the hyperlink "Response in: 8" I was able to find the frame that has that section.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/ba919e9e-4aa2-467d-b109-fe5310682ecc)

Now I need to find device 16.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/4d512420-5c91-44fc-bc33-b2eae12f4990)

Device 16's response frame.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/a12ff18a-af7d-4d08-90e1-8cdae4ba56a2)

Next I need to look at frames from the keyboard and find the ones that have HID data.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/4f12ac54-90eb-4597-944a-7a425942e2ef)

All of these frames have HID data. Now I need to use tshark to run the following command.

```
tshark -r keystrokes.pcapng -Y 'usb.device_address == 16 && usb.data_len == 8' -Tfields -e usbhid.data | sed 's/../:&/g2' > loggerData
```

if you just run the following command...

```
tshark -r keystrokes.pcapng -Y 'usb.device_address == 16 && usb.data_len == 8' -Tfields -e usbhid.data | sed 's/../:&/g2' 
```

You should get this output.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/6f644f12-9906-4c71-a72b-76c527b79b6d)

Which grabs the hid data section of each related frame. You can also put this infomation in a .csv file like this...

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/99a0c1af-be1f-4084-978d-8307f2fabb56)

But the data came out weird for me. It is 100% user error cause i'm not familiar with libre office formatting. However the tshark command is easier in my opinion.

Now I am going to use this CTF script: https://github.com/TeamRocketIst/ctf-usb-keyboard-parser to process the data.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/619b9973-295e-4c1f-8944-690974eaed35)

Enter the command as directed with the loggerData file I made.

``` 
python usbkeyboard.py loggerData 
```

Got the flag.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/ae424cce-18b4-48af-92bb-e9a834c69b43)

Now I just have to clean it up and submit.

![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/0656f56a-5bc1-40a6-b239-27a46e322e8f)
