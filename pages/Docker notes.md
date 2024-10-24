  

- Block quotes

> [!important]  
  > Docker run the exactly same application and environment, you don`t need to worry about install extra tools in that place to run the application  
   
> [!important]  
> Docker is usefull because we (as software developer) have different development and production environments  
   

When you have your docker image, you can build that on your project running this simple command below:

```JavaScript
docker build . 
```

After that, you get the sha of docker image, run this code  
  
```JavaScript
docker run <your-image-id>
```

To add a specific port, you need to add the `-p` tag

```JavaScript
docker run -p 3000:3000 <your-image-id>
```

  

To remove an image running use that  
  

```JavaScript
docker ps

docker stop <image-name>
```
