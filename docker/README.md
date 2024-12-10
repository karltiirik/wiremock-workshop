# Requirement
[Docker installed](https://www.docker.com/get-started/) and accessible from shell:
```shell
docker -v
```

# Start WireMock container
Starts in the service, detach and return to terminal prompt. 
```shell
docker compose up --detach
```

## Restart WireMock
```shell
docker compose restart
```

## Stop WireMock
```shell
docker compose down
```

# Links
* List of all mappings: http://localhost:8080/__admin/mappings
* Mapping created from [static-endpoint.json](mappings/mappings.json): http://localhost:8080/static-endpoint
* File served directly: http://localhost:8080/example-file.txt
* File contents served: http://localhost:8080/file-response-endpoint
* Admin API OpenAPI description: https://wiremock.org/docs/standalone/admin-api-reference/
  * The OpenAPI specification can be downloaded and imported into Postman/Hoppscotch to try out Admin API functionality 
* View specification locally: http://localhost:8080/__admin/docs

# Adding new mapping through WireMock Admin API
Create mapping
```shell
curl -X POST http://localhost:8080/__admin/mappings \
     -H "Content-Type: application/json" \
     -d '{
           "request": {
             "method": "GET",
             "url": "/example"
           },
           "response": {
             "status": 200,
             "body": "This is a mocked response created through Admin API",
             "headers": {
               "Content-Type": "text/plain"
             }
           }
         }'
```
Verify mapping
http://localhost:8080/example

# WireMock with GUI
There is Docker image that extends WireMock with a graphical user interface.

*NB! Make sure that the previous WireMock instance is not running (or anything else on port 8080)*
```shell
docker compose -f docker-compose-gui.yml up -d
```
The GUI is now accessible from http://localhost:8080/__admin/webapp/
