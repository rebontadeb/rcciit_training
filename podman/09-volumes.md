# PODMAN VOLUMES

If we want to create a volume we can use the below command.
`podman volume create myvolume`

If we want to check if the volume is created.
`podman volume ls`

If we want to know the details about the volume created.
`podman volume inspect myvolume`

If we want to delete the volume created.
`podman volume rm myvolume`


Once the volume is created we can attach the volume in our container.
In this case we use `-v` flag.
```
podman run -d --name sample-app -v myvolume:/tmp quay.io/basics/my-sample-app:v1 
```