# PostgreSQL in containers

1. Make sure you have docker and docker-compose installed on system.

1. Start Command prompt or Powershell in Windows

1. Use following commands to create a new folder and open VSCode in it.

    ```cmd
    mkdir postgres-db
    code postgres-db
    ```

1. create a file `compose.yml` in VSCode

1. Copy following contents in the new file

    ```yaml
    services:
      postgres:
        image: postgres:latest
        container_name: postgres
        environment:
          POSTGRES_USER: admin
          POSTGRES_PASSWORD: admin123
          POSTGRES_DB: mydatabase
        volumes:
        - postgres_data:/var/lib/postgresql/data
        ports:
        - "5432:5432"
        networks:
        - postgres_network


      pgadmin:
        image: dpage/pgadmin4:latest
        container_name: pgadmin
        environment:
          PGADMIN_DEFAULT_EMAIL: admin@admin.com
          PGADMIN_DEFAULT_PASSWORD: admin123
        ports:
        - "9000:80"
        depends_on:
        - postgres
        networks:
        - postgres_network

    volumes: 
          postgres_data:

    networks:
      postgres_network:
        driver: bridge
    ```
1. In VSCode, goto `Terminal` Menu and use option `New Terminal`
1. use following command to start the database and client app

    ```
    docker-compose up -d
    ```

1.  Verify if both database and pgadmin are UP and RUNNING

    ```
    docker-compose ps
    ```

1.  Access PGAdmin using URL `http://localhost:9000`

1.  Login using Username/password:

    ```ini
    Username=admin@admin.com
    Password=admin123
    ```

1.  On pgAdmin console, click on `Add New Server` and provide connection details:

    ```yaml
    General:
        Name: postgres  # User defined value, can be anything !!!
    Connection:         # Must be exactly same
        Host: postgres 
        Username: admin
        Password: admin123
    ```

1.  Click `Save` button to start connection to server.
1.  Expand the Database Server, goto Databases -> select `mydatabase` then choose `schemas` and then `public`

1.  Right click on `Public` schema and choose options to create table