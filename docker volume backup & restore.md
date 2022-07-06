## Backup

```bash
docker cp CONTAINER:/MOUNT_POINT_OF_VOLUME ./LOCAL_FOLDER
```

### Create tar archive

```bash
tar cvf backup.tar -C LOCAL_FOLDER .
```

copy to other host using sftp or something

## Restore

```bash
docker run -v VOLUME_NAME:MOUNT_POINT --name CONTAINER_NAME -d alpine
```

```bash
docker cp - CONTAINER_NAME:MOUNT_POINT < backup.tar
```

Data will be stored in VOLUME_NAME

Container can be removed afterwards

```bash
docker container rm CONTAINER_NAME
```

