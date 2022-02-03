## Export Database

```
sudo mysqldump -u root -p testDB > testDB_backup1.sql
```

## Copy database using ssh scp

```
scp testDB_backup1.sql raihan@100.104.180.18
```
