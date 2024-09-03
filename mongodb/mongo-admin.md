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
    mongodump -u root -p pass1234 -d admin -c movies -o /opt/bitnami/mongodb/backups/admin/
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