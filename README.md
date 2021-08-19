# docker-part1

## 1.1

```
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS                      PORTS     NAMES
3a1384665abb   nginx     "/docker-entrypoint.…"   3 minutes ago   Exited (0) 25 seconds ago             brave_yonath
c2d283c6508f   nginx     "/docker-entrypoint.…"   4 minutes ago   Exited (0) 9 seconds ago              mystifying_sutherland
89e4514bfc12   nginx     "/docker-entrypoint.…"   5 minutes ago   Up 5 minutes                80/tcp    objective_cerf
```

## 1.2

```
docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

docker images
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
```

## 1.3

```
docker run -d -it --name simple devopsdockeruh/simple-web-service:ubuntu
docker exec -it simple bash
tail -f ./text.log
Secret message is: 'You can find the source code here: https://github.com/docker-hy'
```

## 1.4

```
docker run -d -it --name site ubuntu
docker exec -it site bash
apt-get update
apt-get install curl
sh -c 'echo "Input website:"; read website; echo "Searching.."; sleep 1; curl http://$website;'
helsinki.fi
```

## 1.5

```
REPOSITORY                          TAG       IMAGE ID       CREATED        SIZE
devopsdockeruh/simple-web-service   ubuntu    4e3362e907d5   5 months ago   83MB
devopsdockeruh/simple-web-service   alpine    fd312adc88e0   5 months ago   15.7MB

docker run -d -it --name alp devopsdockeruh/simple-web-service:alpine
docker exec -it alp sh
tail -f ./text.log
Secret message is: 'You can find the source code here: https://github.com/docker-hy'
```