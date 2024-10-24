  

These are two steps that’s we need to get aware of before to create deployments with docker

  

- Bind mounts shouldn’t be used in production
- Containerized apps **might be need a build step**
- Multiples containers projects **might need to split** across multiples hosts/remote machines

  

![[assets/image 2.png|image 2.png]]

  

![[image 1.png]]

  

> [!important]  
> Follow this step after creating a EC2 instance on AWS  

  

![[assets/image 2 2.png|image 2 2.png]]

  

## A Quick view about Security Groups

  

`Inbound rules` - Means what’s groups can have access into your EC2 instance.

`Ooutbound rules` - What’s groups your machine can have access

  

> [!important]  
> This is a first example showing how to deploy a web project doing all major things by yourself, setup EC2, pushing docker image, manage SSH to connect for this EC2 machine  

  

In the next chapter, we are going to see other ways to replace a web project, but less manually and more continuous.