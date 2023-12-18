# **Lab 12 PHP Form Login**

```
Nama    : Dipca Anugrah
NIM     : 312210666
Kelas   : TI.22.A.4
Matkul  : Pemrograman Web 1
```

## **Daftar Isi**

**[Langkah-langkah Praktikum](#langkah-lankgah-praktikum)**

**[Result](#result)**

## **Langkah-lankgah Praktikum**

• **DDL: Table user**

```sql
CREATE TABLE `user`(
`id` INT NOT NULL AUTO_INCREMENT,
`username` VARCHAR(50),
`password` VARCHAR(50),
PRIMARY KEY (`id`),
UNIQUE INDEX `UNIQUE` (`username`)
) ENGINE=MYISAM;
INSERT INTO `user` (`username`, `password`) VALUES ('admin', md5('admin'));
```

**• File: login_session.php**

```php
<?php
session_start();
if (!isset($_SESSION['isLogin']))
header('location: login.php');
?>
```


• **File: login.php**

```php
<?php
session_start();
$title = 'Data Barang';
include_once 'koneksi.php';
if (isset($_POST['submit']))
{
 $user = $_POST['user'];
 $password = $_POST['password'];

 $sql = "SELECT * FROM user WHERE username = '{$user}'

AND password = md5('{$password}') ";
$result = mysqli_query($conn, $sql);
    if ($result && mysqli_affected_rows($conn) != 0)
    {
        $_SESSION['isLogin'] = true;
        $_SESSION['user'] = mysqli_fetch_array($result);
        header('location: index.php');
    } else
        $errorMsg = "<p style=\"color:red;\">Gagal Login,
        silakan ulangi lagi.</p>";
    }
include_once "header.php";
if (isset($errorMsg)) echo $errorMsg;
?>
<h2>Login</h2>
<form method="post">
    <div class="input">
        <label>Username</label>
        <input type="text" name="user" />
    </div>
    <div class="input">
        <label>Password</label>
        <input type="password" name="password" />
    </div>
    <div class="submit">
        <input type="submit" name="submit" value="Login" />
    </div>
</form>
<?php
include_once 'footer.php';
?>

```

<img src="https://github.com/dipca0895/Lab12PHP_Form_Login/blob/main/gambar/login.png" width=70% height=70%>

## **Result**

https://github.com/dipca0895/Lab12PHP_Form_Login/assets/115719283/60e3ca33-cd66-4fe7-845d-5e4362ca35a1

<hr>

**[Back-->](#lab-10-php-oop)**
