# PODMAN NETWORK

If we want to create a network we can use the below command.
`podman network create mynet`

If we want to check if the network is created.
`podman network ls`

If we want to know the details about the network created.
`podman network inspect mynet`

If we want to delete the network created.
`podman network rm mynet`


Once the network is created we can attach the network in our container.
In this case we use `--network` flag.

```
podman run -d --name sample-app --network mynet quay.io/basics/my-sample-app:v1 
```