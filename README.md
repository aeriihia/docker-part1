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

## 1.6

```
docker run -it devopsdockeruh/pull_exercise
Give me the password: basics
You found the correct password. Secret message is:
"This is the secret message"
```

## 1.7

Dockerfile
```
FROM devopsdockeruh/simple-web-service:alpine
CMD server
```

Commands
```
docker build . -t web-server
docker run web-server
```

## 1.8

Dockerfile
```
FROM ubuntu:18.04
WORKDIR /usr/src/app
COPY script.sh .
RUN chmod +x script.sh
RUN apt-get update && apt-get install -y curl
CMD ./script.sh
```

Commands
```
docker build . -t curler
docker run -it curler
```

## 1.9
```
docker run -v "/home/text.log:/usr/src/app/text.log" devopsdockeruh/simple-web-service
```

## 1.10
```
docker run -p 4567:8080 web-server
```

## 1.11

Dockerfile
```
FROM openjdk:8
EXPOSE 8080
WORKDIR /usr/src/app
COPY . .
RUN ./mvnw package
CMD ["java", "-jar", "./target/docker-example-1.1.3.jar"]
```

Commands
```
docker build . -t spring-project && docker run -p 8080:8080 spring-project
```

## 1.12

Dockerfile
```
FROM node
EXPOSE 5000
WORKDIR /usr/src/app
COPY . .
RUN npm install
RUN npm run build
RUN npm install -g serve
CMD ["serve", "-s", "-l", "5000", "build"]
```

Commands
```
docker build . -t example-frontend && docker run -p 5000:5000 example-frontend
```

## 1.13

Dockerfile
```
FROM golang:1.16
EXPOSE 8080
WORKDIR /usr/src/app
COPY . .
RUN go build
CMD ./server
```

Commands
```
docker build . -t example-backend && docker run -p 8080:8080 example-backend
```

## 1.14

Dockerfile (Frontend)
```
FROM node
EXPOSE 5000
ENV REACT_APP_BACKEND_URL=http://localhost:8080
WORKDIR /usr/src/app
COPY . .
RUN npm install
RUN npm run build
RUN npm install -g serve
CMD ["serve", "-s", "-l", "5000", "build"]
```

Dockerfile (Backend)
```
FROM golang:1.16
EXPOSE 8080
ENV REQUEST_ORIGIN=http://localhost:5000
WORKDIR /usr/src/app
COPY . .
RUN go build
CMD ./server
```

Commands
```
docker build . -t example-frontend && docker run -p 5000:5000 example-frontend
docker build . -t example-backend && docker run -p 8080:8080 example-backend
```

## 1.16
https://thawing-savannah-73156.herokuapp.com/