# PODMAN LOGS.


## Check Logs of Container.
If you want to check logs of a running or stopped containers,first we will grab the value of `CONTAINER ID` or `NAMES` from the command output of `podman ps` or `podman ps -a`.

Then use the respective value to check the logs of the container.

`podman logs <value of CONTAINER ID>` or `podman logs <value of NAMES>` 

If you want to stram the logs continouously use:

`podman logs -f <value of CONTAINER ID>` or `podman logs -f <value of NAMES>` 

