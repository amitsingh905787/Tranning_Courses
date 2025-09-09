What are Containers?

Think of a container like a lightweight, portable box that carries everything your application needs to run – the code, libraries, dependencies, and settings.

Unlike virtual machines, containers don’t need a full operating system, so they’re smaller and faster.

They ensure your app works the same everywhere – on your laptop, a server, or in the cloud.

🔹 What is Docker?

Docker is a platform/tool that makes it super easy to create, run, and manage containers.

Without Docker → You’d manually set up environments.

With Docker → Just one command and your app runs in a container.

👉 Think of Docker as the shipping company that packs your app into a container and moves it anywhere you want.

🔹 Why Do You Need Docker?

Consistency → Works the same on dev, test, and production.

Speed → Containers start in seconds.

Efficiency → Uses fewer resources than VMs.

Portability → Run anywhere (Windows, Mac, Linux, Cloud).

Scalability → Spin up multiple copies of your app easily.

🔹 What Can Docker Do?

Package apps into containers.

Run apps anywhere with one command.

Manage container networking.

Scale apps using Docker Swarm or Kubernetes.

🔹 Run Docker Containers
# Run an Ubuntu container and open terminal
docker run -it ubuntu bash

# Run Nginx web server
docker run -d -p 8080:80 nginx

# List running containers
docker ps

# Stop a container
docker stop <container_id>

🔹 Create a Docker Image

Create a file called Dockerfile:

# Use Python base image
FROM python:3.9

# Set working directory
WORKDIR /app

# Copy app files
COPY . .

# Install dependencies
RUN pip install -r requirements.txt

# Run app
CMD ["python", "app.py"]


Build the image:

docker build -t my-python-app .


Run the image as a container:

docker run -d -p 5000:5000 my-python-app

🔹 Networks in Docker

Containers can talk to each other using Docker networks.

# Create a network
docker network create mynetwork

# Run two containers in the same network
docker run -d --name db --network mynetwork mysql
docker run -d --name web --network mynetwork nginx

🔹 Docker Compose

Docker Compose lets you manage multi-container apps using a single YAML file.

docker-compose.yml:

version: "3"
services:
  web:
    image: nginx
    ports:
      - "8080:80"
  db:
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: root


Run it with:

docker-compose up -d

🔹 Docker Concepts in Depth

Images → Blueprints for containers.

Containers → Running instances of images.

Volumes → Store persistent data.

Networks → Let containers talk to each other.

Registry → Place to store images (Docker Hub).

🔹 Docker for Windows/Mac

Install Docker Desktop.

Provides a GUI + command line.

Uses lightweight Linux VM under the hood.

🔹 Docker Swarm

Swarm is Docker’s built-in tool for clustering and scaling containers.

# Initialize swarm
docker swarm init

# Deploy a service
docker service create --replicas 3 -p 8080:80 nginx

🔹 Docker vs Kubernetes
Feature	Docker Swarm	Kubernetes
Ease of use	Simple, quick	Complex, powerful
Scaling	Basic scaling	Advanced auto-scaling
Networking	Easy setup	Advanced networking
Industry use	Small/medium apps	Large, enterprise-grade apps

👉 Docker = Creates and runs containers
👉 Kubernetes = Manages containers at scale
