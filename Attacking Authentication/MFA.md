# Attacking Authentication - MFA

- We have user credentials as :
  - user: jessamy
  - Password: pasta
  - Target account: Jeremy

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/66ad163a-0c44-4dee-b81d-2124fcd80324)

- On clicking submit we have landed on the MFA.
- By clicking "found here" we got our code.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/960f7bbb-bf9a-48ac-846c-cfc8032ae84c)

- On submitting the code we successfully logged in.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/a3e7b00b-433b-460c-b613-7ad1f06dd402)

- Now, we will again try to log in, but this time we will intercept the request to burp suite on entering MFA.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/66b47b9e-aaf4-4855-b77d-618eb04bc362)

- In request, we will change the name from "jessamy" to "jeremy" and hit the intercept off, in browser we get successfully logged in as Jeremy.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/b0ba2d29-940e-4f88-b051-0f73ed8d7d42)

