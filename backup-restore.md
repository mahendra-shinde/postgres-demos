# Postgres Backup and Restore

1.  Connect PSQL and Verify the `products` table

    ```bash
    sudo -u postgres psql
    postgres =# select * from products;
    # Expected at least single record
    \q
    ```

1.  Take `Plain Text` backup 

    ```bash
    sudo -u postgres pg_dump -f /var/lib/pgsql/backups/backup1.txt 
    ## Check the size of file
    ls -lh /var/lib/pgsql/backups/backup1.txt 
    ## View contents of Text file
    cat /var/lib/pgsql/backups/backup1.txt 
    ```

1.  Modify the database (Trigger data loss)

    ```bash
    sudo -u postgres psql
    # Delete all records
    postgres =# delete from products;
    # Fetch records
    postgres =# select * from products;
    # Expected ZERO records
    \q
    ```

1.  Recover data from Plain text backup and verify

    ```bash
    sudo -u postgres psql < /var/lib/pgsql/backups/backup1.txt 
    sudo -u postgres psql
    postgres =# select * from products;
    # Expected at least single record
    \q
    ```