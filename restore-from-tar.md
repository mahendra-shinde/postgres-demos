# PG_DUMP and PG_RESTORE for Medium to large database

1.  Download the sample database

    ```bash
    curl -o orderdb.sql https://raw.githubusercontent.com/mahendra-shinde/postgres-demos/main/order-db.sql 
    ```

1.  Connect PSQL and Create new `sample` database; import all data from downloaded SQL file.

    ```bash
    sudo -u postgres psql 
    postgres =# create database sample;
    \q
    sudo -u postgres psql sample < order-db.sql
    sudo -u postgres psql sample
    sample =# select * from pg_tables;
    \q
    ```

1.  Take a backup of sample database in  "TAR" format 

    ```bash
    sudo -u postgres pg_dump -F t -f /var/lib/pgsql/backups/backup2.tar -d sample
    ls -lh /var/lib/pgsql/backups/backup2.tar
    ```

1.  Restore the backup in NEW database.

    ```bash
    sudo -u postgres psql 
    postgres =# create database sample2;
    \q
    sudo -u postgres pg_restore /var/lib/pgsql/backups/backup2.tar -F t -d sample2
    sudo -u postgres psql sample2
    sample2 =# select * from pg_tables;
    \q
    ```