# MySQL Server Installation (No Admin Required)

A comprehensive guide for installing MySQL Server on Windows without administrator privileges using the ZIP archive.

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Download MySQL](#download-mysql)
3. [Installation Steps](#installation-steps)
4. [Configuration](#configuration)
5. [Database Initialization](#database-initialization)
6. [Server Management](#server-management)
7. [User and Database Management](#user-and-database-management)
8. [Testing and Verification](#testing-and-verification)
9. [Troubleshooting](#troubleshooting)

## Prerequisites

- Windows 10 or later
- User account with standard privileges
- Internet connection
- Approximately 300MB of free disk space

## Download MySQL

### 1. Download MySQL ZIP Archive

**Option 1: Direct Download**
```cmd
powershell -c "(new-object System.Net.WebClient).DownloadFile('https://cdn.mysql.com//Downloads/MySQL-9.3/mysql-9.3.0-winx64.zip','%userprofile%\downloads\mysql-9.3.0-winx64.zip')"
```

**Option 2: Manual Download**
- Go to [MySQL Downloads](https://dev.mysql.com/downloads/mysql/)
- Select **Windows (x86, 64-bit), ZIP Archive**
- Download the ZIP file (not the installer)

## Installation Steps

### 1. Create Directory Structure

```cmd
mkdir C:\sw\db\mysql
```

### 2. Extract MySQL

```cmd
powershell -c "Expand-Archive -Path '%userprofile%\downloads\mysql-9.3.0-winx64.zip' -DestinationPath 'C:\sw\db\mysql'"
```

### 3. Rename Directory

```cmd
move "C:\sw\db\mysql\mysql-9.3.0-winx64" "C:\sw\db\mysql\mysql-9.3.0"
```

### 4. Create Required Directories

```cmd
mkdir C:\sw\db\mysql\mysql-9.3.0\data
mkdir C:\sw\db\mysql\mysql-9.3.0\logs
```

### 5. Set Environment Variables

```cmd
setx MYSQL_ROOT "C:\sw\db\mysql\mysql-9.3.0"
```

### 6. Add to PATH

**Using GUI (Recommended):**
```cmd
rundll32 sysdm.cpl,EditEnvironmentVariables
```
Add `%MYSQL_ROOT%\bin` to your PATH.

**Or using command line:**
```cmd
setx PATH "%PATH%;%MYSQL_ROOT%\bin"
```

## Configuration

### 1. Create MySQL Configuration File

Create `C:\sw\db\mysql\mysql-9.3.0\my.ini`:

```cmd
notepad C:\sw\db\mysql\mysql-9.3.0\my.ini
```

### 2. Configuration Content

Add the following content to `my.ini`:

```ini
[mysqld]
# Basic Settings
user                    = mysql
port                    = 3306
bind-address            = 0.0.0.0
max_connections         = 150

# Directory Settings
basedir = "C:/sw/db/mysql/mysql-9.3.0"
datadir = "C:/sw/db/mysql/mysql-9.3.0/data"
tmpdir = "C:/sw/db/mysql/mysql-9.3.0/logs"

# Logging
log-error = "C:/sw/db/mysql/mysql-9.3.0/logs/mysql-server-error.log"
general_log = 1
general_log_file = "C:/sw/db/mysql/mysql-9.3.0/logs/mysql-server-general.log"

# Performance Settings
innodb_buffer_pool_size = 128M
innodb_log_file_size = 50M

# Security Settings
sql_mode = STRICT_TRANS_TABLES,NO_ZERO_DATE,NO_ZERO_IN_DATE,ERROR_FOR_DIVISION_BY_ZERO

[mysql]
default-character-set = utf8mb4

[client]
default-character-set = utf8mb4
```

## Database Initialization

### 1. Close Current Terminal

```cmd
exit
```

### 2. Open New Terminal

Open a new command prompt to load the updated environment variables.

### 3. Initialize Database

```cmd
mysqld --initialize --user=root --console
```

**Important:** Note the temporary root password that will be displayed. It looks like:
```
[Note] A temporary password is generated for root@localhost: kB3mP9x&vN2!
```

**Parameters explained:**
- `--initialize`: Creates a new database with random root password
- `--user=root`: Run as root user
- `--console`: Display output in console instead of log file

## Server Management

### 1. Start MySQL Server

```cmd
mysqld --console
```

**Note:** Keep this terminal window open while using MySQL. The server will stop when you close this window.

### 2. Start Server in Background (Alternative)

```cmd
mysqld --install-manual MySQL93
net start MySQL93
```

### 3. Stop Server

If running with `--console`, press `Ctrl+C` in the server terminal.

If running as service:
```cmd
net stop MySQL93
```

## User and Database Management

### 1. Connect to MySQL

Open a **new terminal window** (keep the server running in the first one):

```cmd
mysql -u root -p
```

Enter the temporary password from the initialization step.

### 2. Change Root Password

```sql
-- Change root password (use a secure password in production)
ALTER USER 'root'@'localhost' IDENTIFIED BY '1';

-- Create root user for remote connections
CREATE USER 'root'@'%' IDENTIFIED BY '1';

-- Grant all privileges
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%';

-- Apply changes
FLUSH PRIVILEGES;

-- Exit MySQL
exit
```

### 3. Test New Password

```cmd
mysql -u root -p
```

Enter the new password (`1` in this example).

### 4. Create Application User and Database

```sql
-- Create a new database
CREATE DATABASE testapp;

-- Create a new user
CREATE USER 'appuser'@'localhost' IDENTIFIED BY 'apppassword';
CREATE USER 'appuser'@'%' IDENTIFIED BY 'apppassword';

-- Grant privileges to the database
GRANT ALL PRIVILEGES ON testapp.* TO 'appuser'@'localhost';
GRANT ALL PRIVILEGES ON testapp.* TO 'appuser'@'%';

-- Apply changes
FLUSH PRIVILEGES;

-- Show databases
SHOW DATABASES;

-- Show users
SELECT user, host FROM mysql.user;

-- Exit
exit
```

## Testing and Verification

### 1. Test Connection with New User

```cmd
mysql -u appuser -p -D testapp
```

### 2. Create and Test Table

```sql
-- Create a test table
CREATE TABLE products (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    price DECIMAL(10,2),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Insert test data
INSERT INTO products (name, price) VALUES 
('Laptop', 999.99),
('Mouse', 29.99),
('Keyboard', 79.99);

-- Query the data
SELECT * FROM products;

-- Show table structure
DESCRIBE products;
```

### 3. Test Basic Operations

```sql
-- Update data
UPDATE products SET price = 899.99 WHERE name = 'Laptop';

-- Delete data
DELETE FROM products WHERE price < 50;

-- Count records
SELECT COUNT(*) FROM products;

-- Show tables
SHOW TABLES;

-- Exit
exit
```

## Troubleshooting

### Common Issues

#### 1. Command Not Found
**Problem:** `'mysql' is not recognized as an internal or external command`

**Solutions:**
- Verify `MYSQL_ROOT` environment variable is set
- Check that `%MYSQL_ROOT%\bin` is in PATH
- Close and reopen command prompt
- Verify mysql.exe exists in the bin directory

#### 2. Server Won't Start
**Problem:** `mysqld` command fails to start

**Solutions:**
- Check if another MySQL instance is running
- Verify the data directory is properly initialized
- Check the error log:
```cmd
type "C:\sw\db\mysql\mysql-9.3.0\logs\mysql-server-error.log"
```
- Ensure port 3306 is not in use by another application

#### 3. Access Denied Errors
**Problem:** Cannot connect to MySQL server

**Solutions:**
- Verify the server is running
- Check username and password
- Ensure the user has proper privileges
- Try connecting as root first

#### 4. Configuration Issues
**Problem:** Server starts but behaves unexpectedly

**Solutions:**
- Check the `my.ini` configuration file
- Verify all directory paths exist and are writable
- Check the error log for configuration warnings

#### 5. Port Already in Use
**Problem:** Error binding to port 3306

**Solutions:**
- Check if another MySQL instance is running:
```cmd
netstat -an | findstr :3306
```
- Change the port in `my.ini` if needed
- Stop other MySQL services

### Useful Commands

```cmd
# Check MySQL version
mysql --version

# Show MySQL configuration
mysql --help --verbose

# Check server status
mysqladmin -u root -p status

# Show running processes
mysqladmin -u root -p processlist

# Create database backup
mysqldump -u root -p testapp > backup.sql

# Restore database
mysql -u root -p testapp < backup.sql

# Check which port MySQL is using
netstat -an | findstr :3306
```

### MySQL Client Commands

```sql
-- Show current user
SELECT USER();

-- Show current database
SELECT DATABASE();

-- Show server version
SELECT VERSION();

-- Show server status
SHOW STATUS;

-- Show server variables
SHOW VARIABLES;

-- Show databases
SHOW DATABASES;

-- Show tables in current database
SHOW TABLES;

-- Show table structure
DESCRIBE table_name;

-- Show create statement for table
SHOW CREATE TABLE table_name;
```

### File Locations

- **MySQL Installation:** `C:\sw\db\mysql\mysql-9.3.0`
- **Configuration File:** `C:\sw\db\mysql\mysql-9.3.0\my.ini`
- **Data Directory:** `C:\sw\db\mysql\mysql-9.3.0\data`
- **Log Files:** `C:\sw\db\mysql\mysql-9.3.0\logs`
- **Error Log:** `C:\sw\db\mysql\mysql-9.3.0\logs\mysql-server-error.log`

## Best Practices

1. **Security:** Use strong passwords and create specific users for applications
2. **Backups:** Regularly backup your databases using `mysqldump`
3. **Monitoring:** Check error logs regularly for issues
4. **Performance:** Adjust buffer pool size based on available memory
5. **Updates:** Keep MySQL updated to the latest stable version
6. **User Management:** Don't use root for application connections

## Related Links

- [MySQL Official Documentation](https://dev.mysql.com/doc/)
- [MySQL Downloads](https://dev.mysql.com/downloads/mysql/)
- [MySQL Tutorial](https://www.mysqltutorial.org/)
- [Back to Main Guide](readme.md)