# MySQL Server Installation (No Admin Required)

Install **MySQL Server on Windows without administrator privileges** using the ZIP archive method.

---

## 📑 Table of Contents
1. [Prerequisites](#prerequisites)  
2. [Download MySQL](#download-mysql)  
3. [Installation Steps](#installation-steps)  
4. [Configuration](#configuration)  
5. [Database Initialization](#database-initialization)  
6. [Server Management](#server-management)  
7. [User and Database Management](#user-and-database-management)  
8. [Testing and Verification](#testing-and-verification)  
9. [Troubleshooting](#troubleshooting)  
10. [Best Practices](#best-practices)  

---

## ✅ Prerequisites
- Windows 10 or later  
- Standard user account (no admin rights)  
- Internet connection  
- ~300MB free disk space  

---

## 📥 Download MySQL

### Option 1: PowerShell Direct Download
```cmd
powershell -c "(new-object System.Net.WebClient).DownloadFile('https://cdn.mysql.com//Downloads/MySQL-9.3/mysql-9.3.0-winx64.zip','%userprofile%\downloads\mysql-9.3.0-winx64.zip')"
```

### Option 2: Manual Download
1. Visit [MySQL Downloads](https://dev.mysql.com/downloads/mysql/)  
2. Select **Windows (x86, 64-bit), ZIP Archive**  
3. Download the ZIP file (not the installer)  

---

## 🛠 Installation Steps

1. **Create directory structure**
   ```cmd
   mkdir C:\sw\db\mysql
   ```

2. **Extract MySQL**
   ```cmd
   powershell -c "Expand-Archive -Path '%userprofile%\downloads\mysql-9.3.0-winx64.zip' -DestinationPath 'C:\sw\db\mysql'"
   ```

3. **Rename directory**
   ```cmd
   move "C:\sw\db\mysql\mysql-9.3.0-winx64" "C:\sw\db\mysql\mysql-9.3.0"
   ```

4. **Create data and log directories**
   ```cmd
   mkdir C:\sw\db\mysql\mysql-9.3.0\data
   mkdir C:\sw\db\mysql\mysql-9.3.0\logs
   ```

5. **Set environment variables**
   ```cmd
   setx MYSQL_ROOT "C:\sw\db\mysql\mysql-9.3.0"
   ```

6. **Add MySQL to PATH**
   - GUI: `rundll32 sysdm.cpl,EditEnvironmentVariables` → add `%MYSQL_ROOT%\bin`  
   - CLI:  
     ```cmd
     setx PATH "%PATH%;%MYSQL_ROOT%\bin"
     ```

---

## ⚙️ Configuration

Create `C:\sw\db\mysql\mysql-9.3.0\my.ini` with:

```ini
[mysqld]
user = mysql
port = 3306
bind-address = 0.0.0.0
max_connections = 150

basedir = "C:/sw/db/mysql/mysql-9.3.0"
datadir = "C:/sw/db/mysql/mysql-9.3.0/data"
tmpdir = "C:/sw/db/mysql/mysql-9.3.0/logs"

log-error = "C:/sw/db/mysql/mysql-9.3.0/logs/mysql-server-error.log"
general_log = 1
general_log_file = "C:/sw/db/mysql/mysql-9.3.0/logs/mysql-server-general.log"

innodb_buffer_pool_size = 128M
innodb_log_file_size = 50M

sql_mode = STRICT_TRANS_TABLES,NO_ZERO_DATE,NO_ZERO_IN_DATE,ERROR_FOR_DIVISION_BY_ZERO

[mysql]
default-character-set = utf8mb4

[client]
default-character-set = utf8mb4
```

---

## 🗄 Database Initialization

1. Close terminal → reopen to load new PATH  
2. Run initialization:
   ```cmd
   mysqld --initialize --user=root --console
   ```
   - Note the **temporary root password** displayed.  

---

## 🚀 Server Management

- **Start server (console mode):**
  ```cmd
  mysqld --console
  ```
- **Stop server (console mode):** `Ctrl+C`  
- **Start as background service (optional):**
  ```cmd
  mysqld --install-manual MySQL93
  net start MySQL93
  ```
- **Stop service:**
  ```cmd
  net stop MySQL93
  ```

---

## 👤 User & Database Management

1. Connect:
   ```cmd
   mysql -u root -p
   ```
2. Change root password & create users:
   ```sql
   ALTER USER 'root'@'localhost' IDENTIFIED BY 'newpassword';
   CREATE USER 'appuser'@'localhost' IDENTIFIED BY 'apppassword';
   GRANT ALL PRIVILEGES ON testapp.* TO 'appuser'@'localhost';
   FLUSH PRIVILEGES;
   ```

---

## 🔍 Testing & Verification

- Connect as appuser:
  ```cmd
  mysql -u appuser -p -D testapp
  ```
- Create and query tables:
  ```sql
  CREATE TABLE products (...);
  INSERT INTO products (name, price) VALUES ('Laptop', 999.99);
  SELECT * FROM products;
  ```

---

## 🧩 Troubleshooting

**Common Issues:**
- **Command not found:** Check PATH and `%MYSQL_ROOT%\bin`  
- **Server won’t start:** Verify data dir, check logs  
- **Access denied:** Ensure correct user/password, privileges  
- **Port in use:** Run `netstat -an | findstr :3306`  

---

## 🛡 Best Practices
1. Use strong passwords  
2. Create app-specific users (avoid root)  
3. Regular backups with `mysqldump`  
4. Monitor logs regularly  
5. Tune performance settings for your system  
6. Keep MySQL updated  

---

## 🔗 Related Links
- [MySQL Official Docs](https://dev.mysql.com/doc/)  
- [MySQL Downloads](https://dev.mysql.com/downloads/mysql/)  
- [MySQL Tutorial](https://www.mysqltutorial.org/)  
- [Back to Main Guide](/readme.md)
