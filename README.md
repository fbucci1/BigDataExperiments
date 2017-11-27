# BigDataExperiments

Setup development environment using Docker:

# Install docker
[Instructions here](https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/#install-using-the-repository)

# Install docker-compose
[Instructions here](https://docs.docker.com/compose/install)

# Setup Portainer
```
$ docker run --name portainer1 -d -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock --restart always portainer/portainer
```

# Setup Dokuwiki
```
docker network create dokuwiki-tier
docker run --name dokuwiki1 -it -d -p 80:80 -p 443:443 -v /docker_volumes/dokuwiki1:/bitnami --net dokuwiki-tier -e DOKUWIKI_USERNAME=administrador --restart always bitnami/dokuwiki:latest
```
Install template. http://www.inmotionhosting.com/support/edu/dokuwiki/change-dokuwiki-appearance/change-template-dokuwiki. E.g. https://www.dokuwiki.org/template:writr restart is needed in order to pick up new template.

# Setup Jenkins
```
mkdir /docker_volumes/jenkins1/jenkins_home/
chmod guo+rw /docker_volumes/jenkins1/jenkins_home/
docker run --name jenkins1 -it -p 8080:8080 -v /docker_volumes/jenkins1/jenkins_home:/var/jenkins_home jenkins/jenkins:lts
```

# Setup Sonar
```
sudo docker run --name sonarqube1 -it -d -p 9002:9000 -p 9092:9092 sonarqube
```

# Setup Postgresql
```
docker run --name postgres1 -it -p 5432:5432 -v /docker_volumes/postgres1/data:/var/lib/postgresql/data -e POSTGRES_PASSWORD=apassword  postgres:latest
```

# Setup Hadoop, Spark, Spark-notebook.
Notice only ext folder is mounted as a volume, therefore only notebooks in there are save outside the container.
```
sudo docker run --name spark-notebook1 -p 9001:9000 -v /docker_volumes/spark-notebook1/notebooks_ext:/opt/docker/notebooks/ext andypetrella/spark-notebook:0.9.0-SNAPSHOT-scala-2.11.8-spark-2.2.0-hadoop-2.7.2-with-hive
```
# Setup Hive.
```
docker run --name hive1 -d -p 10000:10000 gillax/hive:latest
#and exec hiveserver2
docker exec -d hive hiveserver2
#run jdbc sample application
./gradlew runApp
```
