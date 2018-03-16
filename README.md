# Install docker on Ubuntu
CentOS have permission problem with docker shared volume. So I chose Ubuntu for docker
```
sudo apt-get update
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
sudo apt-get update
sudo apt-get install docker-ce
```

#### Create a user to use docker
We should not use root account.
```
adduser hung
usermod -aG sudo hung
sudo usermod -aG docker hung
```

###### Pull docker we need
```
docker pull jenkins/jenkins:lts
docker pull jwilder/nginx-proxy
docker pull cypress/base:8
docker pull jrcs/letsencrypt-nginx-proxy-companion
docker pull mysql:5.7
docker pull redmine
docker pull node:8.1
```

# Create a Jenkins image that installed docker inside (docker in docker)
Dockerfile
```
Dockerfile
FROM jenkins/jenkins:lts
	MAINTAINER me@danghung.top
	USER root

RUN  apt-get update
RUN  apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
RUN add-apt-repository    "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   xenial \
   stable"

RUN  apt-get update
RUN  apt-get install -y docker-ce
```

Then build  ``` docker build -t jenkins .  ```

#### 1. First run nginx, let's encrypt, jenkins, mongodb
```
docker-compose up -d
```
#### Second run mongo express
```
docker-compose -f docker-compose.mongoexpress.yml up -d
```
