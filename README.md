# mysql-backup-guideline

How to backup & restore MySQL database

## Backup script
backupmysql.sh
```bash
#!/bin/sh

# backup period（days）
period=3

# backup directory
dirpath='/backup'

# file name with datetime
filename=`date +%y%m%d`

# Mysqldump command
mysqldump -u[USER_NAME] -p[PASSWORD] -h[HOST] [DATABASE_NAME] > $dirpath/$filename.sql

# Permission
chmod 700 $dirpath/$filename.sql

# Remove old file
# Remove after backup period days
oldfile=`date --date "$period days ago" +%y%m%d`
rm -f $dirpath/$oldfile.sql
```

## Crontab

Configure a crontab to run backup script

```bash
http://www.server-memo.net/tips/crontab.html

echo "0 3 * * * root /backupmysql.sh" > /etc/cron.d/backupmysql
```
