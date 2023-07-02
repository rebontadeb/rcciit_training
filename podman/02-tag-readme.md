# PODMAN TAG

## Tag the existing image with a new tag of the repository.
```
podman tag my-sample-app:v1 quay.io/basics/my-sample-app:v1 
```

Here `basics` is the username of remote repository. In this case it is either `quay.io` or `docker.io`


## Check the newly tagged image in local repository

```
podman images 
```
or
```
podman image ls 
```
