# INSTALL KUBERNETES USING KUBEADM

## Pre-Requisites
1. Compatible Linux host(s).
2. First identify how many Leader nodes and How many Follower nodes are to be deployed.
3. Ensure you are having `root` user access for these nodes.
4. Ensure you are having internet access from these nodes.
5. 2 GB or more of RAM per machine and 2 CPUs or more. (any less will leave little room for your apps).
7. Unique hostname, MAC address, and product_uuid for every node.
8. Certain [ports](#Ports Need to be available by default.) are open on your machines.
9. Swap disabled. You MUST disable swap in order for the kubelet to work properly.

## Ports Need to be available by default.
Leader Nodes:
| Protocol    | Direction | Port Range  | Purpose                 | Used By             |
| --------    | --------  | --------    | ---------------------   | ---------------     |
| TCP         | Inbound   | 6443        | Kubernetes API server   | All                 |
| TCP         | Inbound   | 2379-2380   | etcd server client API  | kube-apiserver, etcd|
| TCP         | Inbound   | 10250       | Kubelet API             | Self, Control plane |
| TCP         | Inbound   | 10259       | kube-scheduler          | Self                |
| TCP         | Inbound   | 10257       | kube-controller-manager | Self                |

Follower Nodes:
| Protocol    | Direction | Port Range  | Purpose                 | Used By             |
| --------    | --------  | --------    | ---------------------   | ---------------     |
| TCP         | Inbound   | 10250       | Kubelet API             | Self, Leader        |
| TCP         | Inbound   | 30000-32767 | NodePort Services†      | All                 |
