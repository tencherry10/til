### Cleanup Old Docker Container


List all exited containers: ```docker ps -aq -f status=exited```

List dangling/untagged images: ```docker images -q --filter dangling=true```

Remove all exited container: ```docker ps -aq -f status=exited --no-trunc | xargs docker rm ```

Remove all dangling images: ```docker images -q --filter dangling=true | xargs docker rmi```
