# AreTomo Docker Container Guide
1. Download the Containers
To download the containers from Docker Hub, use the following commands:

```
docker pull gimel12/aretomo:1.3.4
docker pull gimel12/aretomo:interactive
```
2. Running the Non-Interactive Session
To run the AreTomo container in a non-interactive session:

```
docker run --gpus all --shm-size=1g --ulimit memlock=-1 --ulimit stack=67108864 gimel12/aretomo:1.3.4
```
3. Running the Interactive Session
To run the AreTomo container in an interactive session:

```
docker run --gpus all -it --shm-size=1g --ulimit memlock=-1 --ulimit stack=67108864 gimel12/aretomo:interactive
```
4. Connecting a Volume to the Container
To connect a volume from your host machine to the container, use the -v option with the docker run command. This allows the container to access files and directories on the host.

For example, to mount the directory /home/user/data from your host machine to the directory /mnt/data in the container, use the following command:

For the non-interactive container:

```
docker run --gpus all --shm-size=1g --ulimit memlock=-1 --ulimit stack=67108864 -v /home/user/data:/mnt/data gimel12/aretomo:1.3.4
```
For the interactive container:

```
docker run --gpus all -it --shm-size=1g --ulimit memlock=-1 --ulimit stack=67108864 -v /home/user/data:/mnt/data gimel12/aretomo:interactive
```
In these examples:

/home/user/data is the directory on the host machine.
/mnt/data is the directory inside the container where the host directory will be mounted.
## Summary of Commands
Download Containers:
```
docker pull gimel12/aretomo:1.3.4
docker pull gimel12/aretomo:interactive
```
Run Non-Interactive Session:

```
docker run --gpus all --shm-size=1g --ulimit memlock=-1 --ulimit stack=67108864 gimel12/aretomo:1.3.4
```
Run Interactive Session:

```
docker run --gpus all -it --shm-size=1g --ulimit memlock=-1 --ulimit stack=67108864 gimel12/aretomo:interactive
```
## Connect Volume for Data:

Non-Interactive:
```
docker run --gpus all --shm-size=1g --ulimit memlock=-1 --ulimit stack=67108864 -v /home/user/data:/mnt/data gimel12/aretomo:1.3.4
```
Interactive:
```
docker run --gpus all -it --shm-size=1g --ulimit memlock=-1 --ulimit stack=67108864 -v /home/user/data:/mnt/data gimel12/aretomo:interactive
```
# Example: Running AreTomo with Specific Data

Assuming you have a folder /home/user/data on your host machine containing the pictures to be processed by AreTomo.

1. Start the Non-Interactive AreTomo Container
Start the AreTomo container with the necessary parameters and mount the data directory:

```
docker run --gpus all --shm-size=1g --ulimit memlock=-1 --ulimit stack=67108864 -v /home/user/data:/mnt/data --name aretomo-container gimel12/aretomo:1.3.4
```
In this command:

The -v /home/user/data:/mnt/data option mounts the /home/user/data directory on your host to the /mnt/data directory inside the container.
The --name aretomo-container option names the container aretomo-container for easier reference.
2. Running Commands Inside the Container
To execute commands inside the running container and process the data, you can use docker exec. Here’s an example of running a command to process the images in the /mnt/data directory:

```
docker exec -it aretomo-container /usr/local/bin/AreTomo /mnt/data
```
In this command:

The -it option allows for interactive processes (in case you need to provide input or view output directly).
aretomo-container is the name of the running container.
/usr/local/bin/AreTomo is the path to the AreTomo executable inside the container.
/mnt/data is the directory containing the data to be processed.

## Putting It All Together
Here’s a complete example guide:

Step 1: Start the Container
```
docker run --gpus all --shm-size=1g --ulimit memlock=-1 --ulimit stack=67108864 -v /home/user/data:/mnt/data --name aretomo-container gimel12/aretomo:1.3.4
```
Step 2: Execute AreTomo Inside the Running Container
```
docker exec -it aretomo-container /usr/local/bin/AreTomo /mnt/data
```

