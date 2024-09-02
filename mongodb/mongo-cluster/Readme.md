# Mongo DB Cluster (H.A.) with One primary and Two secondaries

1. Create a folder c:\mongo-cluster and copy [docker-compose file](./compose.yml) file into it.
1. Open this folder in VSCode and Launch VSCode Terminal. 
1. Deploy three containers in single compose file, All these are mongo-db instances which are `NOT YET IN CLUSTER`

    ```bash
    docker-compose up -d
    docker-compose ps
    ```

1. Notice, One container is named as `mongo-primary` container, you must connect to primary container and run following command to setup/configure cluster.

    ```bash
    docker-compose exec -it mongo-primary bash
    mongosh --authenticationDatabase admin
    use admin
    rs.status()
    # Expect an ERROR : NotYetInitialized
    ```

1.  Now, you must be inside MongoSH (Mongo-shell) with prompt `admin>` 
    Use following script to initialize your mongo-db replication.

    ```mongosh
    rs.initiate({
        _id: "rs0",
        members: [
            { _id: 0, host: "mongo-primary:27017" },
            { _id: 1, host: "mongo-secondary1:27017" },
            { _id: 2, host: "mongo-secondary2:27017"}

        ]
    })

    ```

1.  Wait for a minute, then use following command to display `Replication Status`

    ```bash
    rs.status()
    # The prompt should be updated
    # rs0 (Direct: primary ) admin>
    exit
    exit
    ```

    > Try to check status from secondary nodes as well !

    ```bash
     docker-compose exec -it mongo-secondary1 bash
    mongosh --authenticationDatabase admin
    use admin
    rs.status()
    ```

    ```bash
    docker-compose exec -it mongo-secondary2 bash
    mongosh --authenticationDatabase admin
    use admin
    rs.status()
    ```

1.  Connect back to primary instance and create a new collection and document.

    ```bash
    docker-compose exec -it mongo-primary bash
    mongosh --authenticationDatabase admin
    use admin
    db.createCollection("movies")
    db.movies.insertOne( { title: "Sholay", year: "1975" })
    exit
    exit
    ```

1.  Connect Secondary1 and check if data is replicated there as well !

    ```bash
    docker-compose exec -it mongo-secondary1 bash
    mongosh --authenticationDatabase admin
    use admin
    show collections
    db.movies.findOne()
    exit
    exit
    ```