# 1. yarn install
# 2. yarn build
# 3. docker build -t mangaclient .
# 4. docker run -d  -e "VIRTUAL_HOST=mymanga.com" -v /Users/danghung/projects/manga/client/uploads:/usr/share/nginx/html/uploads  mangaclient
FROM nginx:1.12-alpine
MAINTAINER  hung.dang980@gmail.com

COPY build /usr/share/nginx/html

# If we need images folder, when run a docker add -v
# -v /Users/danghung/projects/manga/client/uploads:/usr/share/nginx/html/uploads