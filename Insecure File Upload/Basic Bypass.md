# Insecure File Upload - Basic Bypass

- When I arrived at the website, I discovered a section dedicated to uploading files.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/d5cbe3a2-4aaa-4535-b336-98f8d57ee180)

- During my testing, I attempted to upload a text file, but I encountered a restriction stating that only PNG and JPG files are permitted for uploading.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/d7d868bf-26bc-4d31-ab81-4f077aac26d8)

- Once again, I attempted to upload the file to observe if any requests were sent to the server. However, upon further investigation, I did not detect any requests being made during the upload process.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/1c781bad-d29f-4b42-9d63-17504129ac1f)

- I repeated the process of uploading a PNG file and intercepted the corresponding request using Burp Suite for analysis.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/fb4121b3-103b-4290-b836-7fe5d38ac7a5)

- After sending the request to the repeater in Burp Suite, I proceeded to make some minor modifications to the request in an attempt to achieve my goal. I changed the file name extension from "png" to "txt" and removed the image data. Instead, I inserted the text "Hello" in its place.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/e2015bbf-a607-4723-9366-d1477792aeb1)

- Following the successful modification of the request, I refreshed the page on the browser to reverify if the file was indeed uploaded.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/5fa3786f-9a4d-4728-906a-1d4d35f4864a)

### Task Accomplished!
