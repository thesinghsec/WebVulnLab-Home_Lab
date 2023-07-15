# DOM-XSS

- When navigating to the website, we have a to-do list where we can add items.

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/52284a15-31a0-431f-86d1-d852d5b352b3)

- Upon inspecting the element, it appears that no POST request is being sent to the server. This suggests that there might be a possibility of DOM-based XSS (Cross-Site Scripting) vulnerability.

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/ed8009e4-7190-4c25-a722-5e5a451b7d2b)

- I attempted to trigger the payload `<script>prompt(1)</script>`, but it did not execute. It is possible that the input is being filtered or sanitized, which is preventing the payload from being triggered.

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/717a85f5-56de-4d43-8ca4-02cab7ddc4c0)

- Upon sending the payload `<img src=x onerror="prompt(1)">`, it successfully triggered and displayed a prompt.

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/0c71aa5a-fe0e-4517-b4bb-5eb07ca68591)

