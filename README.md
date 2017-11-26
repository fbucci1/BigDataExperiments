# BigDataExperiments

Setup development environment using Docker:

# Install docker
[Instructions here](https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/#install-using-the-repository)

# Install docker-compose
[Instructions here](https://docs.docker.com/compose/install)

# Setup Portainer
```
$ docker run --name portainer1 -d -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock portainer/portainer
```

# Setup Dokuwiki
```
docker network create dokuwiki-tier
docker run --name dokuwiki1 -it -d -p 80:80 -p 443:443 --net dokuwiki-tier -e DOKUWIKI_USERNAME=administrador -v /docker_volumes/dokuwiki1:/bitnami bitnami/dokuwiki:latest
```

# Setup Jenkins
```
mkdir /docker_volumes/jenkins1/jenkins_home/
chmod guo+rw /docker_volumes/jenkins1/jenkins_home/
docker run --name jenkins1 -it -p 8080:8080 -v /docker_volumes/jenkins1/jenkins_home:/var/jenkins_home jenkins/jenkins:lts
```

# Setup Sonar
```
sudo docker run --name sonarqube1 -it -d -p 9001:9000 -p 9092:9092 sonarqube
```

# Setup Postgresql
```
docker run --name postgres1 -it -v /docker_volumes/postgres1/data:/var/lib/postgresql/data -p 33000:5432 -e POSTGRES_PASSWORD=apassword  postgres:latest
```

# Setup Hadoop, Spark, Spark-notebook.
Notice only ext folder is mounted as a volume, therefore only notebooks in there are save outside the container.
```
sudo docker run --name spark-notebook1 -v /docker_volumes/spark-notebook1/notebooks_ext:/opt/docker/notebooks/ext -p 9001:9000 andypetrella/spark-notebook:0.9.0-SNAPSHOT-scala-2.11.8-spark-2.2.0-hadoop-2.7.2
```
