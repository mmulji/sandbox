

https://getkong.org/install/docker/

```shell

# Run the Cassandra database
docker run -d --name kong-database \
              -p 9042:9042 \
              cassandra:2.2

# Run Kong
docker run -d --name kong \
              --link kong-database:kong-database \
              -e "KONG_DATABASE=cassandra" \
              -e "KONG_CASSANDRA_CONTACT_POINTS=kong-database" \
              -p 8000:8000 \
              -p 8443:8443 \
              -p 8001:8001 \
              -p 7946:7946 \
              -p 7946:7946/udp \
              kong

# Check to see if Kong is running
curl http://`docker-machine ip`:8001 | jq .

# Kong UI at:
http://`docker-machine ip`:8080


```
