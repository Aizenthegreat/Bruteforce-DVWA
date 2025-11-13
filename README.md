# Bruteforce-DVWA
brute force walkthrough using burpsuite

In this demonstartaion as per the title. I will demonstrate a brute force login using DVWA using only burpsuit. 
Without further ado, lets get started.

1. Start your VMs (recommended two: attacker + target).

Start Docker and DVWA on the target VM.

Example: DVWA available at http://<VM_IP>:8080.
   - ![Screenshot 2025-11-02 220538](https://github.com/user-attachments/assets/81d646b7-374f-4f98-a736-e3e6b7efdbd8)
     
2. configure Burp & browser proxy

in Burp → Proxy → Options: confirm a listener (e.g., 127.0.0.1:8080).

configure your browser to use that proxy (or use Burp’s embedded browser).

go to Proxy → Intercept and turn Intercept on (we will capture one request).
  ![Screenshot 2025-11-02 220748](https://github.com/user-attachments/assets/9bc47094-d72b-4277-a5aa-1e2d9d9e77e9)
  
browse to DVWA and log in (any creds) to capture the POST request. Burp will show the login request with username and password fields.

- ![Screenshot 2025-11-02 220953](https://github.com/user-attachments/assets/f57f8160-4edf-4082-b9d2-82ede3a22ff7)

3. send request to Intruder & select position(s)

right-click the captured login request → Send to Intruder.

open Intruder → Positions. Click Clear § to remove auto positions.

highlight only the password value and click Add § (so only password is a payload). Don’t include surrounding form names or other params.

attack type: Sniper for single position brute-force. If you want to brute-force username+password combos use Cluster Bomb with two positions.
  - youll see in burpsuite that the login was captured. if you click on it, youll see your username and password.
    ![Screenshot 2025-11-02 223132](https://github.com/user-attachments/assets/9bc8beec-a402-4a4b-9610-b646f9fe734d)
    
  
 ![Screenshot 2025-11-02 223404](https://github.com/user-attachments/assets/03b3085c-78fc-4ec0-a96c-80fe966df97f)
- now create another tab and create a file with random passwords. preferably ones that are very common. we'll head to payload config in intruder and upload that file.
- ![Screenshot 2025-11-02 224053](https://github.com/user-attachments/assets/e46edb5b-8e7b-4cb0-b038-d737bfe94f9e)
- Almost done!, lets go into the code of the webpage where we tried to loginto with our fake credentials. scroll down and find the error message we would get if we were to put in the wrong credentials. copy it and paste it into "Grep - Match"
![Screenshot 2025-11-02 224508](https://github.com/user-attachments/assets/91d9f54d-7f0b-441b-9b86-983e8d68b40c)
![Screenshot 2025-11-02 224701](https://github.com/user-attachments/assets/7e2709e7-29e7-4709-8345-2db35b8d295b)

  - This will tell Burpsuite to flag this reponse if given
    

4. start the attack safely

turn Proxy → Intercept off so automated requests aren’t held.

in Intruder click Start attack. Watch results. Community edition is single-threaded and slow; be patient or use smaller lists.

monitor for: responses that do not contain the grep failure string, responses with different Response length, or responses with redirect codes (3xx). Those are candidate successes.

5. inspect candidate results & verify

click a promising result → view full request/response. Confirm the request body shows the username and the candidate password. 

![Screenshot 2025-11-02 224943](https://github.com/user-attachments/assets/950414c5-02cb-465a-bf39-f62927005bb3)


copy the discovered credentials and test them on DVWA’s login page.

![Screenshot 2025-11-02 225051](https://github.com/user-attachments/assets/94ae8f82-79a3-47b2-88fb-c8b0241b954b)

  Bingo!!!
 







