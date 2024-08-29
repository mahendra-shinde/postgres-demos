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
    Description: This variable lists the PostgreSQL nodes (primary and secondary) that Pgpool-II will manage.
    Format: The value is a comma-separated list where each entry follows the format <ID>:<HOSTNAME>:<PORT>.
    Example: 0:postgres-primary:5432,1:postgres-secondary:5432
        0 and 1 are identifiers for the nodes.
        postgres-primary and postgres-secondary are the hostnames of the PostgreSQL containers.
        5432 is the default port for PostgreSQL.

PGPOOL_SR_CHECK_USER:
    Description: This specifies the PostgreSQL user that Pgpool-II will use to perform health checks on the PostgreSQL nodes. This user should have sufficient privileges to connect to the database and run basic queries.
    Example: your_user
    Note: Ensure that this user exists on all PostgreSQL nodes.

PGPOOL_SR_CHECK_PASSWORD:
    Description: The password for the user specified in PGPOOL_SR_CHECK_USER. This password is used during the health checks to authenticate the user.
    Example: your_password

PGPOOL_ADMIN_USER:
    Description: The administrative user for Pgpool-II's internal management interface. This user can be used to access Pgpool-II's administrative tools, such as the Pgpool-II admin console.
    Example: admin

PGPOOL_ADMIN_PASSWORD:
    Description: The password for the Pgpool-II administrative user defined in PGPOOL_ADMIN_USER.
    Example: admin_password