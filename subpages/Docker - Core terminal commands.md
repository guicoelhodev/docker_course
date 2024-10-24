  

`docker ps -a` - Show all containers (stopped containers too)

`docker start <container-name>` - Start the container but the terminal still can be used by the user.

`-d` - Detached mode - Use this tag when you don't want to block the terminal ( when this option you can’t see logs on the terminal)

`docker logs <container-name>` - See all logs for this container name, if you add `-f` this command will block this terminal

`-it` - Interactive mode, you can press new commands for that application

`docker run --rm` - This `--rm` means that this container should be removed after stopping this container.

---

### Deleting Images and containers

  

`docker rm` - You need to stop the container first

`docker rmi` - Remove the image ( but you need to stop the container first)

`docker images prune`- Remove all images that don’t contain any tag, if you want to delete all tags add `-a` on this command.

---

### Naming and tagging Containers and Images

  

`docker run --name <your-container-name> <image-id>` - Add a name for container

`docker build -t <name-of-tag-image>` - Add tag to image `(ex: node:latest)`

  

### Rename and re-tagging

`docker tag <your-image-name> <new-image-name>`