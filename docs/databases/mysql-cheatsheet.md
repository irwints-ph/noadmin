# ⚡ MySQL No-Admin Quick Start

## 1. Download & Extract
```cmd
powershell -c "(new-object System.Net.WebClient).DownloadFile('https://cdn.mysql.com//Downloads/MySQL-9.3/mysql-9.3.0-winx64.zip','%userprofile%\downloads\mysql.zip')"
mkdir C:\sw\db\mysql
powershell -c "Expand-Archive -Path '%userprofile%\downloads\mysql.zip' -DestinationPath 'C:\sw\db\mysql'"
move "C:\sw\db\mysql\mysql-9.3.0-winx64" "C:\sw\db\mysql\mysql-9.3.0"
mkdir C:\sw\db\mysql\mysql-9.3.0\data
mkdir C:\sw\db\mysql\mysql-9.3.0\logs
setx MYSQL_ROOT "C:\sw\db\mysql\mysql-9.3.0"
setx PATH "%PATH%;%MYSQL_ROOT%\bin"
```

---

## 2. Config File (`my.ini`)
Save at `C:\sw\db\mysql\mysql-9.3.0\my.ini`:
```ini
[mysqld]
basedir = "C:/sw/db/mysql/mysql-9.3.0"
datadir = "C:/sw/db/mysql/mysql-9.3.0/data"
port = 3306
log-error = "C:/sw/db/mysql/mysql-9.3.0/logs/error.log"

[mysql]
default-character-set = utf8mb4

[client]
default-character-set = utf8mb4
```

---

## 3. Initialize & Start
```cmd
mysqld --initialize --user=root --console
mysqld --console
```
👉 Copy the temporary root password shown.

---

## 4. Connect & Setup Users
```cmd
mysql -u root -p
```
Inside MySQL:
```sql
ALTER USER 'root'@'localhost' IDENTIFIED BY 'newpassword';
CREATE DATABASE testapp;
CREATE USER 'appuser'@'localhost' IDENTIFIED BY 'apppassword';
GRANT ALL PRIVILEGES ON testapp.* TO 'appuser'@'localhost';
FLUSH PRIVILEGES;
```

---

## 5. Verify
```cmd
mysql -u appuser -p -D testapp
```
```sql
SHOW DATABASES;
```

---

## 🔗 Related Links
- [MySQL Official Documentation](https://dev.mysql.com/doc/)  
- [MySQL Downloads](https://dev.mysql.com/downloads/mysql/)  
- [MySQL Tutorial](https://www.mysqltutorial.org/)  
- [Back to Main Guide](/readme.md)