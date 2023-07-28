# DOM-XSS

- When navigating to the website, we have a to-do list where we can add items.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/f5228de7-ef71-4395-8d93-1f5115cdd3ff)

- Upon inspecting the element, it appears that no POST request is being sent to the server. This suggests that there might be a possibility of DOM-based XSS (Cross-Site Scripting) vulnerability.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/4495fa4f-0822-44ca-876a-e09e540c9bc9)

- I attempted to trigger the payload `<script>prompt(1)</script>`, but it did not execute. It is possible that the input is being filtered or sanitized, which is preventing the payload from being triggered.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/cc1c5a7f-af6e-4d91-a152-f6fa7d689037)

- Upon sending the payload `<img src=x onerror="prompt(1)">`, it successfully triggered and displayed a prompt.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/f579af0c-33d6-403b-babf-149e93d0af08)
