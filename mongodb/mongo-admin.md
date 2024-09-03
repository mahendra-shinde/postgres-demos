# Mongo Admin Tasks

1.  Stop and delete all running containers and volumes.

    Start Powershell

    ```pwsh
    docker stop %(docker ps -aq)
    docker container prune 
    Delete All ? _Y
    docker volume prune 
    Delete All? _Y
    ```

1.  Launch a new mongodb container instance.

    ```pwsh
    docker run --name mongo1 -e ALLOW_EMPTY_PASSWORD=true -e MONGODB_ROOT_USER=root -e MONGODB_ROOT_PASSWORD=pass1234 -d bitnami/mongodb
    docker ps 
    ```

1.  Launch Two Command Prompts, Run following command on both prompt.

    > Prompt 1 
    ```pwsh
    docker exec -it  -u root mongo1 bash
    ```

    > Prompt 2
    ```pwsh
    docker exec -it  -u root mongo1 bash
    ```

1.  In `Prompt 1` (First Command prompt) use following command to get inside `mongosh` and create collection and documents.

    ```pwsh
    mongosh -u root -p pass1234 
    use admin
    db.createCollection("movies")
    show collections
    db.movies.insertOne(  { _id: 101, title: "Sholay", year: "1975" } )
    db.movies.insertOne( { _id: 102, title: "Kung fu hustle", year: "1990" } )
    ```

1.  In `Prompt 2` (Second command prompt) use following commands to backup `movies` collection

    ```pwsh
    mkdir /opt/bitnami/mongodb/backups
    mongodump -u root -p pass1234 -d admin -c movies -o /opt/bitnami/mongodb/backups
    ```

1.  In `Prompt 1` (First Command prompt) use following command to delete the collection `movies`

    ```pwsh
    use admin
    db.movies.drop()
    show collections
    ## EXPECTED : Collection `movies` not listed !
    ```

1.  In `Prompt 2` (Second command prompt) use following commands to restore `movies` collection

    ```pwsh
    mongorestore -u root -p pass1234 -d admin --dir=/opt/bitnami/mongodb/backups/admin/movies.bson
    ```

1.  In `Prompt 1` (First Command prompt) use following command to verify collection `movies` restored from backup.

    ```pwsh
    use admin
    show collections
    db.movies.find()
    ```

1.  Close both Command prompt windows `prompt 1` and `prompt 2`

## Manage Users

1.   Open TWO command prompts 

    > prompt 1

    ```pwsh
    docker exec -it  -u root mongo1 bash
    ```

    > Prompt 2
    ```pwsh
    docker exec -it  -u root mongo1 bash

1.  Now in `Prompt 1` try to login into mongosh using root user

    ```pwsh
    mongosh -u root -p pass1234
    use appDB
    ```

1.  Create a new user with `reader` role.

    ```bash
    use admin
    show roles # List existing roles
    db.createUser({
        user: "user1",
        pwd: "password",
        roles: [{ role: "read", db: "appDB" }]
    })
    show users
    ```

1.  Now, in `prompt 2` try connecting to mongoshell with new user

    ```pwsh
    ### SYNTAX
    # mongosh -u USERNAME -p PASSWORD 
    mongosh -u user1 -p password 
    use appDB
    db.createCollection("contacts")
    # EXPECTED AN AUTHORIZATION ERROR !
    exit
    ```

1.  Switch back to `Prompt 1` and create another user with `ReadWrite` role.

    ```bash
    use admin
    db.createUser({
        user: "user2",
        pwd: "password",
        roles: [{ role: "readWrite", db: "appDB" }]
    })
    show users
    ```

1.  Switch to `Prompt 1` and try login with new user `user2`

    ```pwsh
    ### SYNTAX
    # mongosh -u USERNAME -p PASSWORD 
    mongosh -u user2 -p password 
    use appDB
    db.createCollection("contacts")
    # EXPECTED SUCCESS !
    exit
    ```    
