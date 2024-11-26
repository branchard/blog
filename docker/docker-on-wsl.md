# Install Docker on WSL 2.3 (without Docker Desktop)
On Windows, the standard method for using Docker involves installing Docker Desktop alongside WSL.

However, this approach has several significant drawbacks. It requires manually starting Docker Desktop alongside WSL, consumes considerable system resources due to virtual machines it relies on, and frequently suffers from connection issues between Docker Desktop and WSL.

Although Docker Desktop provides a graphical interface to manage containers and monitor resources, these benefits are relatively minor compared to the constraints it introduces.

While many tutorials cover this topic, they often rely on outdated versions of WSL and introduce unnecessary complexity.

So, this guide explains how to install and configure Docker directly on WSL 2.3 or higher, without the need for Docker Desktop.

## Prerequisites
- WSL 2.3 or higher
- A working and up-to-date Ubuntu distribution

## Installation
- Update the repository and add the missing packages: 
```shell
sudo apt update && sudo apt install ca-certificates curl
```
- Add keyrings:
```shell
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
echo \\n  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \\n  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \\n  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
- Install docker and some plugins (The docker-buildx-plugin is useful for advanced multi-platform builds, and docker-compose-plugin enables the use of docker compose commands):
```shell
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
- To be able to use Docker without using "sudo" and without being root user, we will have to add a new group and add our user to this group:
```shell
sudo groupadd docker
sudo usermod -aG docker $USER
```
- Log out and log back
- Verify that the installation is successful:
```shell
docker run hello-world
docker ps -a
```

Congratulations, you have now successfully installed Docker on WSL.