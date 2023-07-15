# SQL Injection - UNION 
- A search box was identified within the application. The search box allows users to query and retrieve information from the system.

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/01575e3c-ab17-4971-8b5c-56a48e57d187)

- When entering the username `"jeremy"` the following information about the user was obtained:

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/1a11873e-fb1e-412b-b713-89266f72d149)

- The attempted input of `jeremy'` resulted in a null response, indicating the implementation of a targeted search mechanism.

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/b512c751-c9bb-47c1-811d-b5f65f6d2ccc)

- Upon injecting the input `jeremy' OR 1=1#` into the system, we encountered a significant security vulnerability. The resulting outcome provided us with access to the complete dataset of available users within the database. 

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/eb838956-be55-4ae2-9a5f-368ee0d38f3e)

-  This confirms the existence of a SQL injection vulnerability within the application. By executing the command `jeremy' union select 1,2,version()#` via SQL injection, we successfully obtained the version information from the system. 

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/c2c84d65-8d7c-4499-8148-1ffa9dfc8e66)

- Continuing our enumeration process, we were able to extract table information by executing the command `jeremy' union select 1,2,table_name from information_schema.tables#` via SQL injection.

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/996cc756-ae91-4ae9-bcbb-765d9778cbb1)

- Through meticulous enumeration, we have successfully extracted the column names from the database using the command `jeremy' union select 1,2,column_name from information_schema.columns#` via SQL injection. 

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/9177abfb-8e36-44d9-b3ff-1075c7a38430)

- By executing the command `jeremy' union select 1,2,password from injection0x01#` via SQL injection, we have been able to successfully retrieve the users' passwords. 

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/951793b7-8aa7-4062-b0a9-5e5b7b3fd231)
