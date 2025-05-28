# Installing MySQL Server without admin rights

1: Download mysql zip from the https://dev.mysql.com/downloads/mysql/
	```bash
	powershell -c "(new-object System.Net.WebClient).DownloadFile('https://cdn.mysql.com//Downloads/MySQL-9.3/mysql-9.3.0-winx64.zip','%userprofile%\downloads\mysql-9.3.0-winx64.zip')"
	```
	
2. unzip to c:\sw\db\mysql\
	```bash
	powershell -c Expand-Archive -Path "%userprofile%\downloads\mysql-9.3.0-winx64.zip" -DestinationPath "c:\sw\db\mysql"
	```
3. rename direcotry as c:\sw\db\mysql\mysql-9.3.0
	```bash
	move c:\sw\db\mysql\mysql-9.3.0-winx64 c:\sw\db\mysql\mysql-9.3.0
	```
4. create data and log directory
	```bash
	mkdir c:\sw\db\mysql\mysql-9.3.0\data
	mkdir c:\sw\db\mysql\mysql-9.3.0\logs
	```
5. set environment variable MYSQL_ROOT
	```bash
	SETX MYSQL_ROOT c:\sw\db\mysql\mysql-9.3.0
	```
6. add %MYSQL_ROOT%\bin to environment variable
	```bash
	ev
	%MYSQL_ROOT%\bin
	```
	
7. create c:\sw\db\mysql\mysql-9.3.0\my.ini
	```bash
	notepad c:\sw\db\mysql\mysql-9.3.0\my.ini
	```
```
[mysqld]
user                    = mysql
port                    = 3306
bind-address            = 0.0.0.0
max_connections         = 150

basedir = "c:/sw/db/mysql/mysql-9.3.0"
datadir = "c:/sw/db/mysql/mysql-9.3.0/data"
tmpdir = "c:/sw/db/mysql/mysql-9.3.0/logs"
log-error = "c:/sw/db/mysql/mysql-9.3.0/mysql-server-1.log"
```

8. restart console
	```bash
	exit
	```

9. Initialize DB
	```bash
	mysqld --initialize --user=root --console
	```
	```
	--initialize: create new db. Data direcotry should be blank
	--console: error are displayed in console instead of log
	```

10. Run Server: use the password given in # for first use
	```bash
	mysqld --console
	```

11. Change password, for 1st time use
	```bash
	mysql -u root -p
	```

	```mysql
	ALTER USER 'root'@'localhost' IDENTIFIED BY '1';
	CREATE USER 'root'@'%' IDENTIFIED BY '1';
	GRANT ALL PRIVILEGES ON *.* TO 'root'@'%';
	FLUSH PRIVILEGES;
	exit
	```
