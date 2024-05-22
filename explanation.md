## About.

This file explains the reasoning behind the order of execution of plays (roles) within the main playbook.

## Order of execution.

1. Update ubuntu
2. Install docker
3. Clone yolo repository
4. Create docker network
5. Create db docker image and container
6. Create backend docker image and container
7. Create frontend docker image and container
8. Configure Nginx

## Explanation of the order above.

### 1. Update ubuntu:

- A new installation of ubuntu comes with just enough to have the operating system up and running. It is thus necessary
  to update packages (aptitude repositories).
- This is a prerequisite to installation of other packages.

### 2. Install docker:

- Yolo website will be served through docker microservices, thus installation of docker follows in the execution line.
- This stage begins with installation of packages required by docker.
- Followed by creation of a directory to store docker's GPG key, and then downloading the key.
- Docker's repository is then added to the list of ubuntu's sources.
- Docker packages are thereafter installed one after the other
- A docker group is thereafter added to the list of system user-groups. This enables docker to own directories and
  execute commands.
- Finally, ensure that docker services' state is running.

### 3. Clone yolo repository:

- Yolomy's source code is downloaded from the hosting site (GitHub in this case) and stored in a custom destination
  folder.
- A list of environment variable is copied to the same directory as above.

### 4. Create docker network:

- A custom docker network is then created and a driver allocated to the network.
- This is crucial before the creation of docker containers so that the containers can be attached to this network.

### 5. Create db docker image and container:

- Creation of db container comes first as it is depended upon by the backend container.
- An image hosted in docker hub is used for the db image.
- A persistent volume within the hosts' file system is created to store the db data.
- A container with appropriate name, ports and volume mapping is created and attached to the custom network created
  above.

### 6. Create backend docker image and container:

- Creation of backend container comes next as it is depended upon by the frontend container.
- Appropriate image name, image tag, container ports and container name are assigned.
- The container is then attached to the network created above.

### 7. Create frontend docker image and container:

- This step comes after the creation of the backend container because it depends on it during execution.
- Appropriate image name, image tag, container ports and container name are assigned.
- The container is then attached to the network created in step four above.

### 8. Configure Nginx:
- Nginx is a web server that can also be used as a reverse proxy.
- It is used in this project to proxy requests to frontend and backend. 
- Like the db container, an image hosted in docker hub is used.
- A configuration file is created and shared in the nginx's volume.