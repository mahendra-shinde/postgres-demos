# PostrgreSQL Cluster with HA

Setting up a PostgreSQL High Availability (HA) cluster using Docker Compose involves orchestrating multiple services such as PostgreSQL nodes, a load balancer, and possibly a replication manager. 

Use [this compose](./compose.yml) file as a reference.

## The Services defined in compose file

1.  Postgres Primary: This is the master node of the PostgreSQL cluster. It handles write operations.

1.  Postgres Secondary: This is the replica node that follows the primary for read operations. It is configured to be in hot standby mode.

1.  Pgpool: Pgpool-II is a middleware that manages connections to the PostgreSQL cluster. It handles load balancing and can also be configured to provide failover capabilities.

1.  pgAdmin: The Client tool to interact with Database. 


Pgpool Environment Variables

PGPOOL_BACKEND_NODES:
    
    This variable lists the PostgreSQL nodes (primary and secondary) that Pgpool-II will manage.
    Format: The value is a comma-separated list where each entry follows the format <ID>:<HOSTNAME>:<PORT>.
    Example: 0:postgres-primary:5432,1:postgres-secondary:5432
        0 and 1 are identifiers for the nodes.
    
    postgres-primary and postgres-secondary are the hostnames of the PostgreSQL containers.
    
    5432 is the default port for PostgreSQL.

PGPOOL_SR_CHECK_USER:
    
    This specifies the PostgreSQL user that Pgpool-II will use to perform health checks on the PostgreSQL nodes. This user should have sufficient privileges to connect to the database and run basic queries.
    Example: your_user
    Note: Ensure that this user exists on all PostgreSQL nodes.

PGPOOL_SR_CHECK_PASSWORD:
    
    The password for the user specified in PGPOOL_SR_CHECK_USER. This password is used during the health checks to authenticate the user.
    Example: your_password

PGPOOL_ADMIN_USER:
    
    The administrative user for Pgpool-II's internal management interface. This user can be used to access Pgpool-II's administrative tools, such as the Pgpool-II admin console.
    Example: admin

PGPOOL_ADMIN_PASSWORD:
    
    The password for the Pgpool-II administrative user defined in PGPOOL_ADMIN_USER.
    Example: admin_password

## Steps

1.  Create a new directory c:\postgres-ha and launch Visual studio code

    ```cmd
    C:
    mkdir postgres-ha
    code postgres-ha
    ```

1.  Inside VS Code, create a new file `compose.yml` and copy the contents of [this](./compose.yml) file.

1.  Save the file (CTRL+S)

1.  Open Terminal (Terminal Menu -> New ) and use following command to launch HA Cluster

    ```bash
    docker-compose up -d
    docker-compose ps
    ```

1.  Access PgAdmin on `localhost:9000` and login using credentials

    ```ini
    Username=admin@admin.com
    Password=admin123
    ```

1.  Connect to pgpool using following connection properties:

    ```yml
    General:
        name: pgpool
    Connection:
        host: pgpool
        user: admin
        password: admin123
    ```

1.  Using the active connection (pgpool), try creating a table and few records.

    ```sql
    CREATE TABLE company (
    COMPANY_ID varchar(6) NOT NULL DEFAULT '',
    COMPANY_NAME varchar(25) DEFAULT NULL,
    COMPANY_CITY varchar(25) DEFAULT NULL,
    PRIMARY KEY (COMPANY_ID)
    );

    INSERT INTO company (COMPANY_ID, COMPANY_NAME, COMPANY_CITY) VALUES
    ('18', 'Order All', 'Boston\r'),
    ('15', 'Jack Hill Ltd', 'London\r'),
    ('16', 'Akas Foods', 'Delhi\r'),
    ('17', 'Foodies.', 'London\r'),
    ('19', 'sip-n-Bite.', 'New York\r');

    commit;
    ```

1.  Now, disconnect the pgpool server and create another connection to `secondary` database.

    ```yml
    General:
        name: second
    Connection:
        Host: postgres-secondary
        User: admin
        Password: admin123

    ```

1.  Try to find a table in `sampledb` of `second` database server (right click -> refresh)