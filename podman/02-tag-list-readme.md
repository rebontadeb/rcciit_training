# PODMAN TAG

## Tag the existing image with a new tag of the repository.
```
podman tag my-sample-app:v1 quay.io/basics/my-sample-app:v1 
```

Here `basics` is the username of remote repository. 
In this case check the username from your personal remote repository `quay.io` 

![title](images/quay-io-repository.png)

or `docker.io`

![title](images/docker-hub-repository.png)


## Check the newly tagged image in local repository

```
podman images 
```
or
```
podman image ls 
```
