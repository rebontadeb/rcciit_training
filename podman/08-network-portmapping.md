# PODMAN NETWORK PORT MAPPING


If we want to access any port inside the container into `localhost`,
We can map the internal port to a port in `localhost`.

Then we can access the application using the port.

## Example: 

### Web Server:
```
podman run -d --name nginx-web -p 38080:80 docker.io/library/nginx:latest
```
### Database Server:
```
podman run -d --name mysql-db -p 33060:3306 docker.io/library/mysql:latest
```