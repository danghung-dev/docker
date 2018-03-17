FROM alpine:latest
WORKDIR /app

ENV NODE_ENV=production
ENV PORT=5040
ENV JWT_SECRET=0a6b944d-d2fb-46fc-a85e-0295c986cd9f
ENV MONGO_HOST=mongodb://mongo/web_manga
ENV LETSENCRYPT_EMAIL=muaiphone123@gmail.com
ENV LETSENCRYPT_HOST=manga.server.danghung.top
ENV VIRTUAL_HOST=manga.server.danghung.top
ENV VIRTUAL_PORT=5040

EXPOSE 5040

# install required libs
RUN apk update && apk add --no-cache libstdc++ libgcc

# copy prebuilt binary from previous step
COPY ./pkg/linux /app
CMD ["/app/linux"]