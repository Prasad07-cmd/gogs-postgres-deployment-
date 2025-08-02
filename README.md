# gogs-postgres-deployment-
Seamless Gogs &amp; PostgreSQL Setup with Docker 🚀 
This project provides a reliable, step-by-step guide to deploying a multi-tier application using Docker. It showcases how to connect a Gogs Git server with a PostgreSQL database on a custom Docker network, ensuring seamless communication and persistent data storage.

Key Features & What You'll Learn
Multi-Container Deployment: Master the art of running two or more containers as a single, cohesive application.

Custom Docker Networking: Learn how to create a dedicated network (skynet) for your containers to enhance security and simplify service discovery.

Persistent Configuration: Mount a host directory to a container to ensure your application's settings are never lost.

Troubleshooting Tips: Avoid common "database connection refused" errors by using correct container-to-container communication.

Easy-to-Follow Commands: Get a simple copy-paste guide to get your local Git server up and running in minutes.

Getting Started
Follow these commands in order to get your Gogs server and PostgreSQL database running on a custom network.

1. Create the custom Docker network
This network provides a dedicated, isolated environment for your containers.

docker network create --subnet=192.168.0.0/16 skynet

2. Deploy the PostgreSQL database container
This command runs the PostgreSQL database, exposing it to the skynet network. The database name, user, and password are set via environment variables.

docker run --name gogsdata --network skynet -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=redhat123 -e POSTGRES_DB=gogsdb -d postgres

3. Create the host directory for Gogs configuration
Create a directory on your host machine to store your Gogs configuration files persistently.

mkdir -p /mnt/gogsinfo

4. Deploy the Gogs Git server container
This command launches the Gogs application, linking it to the same skynet network. We also map port 3000 and mount the gogsinfo directory for persistent storage.

docker run --name mygitserver --network skynet -p 3000:3000 -v /mnt/gogsinfo:/data/gogs/conf -d gogs/gogs

5. Complete the web installation
Open your browser and navigate to http://<your-server-ip>:3000. On the Gogs installation page, use the following database settings:

Database Type: PostgreSQL

Host: gogsdata:5432

User: postgres

Password: redhat123

Database Name: gogsdb

Fill in the remaining fields and click "Install Gogs" to finish the setup.

Technology Stack
Container Runtime: Docker

Git Server: Gogs

Database: PostgreSQL

Conclusion
By correctly leveraging container networking, this guide has shown how to build a robust, multi-tier Docker application. This approach is fundamental to creating scalable and maintainable containerized environments.

Keywords for Visibility
#Docker #DevOps #Containerization #Gogs #PostgreSQL #Networking #GitServer #TechGuide #SysAdmin #OpenSource #Tutorial #README
