# How to setup jenkins as a docker compose service

To setup jenkins on premise we should consider it installing inside a docker container and mounting the volumes to the local volumes os that the jobs will persist locally.

The docker compose service will look like this

```yaml
  jenkins:
    image: jenkins/jenkins:lts
    ports:
      - "8080:8080"
    networks:
      - jenkins-network
    volumes:
      - jenkins_home:/var/jenkins_home
```

# Steps to do after installing jenkins

###### Install java
######  Initial admin password 
```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

###### Enable jenkins
```bash
sudo systemctl enable jenkins
sudo systemctl start jenkins
```

###### Install docker
```bash
sudo apt install docker

sudo systemctl enable docker
sudo systemctl start docker
```

###### Adding jenkins and current user to docker group
```bash
sudo usermod -aG docker current_user
sudo usermod -aG docker jenkins
sudo usermod -aG jenkins current_user
```


