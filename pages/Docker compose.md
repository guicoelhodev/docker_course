  

> [!important]  
> Docker compose is not suited for managing multiple containers on different hosts (machines)Docker compose create your own network for that service  

  

1. create `docker-compose.yaml`

  

By default, if you brings the services down, docker compose automatically remove your containers

When you add named containers, keep attention on that:

  

```JavaScript
version: "3.8"
services: 
  mongodb:
    image: 'mongo'
    volumes: 
      - data:/data/db
    # environment:
      \#MONGO_INITDB_ROOT_USERNAME: coelho
      \#MONGO_INITDB_ROOT_PASSWORD: dev
      # - MONGO_INITDB_ROOT_USERNAME=coelho (another option)
    env_file:
      - ./env/mongo.env
  # backend:
  # frontend:
volumes: 
  data:
```

  

- Add volumes key with data name

  

After that, set this command on your terminal `docker-compose up`

To stop uses `docker-compose down`

If you can delete your volume, add `docker-compose down -v`

  

```JavaScript
version: '3.8'
services: 
  mongodb:
    image: 'mongo'
    volumes: 
      - data:/data/db
    # environment:
      \#MONGO_INITDB_ROOT_USERNAME: coelho
      \#MONGO_INITDB_ROOT_PASSWORD: dev
      # - MONGO_INITDB_ROOT_USERNAME=coelho (another option)
    env_file:
      - ./env/mongo.env
  backend:
    build: ./backend
    # build: # long form
    #   context: ./backend
    #   dockerfile: Dockerfile # if you has Dockerfile with another name, you need to add this option
    #   args:
    #     some-arg: someValue
    ports:
      - '80:80'
    volumes: 
      - logs:/app/logs
      - ./backend:/app # use relative path do share all backend files. Bind mounts dont need to specify them
      - /app/node_modules
    env_file: 
      - ./env/backend.env
    depends_on:
      - mongodb
  # frontend:
volumes: 
  data:
  logs:
```

  

### Adding the frontend service

```JavaScript
version: '3.8'
services: 
  mongodb:
    image: 'mongo'
    volumes: 
      - data:/data/db
    # environment:
      \#MONGO_INITDB_ROOT_USERNAME: coelho
      \#MONGO_INITDB_ROOT_PASSWORD: dev
      # - MONGO_INITDB_ROOT_USERNAME=coelho (another option)
    env_file:
      - ./env/mongo.env
  backend:
    build: ./backend
    # build: # long form
    #   context: ./backend
    #   dockerfile: Dockerfile # if you has Dockerfile with another name, you need to add this option
    #   args:
    #     some-arg: someValue
    ports:
      - '80:80'
    volumes: 
      - logs:/app/logs
      - ./backend:/app # use relative path do share all backend files. Bind mounts dont need to specify them
      - /app/node_modules
    env_file: 
      - ./env/backend.env
    depends_on:
      - mongodb
  frontend:
    build: ./frontend
    ports:
      - '3000:3000'
    volumes:
      - ./frontend/src:/app/src # if the code changes, the container changes too
    stdin_open: true # This server need input connection (interactive mode)
    tty: true # attach this terminal
    depends_on:
      - backend
volumes: 
  data:
  logs:
```

  

### Useful commands

---

  

`docker-compose build` - just build the images, without up the application

  

You can add `container_name` to specify the name of container