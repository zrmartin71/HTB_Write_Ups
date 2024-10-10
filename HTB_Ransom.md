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
Malware Analysis

## Points
![image](https://github.com/zrmartin71/HTB_Write_Ups/assets/54414820/a604e486-b35e-4871-b908-3e2b8ad406ce)

## Walkthrough

Extracting the file contents.

![image](https://github.com/user-attachments/assets/e06c0fbb-78b2-4903-8c72-4a7e67100f98)

We have an encrypted excel sheet and an executable. Now to figure out how to decrypt this. To Google!  

![waiting_gif](https://github.com/user-attachments/assets/91cf1bf9-ce5d-4487-9ba0-5be9bbbdb72e)

So I need to use ghidra for this. According to the guide for the box, you need basic decompiler skills. Let's try putting the .enc file in ghidra and see what I get.

Ghidra was a pain in the ass to install, but this video made it easy: https://www.youtube.com/watch?v=rt6Z_ph8ZAg

![image](https://github.com/user-attachments/assets/9d70ef1f-668c-4667-b5d8-8ab902ef9bbe)

Nice! I'm up and running...now to learn how to decrypt the file. Gonna search for anything in the code that has to do with encrypting or decrypting.

![image](https://github.com/user-attachments/assets/83008f18-b9a5-4e48-8b07-80107207b20e)

Let's select the first one and see what I can understand.

![image](https://github.com/user-attachments/assets/651748e6-1537-49e0-baa8-8c01f108281a)

![image](https://github.com/user-attachments/assets/530392c2-243e-4225-affc-651678b8d442)

![image](https://github.com/user-attachments/assets/6a6f7518-1e04-4d2a-a643-ad4027caf496)

After mousing over the variables used in the encryption code, I see that the hex translates to "SUPERSECRUE" or "super secure". I did see this when I pulled strings from the "login" file.

![image](https://github.com/user-attachments/assets/a5e10df5-7d26-48e3-8e7c-b56e5538b6b1)

You see it quite a few times at the end of the file. I didn't even notice.

In this video (https://www.youtube.com/watch?v=7ev6Iq4gpTE) they used a python script to decode the file, but couldn't get the byte array error to go away. I'm going to use the same script and see if i can solve the issue.

Oooorrrrr...I can have AI write break it down and write it for me.

![idea](https://github.com/user-attachments/assets/6e64a240-e400-42c1-b44e-36cd383f520d)

```
def decrypt(data, key):
  """Decrypts the given data using the specified key."""
  decrypted_data = bytearray()
  for i, byte in enumerate(data):
    decrypted_byte = byte ^ key[i % len(key)]
    decrypted_data.append(decrypted_byte)
  return decrypted_data

# Replace with the actual encrypted data
encrypted_data = b"your_encrypted_data_here"

# Key derivation (adjust as needed based on the actual key generation logic)
key = b"your_derived_key_here"  # Replace with the derived key

decrypted_data = decrypt(encrypted_data, key)
print(decrypted_data.decode())

```

Alright. Here's the code Gemini made for me. It's basically the same as the one in the video, but let's see if this runs into the same issue.

![image](https://github.com/user-attachments/assets/7b98f03a-c18a-4e62-83ac-828ad2c99c2a)

Not what I'm looking for. Let's make some changes and see if it works.

```
def decrypt(data, key):
  """Decrypts the given data using the specified key."""
  decrypted_data = bytearray()
  for byte in enumerate(data):
    decrypted_byte = byte ^ key[i % len(key)]
    decrypted_data.append(decrypted_byte)
  return decrypted_data

# Replace with the actual encrypted data
encrypted_data = b"login.xlsx.enc"

# Key derivation (adjust as needed based on the actual key generation logic)
key = b"SUPERSECURE"  # Replace with the derived key

decrypted_data = decrypt(encrypted_data, key)
print(decrypted_data.decode())

```
Back to the drawing board.

```
import base64

def decrypt(data, key):
  """Decrypts the given data using the specified key."""
  decrypted_data = []
  count = 0
  for byte in data:
    decrypted_byte = ord(byte) - key[count % len(key)] #Grabs ascii value of byte then subtracts key for byte
    decrypted_data.append(decrypted_byte)
    count+=1
  return decrypted_data

def decryptedToChar(data2):
  #Returns data back to ascii value
  output = []

  for i in data2:
    letter = chr(i)
    output.append(letter)
  return output

# Read the encrypted file
file = open('login.xlsx.enc', 'r', encoding='ansi')
encrypted = file.read()

# Key derivation (adjust as needed based on the actual key generation logic)
key = list(b'SUPERSECURE')  # Replace with the derived key

decrypted_data = decrypt(encrypted, key)
print(decrypted_data)
n = decryptedToChar(decrypted_data)
print(n)

```
Made a little more progress. I got the same output as the video. I'm satisfied with this but I'm going to find a different approach so I can move on.

This video (https://youtu.be/VLPsY14blnA?si=EJe3rrOTWQ1COf7J) shows how to decrypt the file in cyberchef.

First, I have to upload it as a file and use SUB with the key I found from Ghidra.

![image](https://github.com/user-attachments/assets/ccc8c675-d25d-4c64-8b67-efbc8498b0c2)

To verify that the file is decrypted we need to see the highlighted string above. Now I save the file as a new document.

![image](https://github.com/user-attachments/assets/6100574d-0aab-42e2-8de5-b2de8814941a)

We can open the file in Kali with Libre office and boom we've captured the flag.

![image](https://github.com/user-attachments/assets/be26c3b5-9d86-4be6-b7ce-6abf97b382a1)


![image](https://github.com/user-attachments/assets/80b7d10b-1f2f-4195-8f4f-088aa6e1c2a3)
