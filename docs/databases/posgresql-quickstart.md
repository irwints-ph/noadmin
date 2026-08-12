# ⚡ PostgreSQL No-Admin Quick Start

## 1. Download & Extract
```cmd
mkdir C:\SW\DB\PostgreSQL
powershell -c "(new-object System.Net.WebClient).DownloadFile('https://ftp.postgresql.org/pub/source/v16.1/postgresql-16.1-windows-x64-binaries.zip','%userprofile%\downloads\postgresql.zip')"
powershell -c "Expand-Archive -Path '%userprofile%\downloads\postgresql.zip' -DestinationPath 'C:\SW\DB\PostgreSQL'"
setx PATH "%PATH%;C:\SW\DB\PostgreSQL\pgsql\bin"
```

---

## 2. Initialize Database
```cmd
set DBPATH=C:\SW\DB\PostgreSQL\data\pgdata
initdb -D %DBPATH% -U postgres -W -E UTF8 -A scram-sha-256
```
👉 Enter and remember the password for the `postgres` superuser.

---

## 3. Start & Stop Server
```cmd
pg_ctl -D "%DBPATH%" -l logfile start   # Start
pg_ctl -D "%DBPATH%" stop               # Stop
pg_ctl -D "%DBPATH%" restart            # Restart
pg_ctl -D "%DBPATH%" status             # Status
```

---

## 4. Connect & Create User/DB
```cmd
psql -U postgres
```
Inside PostgreSQL:
```sql
CREATE USER appuser WITH ENCRYPTED PASSWORD 'apppassword';
CREATE DATABASE testdb OWNER appuser;
GRANT ALL PRIVILEGES ON DATABASE testdb TO appuser;
```

---

## 5. Verify
```cmd
psql -U appuser -d testdb
```
```sql
SELECT version();
CREATE TABLE demo (id SERIAL PRIMARY KEY, name TEXT);
INSERT INTO demo (name) VALUES ('Hello PostgreSQL');
SELECT * FROM demo;
```

---

## 🔗 Related Links
- [PostgreSQL Official Documentation](https://www.postgresql.org/docs/)  
- [PostgreSQL Binaries Download](https://www.enterprisedb.com/download-postgresql-binaries)  
- [PostgreSQL Tutorial](https://neon.com/postgresql/tutorial)  
- [Back to Main Guide](/readme.md)