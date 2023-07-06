# PODMAN DELETE CONTAINER AND IMAGE


## DELETE CONTAINERS : Use podman client to delete a container.

`podman rm  <value of CONTAINER ID>` or `podman rm <value of NAMES>`

or forcefully

`podman rm  -f <value of CONTAINER ID>` or `podman rm -f <value of NAMES>`


## DELETE IMAGES : Use podman client to delete a inage.
First we will grab the value of `IMAGE ID` from the command output of `podman images -a` or  `podman image ls -a`.

Then use the respective value to delete the image from local repositoy.
`podman rmi  <value of IMAGE ID>`


## DELETE ALL IMAGES : Use podman client to delete all inage.
To Delete all the images use the below command.

`podman rmi  $(podman images -aq)`
