# question

## 1-1 For which reason is it better to run the container with a flag -e to give the environment variables rather than put them directly in the Dockerfile?
 Passing environment variables with the -e flag when running a container is more secure, flexible, and reusable than hardcoding them in the Dockerfile. It allows for better security of sensitive data, easier updates, and simplifies managing configurations across different environments.

## 1-2 Why do we need a volume to be attached to our postgres container?
Volumes allow data to survive container restarts, upgrades, or recreations, ensuring data durability and backup capability.
so  we need a volume because when we stop the data we ensure that the data won't get lost

## 1-3 Document your database container essentials: commands and Dockerfile.
Run the Postgres container with environment variables and volume
docker run -d --name my-postgres-container --network app-network -e POSTGRES_USER=usr -e POSTGRES_PASSWORD=pwd -e POSTGRES_DB=db -v pgdata:/var/lib/postgresql/data postgres

View logs to see if there is any problem
docker logs my-postgres-container


## 1-4 Why do we need a multistage build? And explain each step of this dockerfile.
To separate the build environment (we used maven) from the final runtime environment, making the final image smaller and more secure. so we have two stages the build one and the runtime

## 1-5 Why do we need a reverse proxy?
We need it to Keeping your backend safe and hiding its address, sharing the work between several servers,
sending requests to the right service under one website, making pages load faster with caching and compression, giving users one easy address to access everything.

## 1-6 Why is docker-compose so important?
Docker Compose allows you to define and manage multiple related containers easily using a single YAML file.

## 1-7 Document docker-compose most important commands.
docker-compose up -d — start in detached mode.
docker-compose down — stop and remove containers, networks.
docker-compose build — build or rebuild images.
docker-compose logs — view logs from services.
docker-compose ps — list running containers.

## 1-8 Document your docker-compose file.
Defines three services, shared network, and persistent volume for Postgres data.
It makes the connection between the the three services database, backend and the httpd. we give where they are build, container name , the depends_on, the port and the network it's on.

## 1-9 Document your publication commands and published images in dockerhub.
I looked wich images I needed with : docker images 
then Tag the images for Docker Hub : docker tag image username/repository:tag
Login to Docker Hub : docker login
Push the image to Docker Hub : docker push username/repository:tag
 
## 1-10 Why do we put our images into an online repo?
To share images with others or between environments.
Enables continuous integration/deployment workflows.
Provides a central storage for versioned images.
Simplifies deployment to production or cloud environments.
Ensures consistency across developer machines and servers.


## 2-1 What are testcontainers?
Docker-based test environments for integration testing, making your tests more realistic and reliable.

## 2-2 For what purpose do we need to use secured variables ?
It's used to secure and protect sensible data in a automized process

## 2-3 Why did we put needs: build-and-test-backend on this job? 
we put needs on a job to make it dependent on the successful completion of the build-and-test-backend job.

## 2-4 For what purpose do we need to push docker images?
We push Docker images to a remote registry to make them accessible from any environment or machine. This allows other developers, servers, or deployment pipelines to pull and run the exact same container, ensuring consistency and reproducibility across development, testing, and production environments. Without pushing, the image remains local and cannot be reused elsewhere

## 3-1 Document your inventory and base commands
Test the connexion : ansible all -i inventories/setup.yml -m ping
get the explotation system of the serveur : ansible all -i inventories/setup.yml -m setup -a filter=ansible_distribution*"
desinstall Apache2 :ansible all -i inventories/setup.yml -m apt -a "name=apache2 state=absent" --become

## 3-2 Document your playbook
The playbook installs and configures Docker on all target servers using a dedicated role called docker. It runs with administrative privileges, gathers system information, and delegates all tasks—such as installing dependencies, adding Docker’s repository, and starting the Docker service—to the role. This structure ensures the playbook is clean, reusable, and easy to maintain.

## 3-3 Document your docker_container tasks configuration
In our Ansible deployment, we used the `docker_container` module to launch three key services: the PostgreSQL database, the backend API, and the HTTP proxy. Each container task specifies the container `name`, the `image` pulled from DockerHub, necessary `environment variables` (like database credentials and URLs), the custom Docker `network` for inter-service communication, and exposed `ports` where needed. We also configured the `ansible_python_interpreter` to use the virtual environment where the Docker SDK is installed, ensuring compatibility. This setup allows automated, reproducible service deployment on the remote server.
