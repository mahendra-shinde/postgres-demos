# Mongo DB Cluster (H.A.) with One primary and Two secondaries

1. Deploy three containers in single compose file, All these are mongo-db instances which are `NOT YET IN CLUSTER`

    ```bash
    docker-compose up -d
    docker-compose ps
    ```

1. Notice, One container is named as `master` container, you must connect to master container and run following command to setup/configure cluster.

    ```bash
    docker exec -it mongo-primary mongo -u admin -p admin123 --authenticationDatabase admin
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
    ```

    > Try to check status from secondary nodes as well !