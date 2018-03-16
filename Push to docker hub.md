1. Log in on https://hub.docker.com/
2. Click on Create Repository.
3. Choose a name (e.g. jenkins) and a description for your repository and click Create.
4. Log into the Docker Hub from the command line
docker login --username=tuankhoi
Enter password
5. Tag image
docker tag <image_id> tuankhoi/jenkins:latest
6. Push image
docker push tuankhoi/jenkins
