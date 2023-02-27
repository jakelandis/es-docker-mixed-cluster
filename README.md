Mixed Cluster Docker for testing
----------

Optional - clean start

```
docker image prune -a # removes all docker images
```

Build local docker distribution for both versions

```bash
./gradlew :distribution:docker:assemble # elder 

or

./gradlew :distribution:docker:buildDockerImage #newer

```

Ensure both docker images are installed.
```bash
docker images | grep elasticsearch
```

Update `docker-compose.yml` with the desired versions 

Run
```bash
docker-compose up
```

Ensure all 3 are running and in the same cluster:
```bash
curl localhost:9200/_cat/nodes?v
```

Double check the versions and send command directly to desired host

```bash
curl -v localhost:9200
curl -v localhost:9201
curl -v localhost:9202
```

Optional: In `docker-compose.yml` uncomment Kibana and point it to the desired host.


To stop a node
```
docker-compose stop elasticsearch[1|2|3]
```

To upgrade a node, change the version then
```bash

docker-compose up -d --no-deps elasticsearch[1|2|3]
```

Double check the versions and send command directly to desired host

```bash
curl -v localhost:9200
curl -v localhost:9201
curl -v localhost:9202
```