### Attaching to a background docker container

Sometimes, you just want to ssh / bash into a running docker container

Old way:
```
$ docker attach <docker-id>
```

New way:
```
$ docker exec -it <docker-id> bash
```

[source](http://askubuntu.com/questions/505506/how-to-get-bash-or-ssh-into-a-running-container-in-background-mode)
