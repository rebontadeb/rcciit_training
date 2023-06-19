# PODMAN BUILD

## Create a shell script with name date.sh
```
while true
do
        date |tee /proc/$$/fd/1 >> /tmp/app.log
        sleep 2
done
```
## Create a file Named Containerfile with the below contents
```
FROM alpine:latest
RUN mkdir -p /app
RUN mkdir -p /var/myapp/log
COPY date.sh /app
RUN chmod +x /app/date.sh
ENTRYPOINT ["sh"]
CMD ["/app/date.sh"]
```
## Run the below command to build the image
```
podman build -t my-sample-app:v1 .
```
or
```
podman build -t my-sample-app:v1 -f Containerfile
```
## List the newly created image in the local repository
```
podman images 
```
or
```
podman image ls 
```

[![Docker Repository on Quay](https://quay.io/repository/rebontadeb/training/my-sample-app/status "Docker Repository on Quay")](https://quay.io/repository/rebontadeb/training/my-sample-app)
