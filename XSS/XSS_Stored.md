# Stored-XSS

- When visiting the website, I noticed a comment box where the input is stored on the server.

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/99033f04-bbd5-47bc-9c81-c025cdee6de0)

- When attempting HTML injection, I was successful, indicating the presence of a possible stored XSS (Cross-Site Scripting) vulnerability.

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/a3448eb2-42e3-4115-a4c3-a7aa11d1f81f)

- I conducted a test for stored XSS by setting a cookie in my browser and attempting to execute a command. The objective was to determine if the cookie would be reflected on other user accounts.

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/1fe931f3-31c7-462f-ad95-307d06a7b210)

- Upon sending the testing code `<script>prompt("hello")</script>`, we discovered that our script was successfully stored on the server and is being reflected on every user's account.

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/b0663a1b-596b-4a77-a79a-f63653d5e989)

- I proceeded with attempting to send a custom cookie that I set myself. I included this custom cookie in the payload `<script>prompt(document.cookie)</script>` and sent it to observe if it triggers a prompt or executes any actions.

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/b2caafca-ea46-4f77-aad5-62e2c4962a44)

