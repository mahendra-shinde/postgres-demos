# Deploy MongoDB in Container

1.  Launch a container of MongoDB built by vendor "bitnami"

    ```bash
    docker run --name mdb -e ALLOW_EMPTY_PASSWORD=true -d bitnami/mongodb
    ```

1.  Verify if Mongo DB Container is RUNNING

    ```bash
    docker ps
    ```

1.  Connect Mongo Shell from container mdb

    ```bash
    docker exec -it mdb mongosh
    ```

1.  Once connected, the default mongo instance name is "test"

1.  You should get a Mongo SHell prompt test>

    ```bash
    test> _
    ```

1.  List all databases, There is no Semi-colon needed !!!!

    ```bash
    test> show database
    ```

1.  Switch to (USE) database "admin"

    ```bash
    test> use admin
    ```

1.  Now, the prompt changes to name of database in use

    ```bash
    admin> _
    ```

1.  List all collections

    ```bash
    admin> show collections
    ```
