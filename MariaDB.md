# MariaDB

## Index

1. [Bases](##Bases)

## Bases

After having installed mariaDB, and having enabled the service using:

```bash
sudo systemctl start mariadb
```

create a user:

```sql
CREATE USER <userName>@localhost IDENTIFIED BY '<password>';
```

And a DB:

```sql
CREATE DATABASE <DBName>;
GRANT ALL PRIVILEGES ON <DBName> TO '<userName>'@'localhost';
```

if you want to check if everything is alright try logging in using:
``` sh
mysql <DB> -u <user> -p 
```
