# docker-cheatsheet
Docker cheat-sheet contains all the basic and advance Docker commands. I will update this repo time to time with latest commands and updates. 

### Docker Version Check
`docker version`

### SSH into default machine(Only for windows)
`docker-machine ssh default`


`docker run hello-world`

`docker create hello-world`

### Shorthand for Run and Create command
`docker start -a hello-world`

### Check Logs
`docker logs <container id>`

`docker run busybox echo hi there`

### Checking all running containers
`docker ps`

### Checking all containers(Including Stopped one's)
`docker ps -a` 

### Delete All
`docker system prune`

### Stop Container
`docker stop <container id>` //takes sometime to stop

`docker kill <container id>`

### Executing Commands inside container
`docker exec -it <container_id> <command>`

//for example

`docker run -d redis`

`docker exec -it redis redis-cli` //with open redis cli

`docker exec -it redis sh` //will open shell or /bin/bash 

### Building Docker file
`docker build .` //build dockerfile

### Dockerfile Commands
* FROM
* WORKDIR
* COPY
* ENV
* RUN
* EXPOSE
* CMD

### Building with noCache
`docker build --no-cache .`

### Building with Tag
`docker build -t <dockerid>/<name>:<version> .`

### Dockerfile for nodejs

```
FROM node:8

WORKDIR /usr/app

COPY ./package* ./

RUN npm install

COPY ./ ./

EXPOSE 8080

CMD ["npm","start"]
```

# Some Basic Docker Compose Commands
### Start Application
`docker-compose up`

### Build App before Starting 
`docker-compose up --build`

### Running in detached Mode
`docker-compose up -d`

### Stopping Application
`docker-compose down`

### Listing Running Containers
`docker-compose ps`

### If Dockerfile name is changed
`docker build -f Dockerfile.dev .`

### Volumes Basics
```javascript
docker run -p 3000:3000 -v /app/node_modules -v $(pwd):/app <name>
//I am adding two volumes because I want my container to reference node_modules folder of container and not host.

//In docker-compose.yml file
volumes:
  - /app/node_modules
  - .:/app
```

### Overriding command mentioned in Dockerfile 
`command: ["npm","test"]`

## Multi step Builds
```
FROM node:alpine as builder
WORKDIR /usr/app
COPY ./package* ./
RUN npm install
COPY ./ ./
RUN npm run build

FROM nginx:latest
COPY --from=builder /app/build /usr/share/nginx/html

```
	


