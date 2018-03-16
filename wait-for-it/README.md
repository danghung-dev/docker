Use to wait database. It is helpful when define service in docker-compose. Because all services start same time, when database is not ready, the application cannot run.

Dockerfile
```
FROM xxx
COPY wait-for-it.sh /wait-for-it.sh
RUN chmod +x /wait-for-it.sh
```

Use in docker-compose.yml
```
command: ["/wait-for-it.sh", "mongo:27017"]
```