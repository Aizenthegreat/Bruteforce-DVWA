# Bruteforce-DVWA
brute force walkthrough using burpsuite

In this demonstartaion as per the title. I will demonstrate a brute force login using DVWA using only burpsuit. 
Withou further ado, lets get started.

1. start up your VMs(recomended to use two). remote into one through cmd and use the other one will be the envirnment that we will use for the attack.
   - start up docker and dvwa 
   - ![Screenshot 2025-11-02 220538](https://github.com/user-attachments/assets/81d646b7-374f-4f98-a736-e3e6b7efdbd8)
     
2. now in the VM that you will be conducting the attack on, head to the left side bar and fire up burpsuite. 
- head to proxy, turn on intercept and open browser
  ![Screenshot 2025-11-02 220748](https://github.com/user-attachments/assets/9bc47094-d72b-4277-a5aa-1e2d9d9e77e9)
- once your in the browser, head to DVWA and login (remember its, http://VM_IP that dvwa is initialized in:8080)
- once your logged in you can see burpsuite capture traffic from your login. itll look something liek this.
- ![Screenshot 2025-11-02 220953](https://github.com/user-attachments/assets/f57f8160-4edf-4082-b9d2-82ede3a22ff7)

  3. once your logged into DVWA, click on brute force and youll see a login prompt. try logging in with random credentials.
  - ![Screenshot 2025-11-02 222944](https://github.com/user-attachments/assets/05262b49-2787-42f7-93b3-1e41cdbe4b2d)
  - youll see in burpsuite that the login was captured. if you click on it, youll see your username and password.
    ![Screenshot 2025-11-02 223132](https://github.com/user-attachments/assets/9bc8beec-a402-4a4b-9610-b646f9fe734d)
  -now were going to click it and forwad it to intruder. Once inside intruder, highlight your password that'll be between $ signs.
 ![Screenshot 2025-11-02 223404](https://github.com/user-attachments/assets/03b3085c-78fc-4ec0-a96c-80fe966df97f)
- now create another tab and create a file with random passwords. preferably ones that are very common. we'll head to payload config in truder and upload that file.
- ![Screenshot 2025-11-02 224053](https://github.com/user-attachments/assets/e46edb5b-8e7b-4cb0-b038-d737bfe94f9e)
- Almost done!, lets go into the code of the webpage where we tried to loginto with our fake credentials. scroll down and find the error message we would get if we were to put in the wrong credentials. copy it and paste it into "Grep - Match"
![Screenshot 2025-11-02 224508](https://github.com/user-attachments/assets/91d9f54d-7f0b-441b-9b86-983e8d68b40c)
![Screenshot 2025-11-02 224701](https://github.com/user-attachments/assets/7e2709e7-29e7-4709-8345-2db35b8d295b)
  - This will tell Burpsuite to flag this reponse if given
4. Now were ready to run our configurations. go ahead and press "start attack". Let it run and you should see something like this after it is done.
![Screenshot 2025-11-02 224943](https://github.com/user-attachments/assets/3d9d2fea-c14a-4498-83ad-b0dc95ede161)

burpsuite used every password within our file, and if you havent noticed there one input that is missing a username 1. that is our password. and when you click on it, you can see the full request. the username and password 
- now lets head back to DVWA and plugin that passowrd.
  ![Screenshot 2025-11-02 225051](https://github.com/user-attachments/assets/94ae8f82-79a3-47b2-88fb-c8b0241b954b)

  Bingo!!!








