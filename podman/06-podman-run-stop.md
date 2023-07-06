# PODMAN START , STOP , RUN A IMAGE

## RUN CONTAINERS : Use podman client to run a image .
```
podman run quay.io/basics/my-sample-app:v1 
``` 
or 

```
podman run docker.io/basics/my-sample-app:v1 
```

This allows us to run the application but in foreground.
To run the application in background we need to provide `-d` flag which stands for `daemon`

```
podman run -d quay.io/basics/my-sample-app:v1 
``` 
or 

```
podman run -d docker.io/basics/my-sample-app:v1 
```
If we want the container needs to be run with our own defined name 
we can run it using the `--name` flag.

```
podman run -d --name sample-app quay.io/basics/my-sample-app:v1 
```


## LIST CONTAINERS : Use podman client to list running container or stopped or failed continer.
` podman ps ` -- For listing the running containers.

` podman ps -a ` -- For listing all the running,stopped or failed containers.

## START CONTAINERS : Use podman client to stop a running container.
First we will grab the value of `CONTAINER ID` or `NAMES` from the command output of `podman ps -a`.
Then use the respective value to stop the running container.

`podman start <value of CONTAINER ID>`
or
`podman start <value of NAMES>`


## STOP CONTAINERS : Use podman client to start a stopped container.


First we will grab the value of `CONTAINER ID` or `NAMES` from the command output of `podman ps`.
Then use the respective value to stop the running container.

`podman stop <value of CONTAINER ID>`
or
`podman stop <value of NAMES>`
