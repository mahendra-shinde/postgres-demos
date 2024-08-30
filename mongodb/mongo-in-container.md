# Deploy MongoDB in Container

### Launch a container of MongoDB built by vendor "bitnami"

```bash
docker run --name mdb -e ALLOW_EMPTY_PASSWORD=true -d bitnami/mongodb
```

## Verify if Mongo DB Container is RUNNING

```bash
docker ps
```

## Connect Mongo Shell from container mdb

```bash
docker exec -it mdb mongosh
```

## Once connected, the default mongo instance name is "test"
## You should get a Mongo SHell prompt test>

```bash
test> _
```

## List all databases, There is no Semi-colon needed !!!!

```bash
test> show database
```

## Switch to (USE) database "admin"

```bash
test> use admin
```

## Now, the prompt changes to name of database in use

```bash
admin> _
```

## List all collections

```bash
admin> show collections
```
