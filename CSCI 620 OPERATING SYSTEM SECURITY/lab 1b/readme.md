# Multics on Docker - Step-by-Step Guide

This guide will walk you through setting up and running a Multics environment using Docker. Follow the steps below to get started.

## Prerequisites
- Ensure you have [Docker](https://docs.docker.com/get-docker/) installed on your system.
- Basic knowledge of using the terminal/command prompt.
- https://www.youtube.com/watch?v=ZyBBv1JmnWQ

```sh
sudo apt update
mkdir lab1b
cd lab1b
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh

sudo usermod -aG docker $USER
newgrp docker
docker run hello-world
```

## Step 1: Pull the Multics Docker Image
First, download the pre-built Multics image from Docker Hub by running the following command:

```sh
docker pull rattydave/alpine-multics
```

This will fetch the latest version of the Multics container image.

## Step 2: Run the Multics Container
Once the image is downloaded, start a new container using:

```sh
docker run -d --name multics -p 6180:6180 rattydave/alpine-multics:latest
```

Explanation of the command:
- `-d` runs the container in detached mode (in the background).
- `--name multics` assigns a name to the container.
- `-p 6180:6180` maps the container's port 6180 to your host system, allowing external connections.
- `rattydave/alpine-multics:latest` specifies the image to use.

## Step 3: Connect to the Multics System
Once the container is running, use Telnet to connect to it:

```sh
telnet 127.0.0.1 6180
```

If Telnet is not installed, you may need to install it first:
- On Ubuntu/Debian: `sudo apt install telnet`
- On macOS: `brew install telnet`
- On Windows: Enable the Telnet client via Control Panel or install a Telnet application like PuTTY.

## Step 4: Login to Multics
After connecting via Telnet:
1. Press **Enter** to select the first HSLA port. You should see a login banner. example d.h000
2. Enter the following login command:

   ```
   login Repair.SysAdmin -cpw
   ```

3. When prompted for the password, enter:

   ```
   repair

   Change password:
   in my case 1234
   ```

4. You will be asked to set a new password. Enter a new password twice.
5. Once logged in, try executing some basic commands, such as:

   ```
   who
   ```

## Step 5: Exiting Multics
When you are done, log out by typing:

```sh
logout
```

To stop the container:

```sh
docker stop multics
```

To remove the container (optional):

```sh
docker rm multics
```

- If you want to access the container logs:

  ```sh
  docker logs multics
  ```

- If you need an interactive shell inside the container:

  ```sh
  docker exec -it multics /bin/sh
  ```

This concludes the setup and usage guide for running Multics using Docker. Happy exploring!

