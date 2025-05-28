### Install PostgreSQL
```bash
mkdir C:\SW\DB\PostgreSQL
```

1. [Download binaries][pgsb] and extract to to C:\SW\DB\PostgreSQL
2. Add C:\SW\DB\PostgreSQL\pgsql\bin to PATH
  ```bash
  setx PATH "%PATH%;C:\SW\DB\PostgreSQL\pgsql\bin"
  ```

### Test the installation 
```bash
postgres -V
psql -V
```

### Create DB
```bash
set DBPATH=C:\SW\DB\PostgreSQL\data\pgdata
initdb -D %DBPATH% -U postgres -W -E UTF8 -A scram-sha-256
```

### Start the PostgreSQL database
```bash
pg_ctl -D "%DBPATH%" -l logfile start
```

#### From
```
https://www.youtube.com/watch?v=cYFYfYXObgA
https://tutlinks.com/install-postgresql-without-admin-rights-windows/#google_vignette
```


[pgsb]:https://www.enterprisedb.com/download-postgresql-binaries
