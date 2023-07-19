Attacking Authentication - MFA

- We have user credentials as :
  - user: jessamy
  - Password: pasta
  - Target account: Jeremy

 ![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/730c64f6-4e49-4aa2-824c-8b1951cb4662)

- On clicking submit we have landed on the MFA.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/d475c3e5-6bb4-43d5-a242-074357279c52)

- By clicking "found here" we got our code.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/798b6952-60ce-4c2a-8c8f-c36f89e4315e)

- On submitting the code we successfully logged in.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/3af2a4e6-dc9c-48d5-9c83-567d60d75313)
![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/6fe856ec-e9b0-4912-8179-baaafcd97af6)

- Now, we will again try to log in, but this time we will intercept the request to burp suite on entering MFA.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/df271bf5-20a6-443c-a882-893e3026b6b7)

- In request, we will change the name from "jessamy" to "jeremy" and hit the intercept off, in browser we get successfully logged in as Jeremy.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/0f555ff8-7a6a-4185-95ba-5f0ebe78c36d)

