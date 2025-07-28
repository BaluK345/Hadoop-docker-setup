Hadoop Setup using Docker on Ubuntu
This project demonstrates how to install and run a single-node Hadoop cluster (NameNode + DataNode) using Docker on Ubuntu.

##🚀 Prerequisites
-Ubuntu OS

-Docker installed

##🐳 Install Docker
''bash

-sudo apt update
-sudo apt install docker.io
-sudo systemctl enable docker --now
##Verify Docker installation:

''bash

-docker --version

##⚙️ Setup Instructions
Step 1: Configure Docker Permissions
''bash
-sudo usermod -aG docker $USER
-newgrp docker
-docker ps

Step 2: Pull Hadoop Docker Images
''bash
-docker pull bde2020/hadoop-namenode:2.0.0-hadoop3.2.1-java8
-docker pull bde2020/hadoop-datanode:2.0.0-hadoop3.2.1-java8

Step 3: Create Docker Network
''bash
-docker network create hadoop-net

Step 4: Run NameNode Container
''bash
-docker run -d \
  --net hadoop-net \
  --name namenode \
  -p 9870:9870 \
  -e CLUSTER_NAME=test \
  bde2020/hadoop-namenode:2.0.0-hadoop3.2.1-java8
Access Hadoop NameNode UI:
http://localhost:9870

Step 5: Run DataNode Container
''bash
-docker run -d \
  --net hadoop-net \
  --name datanode \
  -e CLUSTER_NAME=test \
  bde2020/hadoop-datanode:2.0.0-hadoop3.2.1-java8

##📊 Container Management
Start Containers

''bash
-docker start namenode
-docker start datanode
-Stop Containers

''bash
-docker stop namenode
-docker stop datanode
-Restart Containers

''bash
-docker restart namenode
-docker restart datanode
-Check Running Containers

''bash
-docker ps
-View Logs

''bash
-docker logs namenode
-docker logs datanode
-Remove Containers (Optional)

''bash
-docker rm namenode
-docker rm datanode
-docker network rm hadoop-net
✅ Notes
Ensure Docker is running before using commands.

To work inside containers:

''bash
-docker exec -it namenode /bin/bash
-docker exec -it datanode /bin/bash
Use hdfs commands inside the containers as needed.

🎉 Hadoop Cluster Ready!
Your single-node Hadoop cluster using Docker is now running and ready to use!

Let me know if you want an extended version with multiple DataNodes or Spark integration.
