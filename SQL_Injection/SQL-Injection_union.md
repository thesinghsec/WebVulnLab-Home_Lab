# SQL Injection - UNION 
- A search box was identified within the application. The search box allows users to query and retrieve information from the system.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/6dc94469-f93d-4868-96fd-9529fa39be13)

- When entering the username `"jeremy"` the following information about the user was obtained:

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/8e395182-1c56-4bb4-be0f-bd8d253f5a8c)

- The attempted input of `jeremy'` resulted in a null response, indicating the implementation of a targeted search mechanism.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/98fd7d57-d984-46a4-bf37-7cedad5f9f8e)

- Upon injecting the input `jeremy' OR 1=1#` into the system, we encountered a significant security vulnerability. The resulting outcome provided us with access to the complete dataset of available users within the database. 

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/905ef362-d495-4304-adbc-2c4a1d8b0454)

-  This confirms the existence of a SQL injection vulnerability within the application. By executing the command `jeremy' union select 1,2,version()#` via SQL injection, we successfully obtained the version information from the system. 

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/05614dc5-a3bb-4b45-8719-37da46e77b50)

- Continuing our enumeration process, we were able to extract table information by executing the command `jeremy' union select 1,2,table_name from information_schema.tables#` via SQL injection.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/ffb8b004-4698-4172-b042-84938107f5fb)

- Through meticulous enumeration, we have successfully extracted the column names from the database using the command `jeremy' union select 1,2,column_name from information_schema.columns#` via SQL injection. 

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/817d7b01-1d78-4ed6-a279-81285aad2eae)

- By executing the command `jeremy' union select 1,2,password from injection0x01#` via SQL injection, we have been able to successfully retrieve the users' passwords. 

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/6e7d05a4-5947-44b3-bd78-373f479aedf4)
