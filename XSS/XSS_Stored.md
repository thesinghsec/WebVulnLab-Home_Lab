# Stored-XSS

- When visiting the website, I noticed a comment box where the input is stored on the server.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/532855a3-5295-41a7-8f74-8657647e3ed4)

- When attempting HTML injection, I was successful, indicating the presence of a possible stored XSS (Cross-Site Scripting) vulnerability.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/86b49fdf-ef67-4f50-9d40-ed4fed47addb)

- I conducted a test for stored XSS by setting a cookie in my browser and attempting to execute a command. The objective was to determine if the cookie would be reflected on other user accounts.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/5b12111b-ef9d-4c04-88b1-35537d2b024b)

- Upon sending the testing code `<script>prompt("hello")</script>`, we discovered that our script was successfully stored on the server and is being reflected on every user's account.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/6792170f-8325-446f-9cc3-ebba8f8fab41)

- I proceeded with attempting to send a custom cookie that I set myself. I included this custom cookie in the payload `<script>prompt(document.cookie)</script>` and sent it to observe if it triggers a prompt or executes any actions.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/fc3e719e-bcd8-4397-a211-6f8d3cb9937f)

