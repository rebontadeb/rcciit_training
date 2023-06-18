# PODMAN TAG

## Tag the existing image with a new tag of the repository.
```
podman tag my-sample-app:v1 quay.io/test_app/basics/my-sample-app:v1 
```

## Check the newly tagged image in local repository

```
podman images 
```
or
```
podman image ls 
```