# PODMAN PUSH , PULL and SAVE

## Push the existing tagged image with a new tag of your own repository.
```
podman push quay.io/basics/my-sample-app:v1 
```

Here `basics` is the username of remote repository. 
In this case check the username from your personal remote repository `quay.io` 

![title](images/quay-io-repository.png)

or `docker.io`

![title](images/docker-hub-repository.png)

## Once the Image is successfully pushed the image can be again pulled to the local registry from remote registry.
```
podman pull quay.io/basics/my-sample-app:v1 
```

## Save a image to be shipped in TAR or ZIP format.

Use the below command to save the command in Tar or Zip format

`podman save -o image.tar.gz image`