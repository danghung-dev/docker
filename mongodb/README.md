# Backup
We run another mongodb container to run mongodump. Dump file will be in /home/hung/backup folder
```
docker run --rm --link mongodb:mongo -v /home/hung/backup:/backup mongo bash -c 'mongodump --out /backup --host mongo:27017'
```

# Restore
We run another mongodb container to run mongorestore. Input dump folder is /home/hung/backup
```
docker run --rm --link mongodb:mongo -v /home/hung/backup:/backup mongo bash -c 'mongorestore /backup --host mongo:27017'
```

docker run --rm --network nginx --link mongodb:mongo -v /home/hung/mongodb/restore:/backup mongo bash -c 'mongorestore /backup --host mongo:27017'