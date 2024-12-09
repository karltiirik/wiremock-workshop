# Requirement
Docker installed and accessible from shell:
```shell
docker -v
```

# Start WireMock container
Starts in the service, detach and return to terminal prompt. 
```shell
docker compose up --detach
```

# Links
* List of all mappings: http://localhost:8080/__admin/mappings
* Mapping created from [static-endpoint.json](mappings/mappings.json): http://localhost:8080/static-endpoint
* File served directly: http://localhost:8080/example-file.txt
* File contents served: http://localhost:8080/file-response-endpoint
* Admin API OpenAPI description: https://wiremock.org/docs/standalone/admin-api-reference/

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