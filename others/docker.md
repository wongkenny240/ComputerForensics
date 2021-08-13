---
description: Some docker commands
---

# Docker

### Stop the process

```
 docker stop [OPTIONS] CONTAINER [CONTAINER...]
```


### Procedure to remove file and database

1. Stop the container\(s\) using the following command:

   ```text
   docker-compose down
   ```

2. Delete all containers using the following command:

   ```text
   docker rm -f $(docker ps -a -q)
   ```

3. Delete all volumes using the following command:

   ```text
   docker volume rm $(docker volume ls -q)
   ```

4. Restart the containers using the following command:

   ```text
   docker-compose up -d
   ```

