## Rereference Links 
- Tutorial Video - https://youtu.be/6YZvp2GwT0A 
- Original Github - https://github.com/devopsjourney1/jenkins-101
- My Github - https://github.com/palashencode/devops-jenkins-101
- Official Docs - https://www.jenkins.io/doc/
- Jenkins Docker Install - https://www.jenkins.io/doc/book/installing/docker/

## Combined Commands
``` bash

# Build the Jenkins BlueOcean Docker Image
docker build -t myjenkins-blueocean:2.414.2 .
docker pull devopsjourney1/jenkins-blueocean:2.332.3-1 && docker tag devopsjourney1/jenkins-blueocean:2.332.3-1 myjenkins-blueocean:2.332.3-1

# create network
docker network create jenkins

# Windows
docker run --name jenkins-blueocean --restart=on-failure --detach `
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 `
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 `
  --volume jenkins-data:/var/jenkins_home `
  --volume jenkins-docker-certs:/certs/client:ro `
  --publish 8080:8080 --publish 50000:50000 myjenkins-blueocean:2.414.2

# Get Password - https://localhost:8080/
docker exec jenkins-blueocean cat /var/jenkins_home/secrets/initialAdminPassword

# Get Docker Host IP
docker run -d --restart=always -p 127.0.0.1:2376:2375 --network jenkins -v /var/run/docker.sock:/var/run/docker.sock alpine/socat tcp-listen:2375,fork,reuseaddr unix-connect:/var/run/docker.sock

docker inspect <container_id> | grep IPAddress

# Jenkins Python Agent 
docker pull devopsjourney1/myjenkinsagents:python

```
