# Frontend build & deploy as docker image

I use nginx to server static file. It's light just 15MB.
I just copy to build folder to /usr/share/nginx/html folder. Nginx will do rest things.

1.  yarn install
2.  yarn build
3.  docker build -t mangaclient .
4.  Push to registry
5.  docker run -d -e "VIRTUAL_HOST=mymanga.com" -v /Users/danghung/projects/manga/client/uploads:/usr/share/nginx/html/uploads mangaclient

### Build frontend project

If you follow above, you don't need this.

1.  Install yarn

curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt-get update && sudo apt-get install yarn

2.  git clone frontend project

3.  copy .env, add environment REACT_APP_BASE_API=https://manga.server.danghung.top/api/v1

4.  yarn install && yarn build

5.  copy uploads (images folder) to build/ folder

### Config Https for frontend

1.  Run nginx docker with volume frontend, conf.d

```
	docker run -d -p 80:80 -p 443:443 \
	    --name nginx-proxy \
	    -v /home/hung/docker/nginx/certs:/etc/nginx/certs:ro \
	    -v /var/run/docker.sock:/tmp/docker.sock:ro \
	    -v /home/hung/docker/nginx/conf.d:/etc/nginx/conf.d \
	    -v /home/hung/docker/nginx/frontend:/var/www \
	    -v /etc/nginx/vhost.d \
	    -v /usr/share/nginx/html \
	    --label com.github.jrcs.letsencrypt_nginx_proxy_companion.nginx_proxy \
	    jwilder/nginx-proxy
```

2.  Run let's encrypt container

```
docker run -d \
    --network nginx \
    -v /home/hung/docker/nginx/certs:/etc/nginx/certs:rw \
    -v /var/run/docker.sock:/var/run/docker.sock:ro \
    --volumes-from nginx-proxy \
    jrcs/letsencrypt-nginx-proxy-companion
```

3.  Run jenkins (or something else) to generate certificates

```
/var/run/docker.sock:/var/run/docker.sock -e "LETSENCRYPT_EMAIL=muaiphone123@gmail.com" -e "LETSENCRYPT_HOST=sitename.danghung.top"  -e "VIRTUAL_HOST=sitename.danghung.top" -e VIRTUAL_PORT=8080 jenkins
```

4.  Open /home/hung/docker/nginx/conf.d/default, copy content sitename.danghung.top. Create a new file sitename.conf to paste those contents.
    Fix content to open index.html files (see example manga.conf)

5.  Copy frondend code to /home/frontend, copy manga.conf to /home/nginx/conf.d

6.  Restart nginx container (stop and start again)
