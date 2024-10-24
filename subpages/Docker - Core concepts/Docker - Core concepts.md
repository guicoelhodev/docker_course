  

`Images` are the template/blueprints for `containers`, that contain code + required tools/ runtime

  

![[Untitled.png]]

  

- You can add `-it` tag to add interactive terminal

```JavaScript
docker run -it node
```

> [!important]  
> This command you can use node inside the container, you don’t need to install node on your local machine to this work.  

---

## Creating an image

  

```JavaScript
FROM node 
WORKDIR /app
COPY package.json /app
RUN npm install
COPY . ./

EXPOSE 8080
CMD ["node", "server.js"]
```

  

- `FROM` - this command will try to get your local image or try to get on docker hub image to download

  

- `COPY . /app` - The first dot means that all files should be copied for this image while the second dot means that is the path inside of the image where these files should be stored.
    
    Note that we have added `WORKDIR` command, this means that we don’t need to add `COPY . /app` because docker understands that the work directory is the `/app`
    

  

- Difference between `CMD` and `RUN` command. The `RUN` command always runs when loading the image, but `CMD` only run if the container has started.

  

- `EXPOSE` exposes what port is enabled to use

  

After that, run `docker build .` then

```JavaScript
docker run -p 3000:8080 <your-image-id>
```

  

- `3000` is a local computer port, and `8080` it’s the port that is running the server on docker container

---

### Image layers

  

- Every instruction in an image creates a cacheable layer - layers help with image re-building and sharing

---