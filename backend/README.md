# Backend build & deploy as docker image

_Install dependencies_

```
npm install -g pkg
```

#### We will build NodeJS app to binary file. It helps reduce application size.

#### We wrap it to docker image using very light os alpine, then push the image to docker hub.

1.  yarn install
2.  yarn build
3.  yarn package
4.  docker build -t manga-server .
5.  docker tag manga-server danghung/manga-server
6.  docker push danghung/manga-server

#### In server production we just pull

7.  docker pull danghung/manga-server
8.  docker run -d --network nginx --link mongodb:mongo danghung/manga-server
