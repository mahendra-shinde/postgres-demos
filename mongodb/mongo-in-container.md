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
    test> show databases
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

1.  Create a new collection `movies`

    ```bash
    admin> db.createCollection( 'movies' )
    admin> use movies
    movies> _
    ```

1.  Try finding all the documents in collection `movies`, expect EMPTY response

    ```bash
    movies> db.movies.find( {} )


    ```

1.  Add two new movies

    ```bash
    movies> db.movies.insertOne(  { _id: 101, title: "Sholay", year: "1975" } )

    movies> db.movies.insertOne( { _id: 102, title: "Kung fu hustle", year: "1990" } )

    db.movies.find( {} )
    ```